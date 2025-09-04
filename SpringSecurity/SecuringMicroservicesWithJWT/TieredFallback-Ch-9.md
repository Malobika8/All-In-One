A **tiered fallback approach** where:

1. **Feign fallback** = first safety net (per-client defaults).
2. **CircuitBreaker fallback** = second safety net (global resilience fallback).

---

## 1️⃣ Define Feign Client + Fallback

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
        // Feign fallback (service not discoverable, load balancer error, etc.)
        return List.of("Default Product A (Feign Fallback)", "Default Product B (Feign Fallback)");
    }
}
```

✅ This catches **“no instance available in Eureka”** cases.

---

## 2️⃣ Wrap Feign Call with CircuitBreaker

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
                .run(productClient::getProducts, this::circuitBreakerFallback);
    }

    // ✅ CircuitBreaker fallback (handles Feign fallback failures, 500/503 errors, timeouts)
    private List<String> circuitBreakerFallback(Throwable throwable) {
        if (throwable instanceof FeignException) {
            FeignException fe = (FeignException) throwable;
            if (fe.status() == 500) {
                return List.of("CircuitBreaker Fallback: Product service error (500)");
            } else if (fe.status() == 503) {
                return List.of("CircuitBreaker Fallback: Product service unavailable (503)");
            }
        }
        return List.of("CircuitBreaker Fallback: Generic Order Response");
    }
}
```

---

## 3️⃣ Flow of Execution

* **Case A: Product-service DOWN (not in Eureka)**

  * Feign fails in `LoadBalancerClient`.
  * Feign fallback (`ProductClientFallback`) returns its defaults.
  * CircuitBreaker sees this as a **success** because the fallback already handled it.

* **Case B: Product-service UP but errors (500/503)**

  * Feign actually calls the service and gets error response.
  * CircuitBreaker catches `FeignException`.
  * CircuitBreaker fallback (`circuitBreakerFallback`) executes.

* **Case C: Feign fallback itself fails for some reason**

  * CircuitBreaker fallback still catches it → acts as global safety net.

---

## 4️⃣ Controller Example

```java
@RestController
@RequestMapping("/orders")
public class OrderController {

    private final OrderService orderService;

    public OrderController(OrderService orderService) {
        this.orderService = orderService;
    }

    @GetMapping
    public List<String> getOrders() {
        return orderService.getOrders();
    }
}
```

---

## ✅ Best Practices Recap

* **Use Feign fallback** for **service not registered / unavailable** → quick per-service defaults.
* **Use CircuitBreaker fallback** for **service errors / timeouts** → resilience + retry + thresholds.
* **Wrapping Feign in CircuitBreaker** = ensures **all errors** can still be contained and degraded gracefully.

---

👉 This way you get **tiered resilience**:
**Feign fallback (service-specific) → CircuitBreaker fallback (global resilience)**.

---

