# What is an API Gateway in microservices? Why do we need it? Explain with an example (Zuul or Spring Cloud Gateway). Also explain: how does routing and filtering work?

### Sol:

In a microservices architecture, there are often many services with different hostnames, ports, and APIs.
👉 It’s **not practical** for clients (e.g., frontend apps) to manage all these endpoints.

An **API Gateway** acts as a **single entry point** for all client requests. It handles:

* **Routing**: Forwards requests to the appropriate microservice.
* **Abstraction**: Hides internal service details from the client.
* **Cross-cutting concerns**:

  * Authentication & Authorization (e.g., JWT)
  * Logging & Monitoring
  * Rate Limiting / Throttling
  * Load balancing (can delegate to Eureka or others)
  * Request/Response transformations

#### Example Scenario:

Suppose we have:

* `student-service` at `/student`
* `book-service` at `/book`

Instead of hitting:

```
http://localhost:8081/student
http://localhost:8082/book
```

Clients hit:

```
http://gateway-service/student
http://gateway-service/book
```

The **API Gateway** forwards these calls based on **route configurations**.

#### Common API Gateway Tools:

1. **Spring Cloud Gateway** (modern, reactive, built on WebFlux)
2. **Zuul (Netflix)** – older but still used
3. **Kong, NGINX, AWS API Gateway** – popular in production
   
#### Spring Cloud Gateway – Example:

```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: student-service
          uri: lb://STUDENT-SERVICE
          predicates:
            - Path=/student/**
        - id: book-service
          uri: lb://BOOK-SERVICE
          predicates:
            - Path=/book/**
```

* `lb://STUDENT-SERVICE` uses **service discovery (Eureka)**.
* `Path=/student/**` means requests with `/student/...` go to that service.

#### Filtering:

Gateway can apply filters:

* **Pre-filters** (e.g., auth, logging)
* **Post-filters** (e.g., modifying response)

Example in Java config:

```java
@Bean
public RouteLocator customRoutes(RouteLocatorBuilder builder) {
    return builder.routes()
        .route("student_route", r -> r.path("/student/**")
            .filters(f -> f.addRequestHeader("X-Request-ID", UUID.randomUUID().toString()))
            .uri("lb://STUDENT-SERVICE"))
        .build();
}
```

> API Gateway **centralizes control**, simplifies clients, and supports cross-cutting concerns in a scalable way.

---

# Suppose your BookService is down, and a client requests book info via Gateway. How will you handle this failure gracefully?

### Sol:

When a microservice like **BookService** goes down, we want to prevent cascading failures and provide a **graceful degradation** of service.

#### Patterns to Handle Failures:

#### 1. **Retry**

* Automatically re-attempt failed requests a few times before giving up.
* Used when failures are **transient** (e.g., network glitch).
* Configurable via Resilience4j Retry or Spring Retry.

#### 2. **Circuit Breaker**

* Prevents repeated calls to a failing service.
* Opens the circuit after a threshold of failures.
* Requests are **short-circuited** and redirected to a **fallback method**.
* After a cooldown period, it transitions to **half-open**, then back to **closed** if the service recovers.

#### 3. **Fallbacks**

* A **default method or response** when the actual service is unavailable.
* Can return cached data, static message, or empty fallback.

#### Where to Implement Circuit Breaker?

#### a) **Inside a service (e.g., StudentService calling BookService)**

Use `@CircuitBreaker` from **Resilience4j**:

```java
@CircuitBreaker(name = "bookService", fallbackMethod = "bookFallback")
public Book getBooks(int studentId) {
    return bookClient.getBooksByStudentId(studentId);
}

public Book bookFallback(int studentId, Throwable ex) {
    return new Book("Fallback Book", "Service is down");
}
```

#### b) **At API Gateway level**

Spring Cloud Gateway integrates with **Resilience4j** or **Hystrix** (deprecated).

**Example YAML config:**

```yaml
spring:
  cloud:
    gateway:
      routes:
        - id: book-service
          uri: lb://BOOK-SERVICE
          predicates:
            - Path=/book/**
          filters:
            - name: CircuitBreaker
              args:
                name: bookCircuit
                fallbackUri: forward:/fallback/book
```

And controller for fallback:

```java
@RestController
public class FallbackController {
    
    @GetMapping("/fallback/book")
    public ResponseEntity<String> fallbackBook() {
        return ResponseEntity.ok("Book service is currently unavailable. Please try again later.");
    }
}
```

> To handle service failure, we use patterns like **Retry, Circuit Breaker, and Fallback** — implemented either inside the calling service (via Resilience4j) or at the **API Gateway layer**.
> This ensures the system stays **resilient**, avoids unnecessary strain on failing services, and provides a **graceful user experience**.

---

# A **Spring Cloud Gateway** project that implements a **Circuit Breaker with fallback**, using **Resilience4j**.

#### Goal:

When a client hits `/book/**`, Gateway tries to route to `book-service`.
If `book-service` is down or slow, the **circuit breaker opens**, and a **fallback route** responds with a friendly message.

#### 1. **Dependencies (`pom.xml`)**

```xml
<dependencies>
    <!-- Spring Boot Starter -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter</artifactId>
    </dependency>

    <!-- Spring Cloud Gateway -->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-gateway</artifactId>
    </dependency>

    <!-- Eureka Discovery Client -->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>

    <!-- Resilience4j Circuit Breaker -->
    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-circuitbreaker-reactor-resilience4j</artifactId>
    </dependency>

    <!-- For actuator (optional but helpful for monitoring) -->
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-actuator</artifactId>
    </dependency>
</dependencies>

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>2021.0.9</version> <!-- Use compatible version -->
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

#### 2. **application.yml**

```yaml
server:
  port: 8080

spring:
  application:
    name: gateway-service

  cloud:
    gateway:
      routes:
        - id: book-service
          uri: lb://BOOK-SERVICE
          predicates:
            - Path=/book/**
          filters:
            - name: CircuitBreaker
              args:
                name: bookCircuit
                fallbackUri: forward:/fallback/book

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka
```

#### 3. **Main Class**

```java
@SpringBootApplication
@EnableDiscoveryClient
public class GatewayServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(GatewayServiceApplication.class, args);
    }
}
```

#### 4. **Fallback Controller**

```java
@RestController
public class FallbackController {

    @GetMapping("/fallback/book")
    public ResponseEntity<String> fallbackBook() {
        return ResponseEntity.ok("Book Service is temporarily unavailable. Please try again later.");
    }
}
```

#### Optional (Custom Circuit Breaker config in `application.yml`):

```yaml
resilience4j.circuitbreaker:
  instances:
    bookCircuit:
      registerHealthIndicator: true
      slidingWindowSize: 5
      permittedNumberOfCallsInHalfOpenState: 3
      failureRateThreshold: 50
      waitDurationInOpenState: 10s
      minimumNumberOfCalls: 5
```

####  Testing Flow:

1. Start Eureka
2. Start `book-service` (or leave it down for testing fallback)
3. Start `gateway-service`
4. Hit: `http://localhost:8080/book/something`
   - If `book-service` is down or slow, fallback response will trigger after threshold is reached.

#### `name: bookCircuit` — Where is it coming from?

This is the **logical name of the circuit breaker instance**. It’s **not random**, but **you can choose any name** that makes sense (like `bookCircuit`, `paymentCB`, `userCB`, etc.).

✅ This name **must match**:

1. The value you set in `filters.args.name: bookCircuit` in `application.yml`, and
2. The circuit breaker configuration section under `resilience4j.circuitbreaker.instances.bookCircuit` if you want to **customize its behavior**.

So in your `application.yml`:

```yaml
filters:
  - name: CircuitBreaker
    args:
      name: bookCircuit        <-- 🔗 This is the reference name
      fallbackUri: forward:/fallback/book
```

And then the **matching config**:

#### Optional Circuit Breaker Configuration in `application.yml`

Put this **outside** the `spring:` section, typically at the end of the file:

```yaml
resilience4j:
  circuitbreaker:
    instances:
      bookCircuit:   # ⬅️ Must match the name in filters
        registerHealthIndicator: true
        slidingWindowSize: 5                   # Number of recent calls to monitor
        permittedNumberOfCallsInHalfOpenState: 3
        failureRateThreshold: 50               # % of failures to open the circuit
        waitDurationInOpenState: 10s           # Wait before transitioning to half-open
        minimumNumberOfCalls: 5                # Minimum requests before evaluating
```

This controls:

* How quickly the circuit opens
* When it moves to half-open and closed states
* How many calls are allowed during trial phases

#### Summary:

| Config Section               | Purpose                                          |
| ---------------------------- | ------------------------------------------------ |
| `args.name: bookCircuit`     | Defines the circuit breaker name used by Gateway |
| `resilience4j...bookCircuit` | Customizes that circuit breaker's behavior       |









