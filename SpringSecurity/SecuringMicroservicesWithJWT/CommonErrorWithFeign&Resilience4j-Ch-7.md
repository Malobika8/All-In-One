# We might come across an error when the product-service is down and we try to hit the api of the order-service

```java
2025-09-04T13:01:32.012+05:30  WARN 1810 --- [order-service] [nio-8082-exec-7] o.s.c.l.core.RoundRobinLoadBalancer      : No servers available for service: product-service
2025-09-04T13:01:32.012+05:30  WARN 1810 --- [order-service] [nio-8082-exec-7] .s.c.o.l.FeignBlockingLoadBalancerClient : Load balancer does not contain an instance for the service product-service
2025-09-04T13:01:32.014+05:30 ERROR 1810 --- [order-service] [nio-8082-exec-7] o.a.c.c.C.[.[.[/].[dispatcherServlet]    : Servlet.service() for servlet [dispatcherServlet] in context with path [] threw exception [Request processing failed: feign.FeignException$ServiceUnavailable: [503] during [GET] to [http://product-service/products] [ProductClient#getProducts()]: [Load balancer does not contain an instance for the service product-service]] with root cause

feign.FeignException$ServiceUnavailable: [503] during [GET] to [http://product-service/products] [ProductClient#getProducts()]: [Load balancer does not contain an instance for the service product-service]
	at feign.FeignException.serverErrorStatus(FeignException.java:287) ~[feign-core-13.6.jar:na]
```

---

### 🔎 What’s happening?

* `order-service` uses **Feign + Eureka** to call `product-service`.
* When `product-service` is running → everything works fine.
* When `product-service` is down → **Feign asks Eureka for an instance**, but Eureka replies **no instance available** → you see:

```
Load balancer does not contain an instance for the service product-service
```

and Feign throws **503 ServiceUnavailable**.

---

### 🔹 Why isn’t Resilience4j catching it?

Resilience4j **CircuitBreaker** should wrap this exception and go to our **fallback method**.
But Feign throws a specific exception (`FeignException$ServiceUnavailable`) and sometimes the fallback doesn’t trigger unless configured properly.

---

# Feign Client + Resilience4j CircuitBreaker in Microservices

## 🔹 1. Types of Failures in Service-to-Service Calls

When `order-service` calls `product-service` via Feign, failures can be of two kinds:

1. **Service Unavailable (No Instance Found in Eureka / Service Down)**

   * Error:

     ```
     Load balancer does not contain an instance for product-service
     ```
   * Occurs when the service is not registered in Eureka or is down.
   * Happens **before Feign actually makes an HTTP call**.

2. **Service Available but Internal Error (HTTP 500, 503, Timeout, etc.)**

   * Error thrown by Feign: `FeignException$InternalServerError`, `FeignException$ServiceUnavailable`
   * Happens **after the HTTP request reaches the service** but it fails internally.

---

## 🔹 2. Feign Fallback vs CircuitBreaker

### ✅ Feign Fallback

* Configured via `@FeignClient(fallback = ...)`.
* Runs immediately if Feign **cannot complete the call**.
* Good for **simple failover logic** (e.g., return dummy/default data).
* **Limitations:**

  * Always runs on failure, no circuit breaker states (open/closed/half-open).
  * No retries, no monitoring, no thresholding.

**When to use?**

* For lightweight services where you just want a “default response” if the call fails.
* Example: Returning cached or dummy products list when `product-service` is down.

---

### ✅ CircuitBreaker with Resilience4j

* Wraps Feign calls with retry, monitoring, and circuit breaker states.
* Provides:

  * **Failure thresholds** (`failureRateThreshold`, `slidingWindowSize`).
  * **Open/closed states** for preventing flooding a failing service.
  * **Fallback methods** only after failure conditions are met.

**When to use?**

* For critical flows where failing fast or retrying is important.
* Example: Payment service calling Inventory service — you may want retries, then fallback if service consistently fails.

---

## 🔹 3. Why CircuitBreaker Didn’t Catch `NoInstanceAvailable`

* If `product-service` is **completely down**, the error happens in `LoadBalancerClient` before Feign executes.
* Solution: **Manually wrap Feign call with `CircuitBreakerFactory.run(...)`**.
* This ensures all errors (service not found, 500s, timeouts) are caught.

---

## 🔹 4. Differentiating Between Service Down vs HTTP 500

Inside the fallback method, check the type of exception:

```java
public List<String> getDefaultOrders(Throwable throwable) {
    if (throwable instanceof FeignException) {
        FeignException fe = (FeignException) throwable;

        if (fe.status() == 500) {
            return List.of("Fallback due to Internal Server Error");
        } else if (fe.status() == 503) {
            return List.of("Fallback due to Service Unavailable");
        }
    }

    if (throwable instanceof IllegalStateException && throwable.getMessage().contains("Load balancer")) {
        return List.of("Fallback due to service down (no instance in Eureka)");
    }

    return List.of("Generic fallback order");
}
```

---

## 🔹 5. Integration Strategies

| Scenario                                                      | Recommended Approach                                                                        |
| ------------------------------------------------------------- | ------------------------------------------------------------------------------------------- |
| **Service down / not registered in Eureka**                   | Wrap Feign call with `CircuitBreakerFactory.run(...)` → fallback when no instance available |
| **Service up but throwing errors (500, 503, etc.)**           | Use `@CircuitBreaker` or Feign fallback → inspect exception for HTTP status                 |
| **Simple “default response” always needed**                   | Use Feign fallback (`fallback = ...`)                                                       |
| **Critical flows needing retries, monitoring, fail-fast**     | Use Resilience4j CircuitBreaker with Feign integration                                      |
| **Mixed (sometimes default data, sometimes retry + circuit)** | Combine Feign + Resilience4j (`spring.cloud.openfeign.circuitbreaker.enabled: true`)        |

---

## 🔹 6. Best Practices

1. **Start simple** with Feign fallback for non-critical services.
2. **Upgrade to CircuitBreaker** for critical paths (payments, inventory, authentication).
3. **Combine with Retry** (`resilience4j.retry`) for transient failures like network glitches.
4. **Expose CircuitBreaker metrics** to monitoring (Actuator + Micrometer + Prometheus).
5. **Differentiate fallback reasons** in logs, so ops team can tell if the failure is service-down vs internal error.

---

✅ **Summary:**

* Use **Feign fallback** for simple defaults.
* Use **Resilience4j CircuitBreaker** for resilience and retries.
* To catch “no instance in Eureka” errors, wrap Feign with `CircuitBreakerFactory.run(...)`.
* Inspect `Throwable` in fallback to tell **service down** vs **HTTP error**.

---

## 4️⃣ Order Service (Consumer with Feign + Resilience4j)

**`application.yml`**

```yaml
server:
  port: 8082

spring:
  application:
    name: order-service

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/

feign:
  circuitbreaker:
    enabled: true   # Feign integrates with Resilience4j
```

---

### (a) Feign Client

```java
@FeignClient(name = "product-service")
public interface ProductClient {
    @GetMapping("/products")
    List<String> getProducts();
}
```

---

### (b) Service Layer with CircuitBreaker

Here we integrate **Feign + Resilience4j** so we can handle:

* Service down (`no instance in Eureka`)
* Service errors (500, 503, etc.)

```java
@Service
public class OrderService {

    private final ProductClient productClient;
    private final CircuitBreakerFactory<?, ?> circuitBreakerFactory;

    public OrderService(ProductClient productClient, CircuitBreakerFactory<?, ?> circuitBreakerFactory) {
        this.productClient = productClient;
        this.circuitBreakerFactory = circuitBreakerFactory;
    }

    public List<String> getOrders() {
        return circuitBreakerFactory.create("productServiceCircuitBreaker")
                .run(productClient::getProducts, this::fallbackOrders);
    }

    // ✅ Fallback method
    private List<String> fallbackOrders(Throwable throwable) {
        if (throwable instanceof FeignException) {
            FeignException fe = (FeignException) throwable;
            if (fe.status() == 500) {
                return List.of("Fallback: Product service error (500)");
            } else if (fe.status() == 503) {
                return List.of("Fallback: Product service unavailable (503)");
            }
        }
        if (throwable instanceof IllegalStateException && throwable.getMessage().contains("Load balancer")) {
            return List.of("Fallback: Product service DOWN (not in Eureka)");
        }
        return List.of("Fallback: Generic order response");
    }
}
```

---

# ✅ Behavior Summary

1. **If Product Service is UP**

   * `/orders` → returns products list via Feign.

2. **If Product Service returns 500 / 503**

   * CircuitBreaker catches FeignException → fallback returns error-specific message.

3. **If Product Service is DOWN (not registered in Eureka)**

   * Load balancer error caught by CircuitBreaker → fallback returns “service DOWN” message.

---

# Feign fallback: Extra improvement (Optional)

If you want to **customize fallbacks per Feign client**, you can also define a fallback class:

```java
@FeignClient(name = "product-service", fallback = ProductClientFallback.class)
public interface ProductClient {
    @GetMapping("/products")
    List<String> getProducts();
}

@Component
class ProductClientFallback implements ProductClient {
    @Override
    public List<String> getProducts() {
        return List.of("Default Product A", "Default Product B");
    }
}
```

## Feign integration with resilience

<img width="1047" height="491" alt="Screenshot 2025-09-04 at 1 12 33 PM" src="https://github.com/user-attachments/assets/5f7f0aed-68df-4a9d-aa32-007246f34d16" />
