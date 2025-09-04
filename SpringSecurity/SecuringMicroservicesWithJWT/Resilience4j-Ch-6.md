# Step 7 — Add Resilience4j to order-service

## 1️⃣ Add dependencies (`order-service/pom.xml`)

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-circuitbreaker-resilience4j</artifactId>
</dependency>
```

*(We already have Feign — this integrates with it nicely.)*

---

## 2️⃣ Update `application.yml` (order-service)

```yaml
resilience4j:
  circuitbreaker:
    instances:
      productServiceCircuitBreaker:   # 👈 name of the circuit breaker
        registerHealthIndicator: true
        slidingWindowSize: 5
        failureRateThreshold: 50
        waitDurationInOpenState: 10s
```

---

## 3️⃣ Add Circuit Breaker around Feign call

Modify `OrderController`:

```java
@RestController
@RequestMapping("/orders")
public class OrderController {

    private final ProductClient productClient;

    public OrderController(ProductClient productClient) {
        this.productClient = productClient;
    }

    @GetMapping
    @CircuitBreaker(name = "productServiceCircuitBreaker", fallbackMethod = "getDefaultOrders")
    public List<String> getOrders() {
        List<String> products = productClient.getProducts(); // may fail if product-service is down
        return List.of("Order1 with " + products.get(0),
                       "Order2 with " + products.get(1));
    }

    // 👇 fallback method (same signature + Throwable param optional)
    public List<String> getDefaultOrders(Throwable throwable) {
        return List.of("Default Order1", "Default Order2");
    }
}
```

---

## 4️⃣ Test it

1. Start everything (`discovery-server`, `product-service`, `order-service`).
2. Call: [http://localhost:8082/orders](http://localhost:8082/orders) → works normally.
3. Now stop `product-service`.
4. Call again: [http://localhost:8082/orders](http://localhost:8082/orders) → should return fallback:

```json
[
  "Default Order1",
  "Default Order2"
]
```

✅ That’s **Resilience4j with Feign + CircuitBreaker + Fallback** 🎉

---

