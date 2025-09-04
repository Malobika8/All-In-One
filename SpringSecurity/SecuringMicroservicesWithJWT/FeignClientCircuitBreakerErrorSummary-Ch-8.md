## 🔎 When does **Feign fallback** vs **CircuitBreaker fallback** apply?

### 1. **Product-service is completely DOWN**

* Eureka → no healthy instance for `product-service`.
* The error is thrown **before Feign makes the HTTP call** (comes from `LoadBalancerClient`).
* 👉 In this case, **Feign fallback** (`fallback = ...` in `@FeignClient`) will trigger.
* CircuitBreaker does not get a chance here unless you explicitly wrap it.

---

### 2. **Product-service is UP but failing internally**

* Example: `/products` returns **500 Internal Server Error** or **503 Service Unavailable**.
* Eureka can find the service → Feign sends the HTTP request.
* Response comes back with an error code.
* 👉 CircuitBreaker wraps the Feign call and will:

  * Count this as a failure.
  * Potentially open the circuit after thresholds.
  * Trigger **CircuitBreaker fallback**.

---

### 3. **Wrapping all Feign errors**

If you want **one consistent place** to handle *all* Feign-related errors (both service down & HTTP failures):

👉 Use:

```java
circuitBreakerFactory.create("productServiceCircuitBreaker")
    .run(productClient::getProducts, this::fallbackOrders);
```

This way:

* **LoadBalancer errors** (service not found in Eureka)
* **Feign errors** (HTTP 500/503 etc.)
  …all get caught by **CircuitBreaker** → one fallback method.

---

## ✅ Which one to use when?

* **Feign Fallback**

  * Best if you want **per-client localized fallback logic**.
  * Example: Each Feign client has its own default response (`ProductClientFallback`, `CustomerClientFallback`).

* **CircuitBreaker Fallback**

  * Best when you want **centralized error handling & resilience patterns** (timeouts, retry, circuit open/close, metrics).
  * Example: Counting errors, applying retry, bulkhead isolation, etc.

* **Both Together (recommended)**

  * Feign fallback for **quick, service-specific defaults**.
  * CircuitBreaker for **resilience policies + global fallback**.

---

✅ **Rule of Thumb**

* If service **not discoverable → Feign fallback**.
* If service is up but **unhealthy/slow → CircuitBreaker fallback**.
* If you want to **handle everything consistently** → wrap Feign calls in `circuitBreakerFactory.create().run(...)`.

---

