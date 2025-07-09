# Citcuit Breaker
The **Circuit Breaker Pattern** is one of the most **essential patterns for building resilient microservices**.

<img width="1102" alt="Screenshot 2025-07-09 at 6 43 41 PM" src="https://github.com/user-attachments/assets/6f5f8414-762b-4b24-bb1e-3f5b43fe2886" />
<img width="1091" alt="Screenshot 2025-07-09 at 6 44 12 PM" src="https://github.com/user-attachments/assets/580753c2-539b-4a63-b451-2accf9f8d95b" />
<img width="1078" alt="Screenshot 2025-07-09 at 6 44 19 PM" src="https://github.com/user-attachments/assets/3f1ad9d9-047b-488b-8cdd-580179204b49" />
<img width="736" alt="Screenshot 2025-07-09 at 6 46 18 PM" src="https://github.com/user-attachments/assets/5e122b10-46ae-4f72-b5b4-002d851322ac" />
<img width="1103" alt="Screenshot 2025-07-09 at 6 47 15 PM" src="https://github.com/user-attachments/assets/a96d6226-541f-466f-9b38-a70336accd36" />

## 🧠 Why Do We Need a Circuit Breaker?

Suppose your service (A) calls another service (B) which is **down** or **very slow**.

Without a circuit breaker:

* Every request to B keeps failing or timing out.
* Threads get stuck, resources exhausted.
* **Cascading failure**: Service A becomes slow or crashes too.

🧨 **Problem**: Your app wastes time and threads calling something that’s already broken.

## ✅ What Is the Circuit Breaker Pattern?

A **Circuit Breaker** acts like a **firewall** between your app and the failing service.

It has **3 states**:

```
         ┌────────────┐
         │   Closed   │──── Service is healthy ───▶ Calls go through
         └────┬───────┘
              │ Failures exceed threshold
              ▼
         ┌────────────┐
         │   Open     │──── Service is failing ───▶ Calls are blocked immediately
         └────┬───────┘
              │ Wait timeout expires
              ▼
         ┌────────────┐
         │ Half-Open  │──── Trial calls are allowed to test recovery
         └────────────┘
```

#### 🔁 Lifecycle in Simple Terms:

| State         | What Happens                                                             |
| ------------- | ------------------------------------------------------------------------ |
| **Closed**    | All calls are allowed. If too many fail, go to **Open**.                 |
| **Open**      | No calls go through. After `X` seconds, go to **Half-Open**.             |
| **Half-Open** | Try one or two calls. If success → go **Closed**, else → **Open** again. |

#### 🎯 Real-World Analogy

> Imagine calling a friend whose phone is always switched off.

* You try 5 times — still switched off (failures).
* You stop calling for 1 minute (**Open state**).
* Then try again after a while (**Half-Open**).
* If it connects, you start calling normally again (**Closed**).

## Circuit Breaker parameter

<img width="987" alt="Screenshot 2025-07-09 at 6 55 48 PM" src="https://github.com/user-attachments/assets/5473e0ed-cb94-42b6-a6b8-399a8c19287a" />
<img width="938" alt="Screenshot 2025-07-09 at 6 59 56 PM" src="https://github.com/user-attachments/assets/1376a340-6f1e-45ae-8e27-00223b2018f8" />
<img width="980" alt="Screenshot 2025-07-09 at 7 02 37 PM" src="https://github.com/user-attachments/assets/63e1ed58-e708-4dab-b85d-655ee98d5834" />
<img width="1095" alt="Screenshot 2025-07-09 at 7 05 50 PM" src="https://github.com/user-attachments/assets/6d28bda6-1e08-4bf3-b522-4b7766a2e454" />

## What to do when a circuit breaks

<img width="867" alt="Screenshot 2025-07-09 at 7 10 19 PM" src="https://github.com/user-attachments/assets/4416219e-fc94-4119-adde-8bde12c92af2" />
<img width="1003" alt="Screenshot 2025-07-09 at 7 10 53 PM" src="https://github.com/user-attachments/assets/16a7067d-5919-4d7f-afd4-212f27a96b7b" />
<img width="1017" alt="Screenshot 2025-07-09 at 7 12 32 PM" src="https://github.com/user-attachments/assets/a6ecf0c2-d689-47a5-8dca-12459a6f4a39" />

## Why circuit breakers

<img width="996" alt="Screenshot 2025-07-09 at 7 16 19 PM" src="https://github.com/user-attachments/assets/467a6991-fd16-4b8e-8eee-d7d698126f54" />
<img width="1109" alt="Screenshot 2025-07-09 at 7 16 46 PM" src="https://github.com/user-attachments/assets/1d0761fd-8f75-4ab4-8185-5bcdf88d5a7e" />

# 💻 Implementing Circuit Breaker in Spring Boot using Resilience4j

Add to `pom.xml`:

```xml
<dependency>
  <groupId>io.github.resilience4j</groupId>
  <artifactId>resilience4j-spring-boot3</artifactId>
</dependency>
```

### ✅ Step 1: Annotate your method

```java
@CircuitBreaker(name = "paymentService", fallbackMethod = "fallbackPayment")
public String callPaymentService() {
    return restTemplate.getForObject("http://external-payment-api/pay", String.class);
}
```

### ✅ Step 2: Fallback method

```java
public String fallbackPayment(Throwable t) {
    return "Payment service is currently unavailable. Please try later.";
}
```

---

## ⚙️ Configure the Circuit Breaker (Optional)

In `application.yml`:

```yaml
resilience4j:
  circuitbreaker:
    instances:
      paymentService:
        failure-rate-threshold: 50
        minimum-number-of-calls: 10
        wait-duration-in-open-state: 10s
        sliding-window-size: 20
```

**Explanation:**

* If **50% of 10 calls fail**, circuit opens.
* Wait 10s before trying again.
* Use a window of 20 calls to track failures.

---

## 🔄 Summary

| Term      | Meaning                                            |
| --------- | -------------------------------------------------- |
| Closed    | Normal state — calls allowed                       |
| Open      | Failing state — calls blocked to protect resources |
| Half-Open | Trial state — allows a few calls to test recovery  |
| Fallback  | Optional method to return a default response       |

---

### ✅ Benefits:

* Protects your app from cascading failures
* Improves performance during downstream outages
* Provides graceful fallback options

---

# Extra (Read if time permits)

### ✅ Step 1: Add Required Dependencies

If using Spring Boot 3.x:

```xml
<dependency>
    <groupId>io.github.resilience4j</groupId>
    <artifactId>resilience4j-spring-boot3</artifactId>
</dependency>
```

Also add:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-aop</artifactId>
</dependency>
```

---

### ✅ Step 2: Annotate Your Method

```java
@CircuitBreaker(name = "movieInfoCB", fallbackMethod = "getFallbackMovieInfo")
public Movie getMovieInfo(String movieId) {
    return restTemplate.getForObject("http://external-moviedb.com/info/" + movieId, Movie.class);
}

public Movie getFallbackMovieInfo(String movieId, Throwable ex) {
    return new Movie(movieId, "Title unavailable", "MovieDB service is currently down");
}
```

**🧠 Resilience4j passes the **exception** to the fallback method — unlike Hystrix which doesn’t require it by default.**

---

### ✅ Step 3: Add Configuration in `application.yml`

```yaml
resilience4j:
  circuitbreaker:
    instances:
      movieInfoCB:
        slidingWindowType: COUNT_BASED
        slidingWindowSize: 10               # Last 10 calls
        minimumNumberOfCalls: 5
        failureRateThreshold: 50            # Open if 50% fail
        waitDurationInOpenState: 10s        # Stay open for 10 seconds
        permittedNumberOfCallsInHalfOpenState: 2
        automaticTransitionFromOpenToHalfOpenEnabled: true
        recordExceptions:
          - java.io.IOException
          - java.util.concurrent.TimeoutException
        ignoreExceptions:
          - com.yourapp.MovieNotFoundException
```

---

### ✅ Optional: Add Timeout (TimeLimiter) for Async Calls

If you make the method `@Async` or `CompletableFuture` based:

```java
@TimeLimiter(name = "movieInfoCB", fallbackMethod = "getFallbackMovieInfo")
@CircuitBreaker(name = "movieInfoCB", fallbackMethod = "getFallbackMovieInfo")
public CompletableFuture<Movie> getMovieInfo(String movieId) {
    return CompletableFuture.supplyAsync(() -> {
        return restTemplate.getForObject("http://external-moviedb.com/info/" + movieId, Movie.class);
    });
}

public CompletableFuture<Movie> getFallbackMovieInfo(String movieId, Throwable t) {
    return CompletableFuture.completedFuture(new Movie(movieId, "Fallback", "MovieDB is down"));
}
```

You also configure timeout duration:

```yaml
resilience4j:
  timelimiter:
    instances:
      movieInfoCB:
        timeoutDuration: 3s
```

---

### 🔁 Optional: Add Retry for Temporary Failures

```java
@Retry(name = "movieInfoRetry", fallbackMethod = "getFallbackMovieInfo")
```

```yaml
resilience4j:
  retry:
    instances:
      movieInfoRetry:
        maxAttempts: 3
        waitDuration: 1s
```

---

### ✅ Final Summary

| Feature        | Hystrix                 | Resilience4j                                |
| -------------- | ----------------------- | ------------------------------------------- |
| Annotation     | `@HystrixCommand`       | `@CircuitBreaker`, `@Retry`, `@TimeLimiter` |
| Fallback Param | Optional                | Must accept `Throwable`                     |
| Timeout config | YAML + Hystrix internal | Use `TimeLimiter`                           |
| Isolation      | Thread (default)        | None by default, but can customize          |
| Future proof   | ❌ Deprecated            | ✅ Maintained and modern                     |

---
