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

### ✅ Fix: Tell Feign to use Resilience4j

In **order-service** `application.yml`:

```yaml
spring:
  cloud:
    openfeign:
      circuitbreaker:
        enabled: true
```

This makes Feign integrate directly with Resilience4j’s circuit breaker.

---

### 🔹 Updated Flow

1. `order-service` → Feign tries calling `product-service`.
2. Eureka says “no instance available” → Feign throws exception.
3. Because **Feign CircuitBreaker is enabled**, Resilience4j catches it.
4. Your `@CircuitBreaker` annotated method triggers the **fallback**.

---

### 🔧 Extra improvement (Optional)

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

This way, you don’t even need `@CircuitBreaker` at controller level — Feign itself handles fallback.

---

✅ With these changes, if `product-service` is **down**, you should get your **fallback orders** instead of a **503 error**.

---

Do you want me to update our setup using **Feign fallback class** (cleaner approach) or stick with `@CircuitBreaker` + fallback method?
