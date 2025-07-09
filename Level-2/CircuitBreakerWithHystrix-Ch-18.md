# Hystrix

<img width="993" alt="Screenshot 2025-07-09 at 7 57 24 PM" src="https://github.com/user-attachments/assets/397c5596-4501-4eb6-a4d7-dbbdefcaa881" />
<img width="1069" alt="Screenshot 2025-07-09 at 8 01 41 PM" src="https://github.com/user-attachments/assets/534586a0-c677-4bb3-913f-32b437107d00" />

## 🎯 What is Hystrix?

**Hystrix** is a **latency and fault-tolerance** library from Netflix. It wraps calls to external services and:

* Detects failures
* Stops cascading failures
* Provides fallbacks
* Uses **Circuit Breaker**, **Timeouts**, **Thread isolation**, etc.

> ⚠️ **Note**: Hystrix is now in **maintenance mode**. Spring Cloud replaced it with **Resilience4j**, but many legacy systems still use Hystrix.

---

## 🧱 Your Scenario:

Movie Catalog Service → calls:

* `MovieInfoService.getMovieInfo(movieId)` → calls **slow MovieDB**
* We wrap this with Hystrix to **fail fast** and provide a fallback movie.

---

## ✅ Step-by-Step: Hystrix in Movie Catalog

### 1. **Add Hystrix Dependency**

If using Spring Boot:

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-hystrix</artifactId>
</dependency>
```

---

### 2. **Enable Hystrix**

```java
@SpringBootApplication
@EnableCircuitBreaker  // Enables Hystrix in Spring Boot
public class MovieCatalogApp { }
```

---

### 3. **Wrap Your Method with @HystrixCommand**

```java
@Service
public class MovieInfoService {

    @HystrixCommand(fallbackMethod = "getFallbackMovieInfo")
    public Movie getMovieInfo(String movieId) {
        return restTemplate.getForObject("http://external-moviedb.com/info/" + movieId, Movie.class);
    }

    public Movie getFallbackMovieInfo(String movieId) {
        return new Movie(movieId, "Unavailable", "MovieDB is down");
    }
}
```

<img width="1122" alt="Screenshot 2025-07-09 at 8 10 22 PM" src="https://github.com/user-attachments/assets/702938c4-a268-4735-8b0e-0edb08b47c52" />

With default circuit breaker config,

<img width="747" alt="Screenshot 2025-07-09 at 8 11 26 PM" src="https://github.com/user-attachments/assets/ae797c3d-2d15-4830-83d3-4bcf9a12702f" />

---

### 4. **Set Timeout & Circuit Breaker Config (Optional)**

In `application.yml`:

```yaml
hystrix:
  command:
    default:
      execution:
        isolation:
          thread:
            timeoutInMilliseconds: 3000   # Timeout for external call
      circuitBreaker:
        requestVolumeThreshold: 10        # Min 10 requests to evaluate
        errorThresholdPercentage: 50      # >50% failure triggers OPEN state
        sleepWindowInMilliseconds: 10000  # Wait 10s before trying again
```

---

## 🧠 What Hystrix Offers (Built-in)

| Feature                    | Purpose                                            |
| -------------------------- | -------------------------------------------------- |
| `@HystrixCommand`          | Wraps method with circuit breaker logic            |
| Fallback method            | Alternate logic when main call fails               |
| Timeout                    | Stops waiting on slow services                     |
| Thread Isolation (default) | Each call runs in its own thread to avoid blocking |
| Circuit Breaker            | Opens to block bad calls after threshold           |

---

## ⚠️ Hystrix vs Resilience4j

| Feature          | Hystrix                    | Resilience4j                       |
| ---------------- | -------------------------- | ---------------------------------- |
| Status           | Maintenance mode (stopped) | Actively maintained                |
| Built for        | Netflix OSS, Spring Cloud  | Java 8+, functional style          |
| Thread isolation | YES (default)              | Optional                           |
| Reactor support  | Weak                       | Strong (supports WebFlux, RxJava)  |
| Configuration    | XML/YAML + annotation      | Fluent Java API or YAML            |
| Performance      | Slightly heavier           | Lightweight, better for modern use |

---

## ✅ Summary (In Context)

You should wrap the slow **MovieDB call** inside a `@HystrixCommand` to:

* Apply a **timeout**
* Use a **fallback**
* Open the **circuit** if failures > threshold
* Return fallback to **CatalogService** instantly without blocking threads

---
