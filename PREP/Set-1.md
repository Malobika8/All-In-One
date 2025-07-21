# What is a microservice? How is it different from a monolith?

### Sol:

A **monolithic architecture** combines all functionalities of an application into a single deployable unit. All modules — like authentication, billing, inventory, etc. — are tightly coupled and share the same codebase, memory space, and deployment cycle. Even a small change requires **redeploying the entire application** and full regression testing.

In contrast, **microservices architecture** breaks the system into **independent, small services**. Each service is:

* Focused on a single business capability,
* Developed, deployed, and scaled independently,
* Communicates with others via **lightweight protocols** like REST or messaging.

This **decouples dependencies**, increases scalability and maintainability, and allows teams to work in parallel.
However, it brings complexities like **distributed transactions**, **network latency**, **service discovery**, and **centralized logging and monitoring**.

#### A real-world analogy for microservices"

> A monolith is like a single restaurant kitchen making all cuisines — slow, complex.
> Microservices are like a food court — each vendor handles one cuisine independently.

---

# What are the main advantages and disadvantages of microservices?

### Sol:

**Advantages of Microservices:**

1. **Loose Coupling & High Cohesion**: Each service handles one specific functionality, making it easier to develop, test, and maintain.
2. **Independent Deployment**: Changes in one service don’t require redeploying the entire system.
3. **Scalability**: You can scale only the services that need more resources, which is **cost-efficient**.
4. **Technology Flexibility**: Different services can use different tech stacks (polyglot architecture).
5. **Faster Development**: Teams can work on different services in parallel, improving productivity.
6. **Fault Isolation**: A failure in one service is less likely to bring down the whole system.

**Disadvantages of Microservices:**

1. **Operational Complexity**: Managing many services, their deployment, configuration, and monitoring can be challenging.
2. **Service Discovery**: Services need to find and talk to each other dynamically (usually solved with tools like Eureka).
3. **Network Latency**: More inter-service communication over the network, which introduces delays and the risk of failure.
4. **Data Management**: Handling consistency, distributed transactions, and data across services becomes harder.
5. **Testing Complexity**: End-to-end testing is more complex due to the distributed nature.

---

# In a microservices architecture, how do services communicate with each other? List and explain different types of communication methods.

### Sol:

In microservices, services communicate with each other mainly in **two ways**:

#### 1. **Synchronous Communication (Request-Response)**

👉 One service sends a request and waits for the response.
Common protocols:

* **HTTP (REST)** – Most common.
* **gRPC** – A faster binary protocol for performance-heavy use cases.

**Popular clients in Spring:**

* `RestTemplate` – Synchronous, traditional (now discouraged for new dev).
* `WebClient` – Non-blocking, reactive alternative to RestTemplate.
* `FeignClient` – Declarative HTTP client; simplifies REST calls with interfaces.

✅ Example use case: `Order Service` calls `Payment Service` to process a payment in real-time.

#### 2. **Asynchronous Communication (Event-Driven)**

👉 One service sends a message or event without waiting for a response.

**Messaging tools:**

* **RabbitMQ**
* **Apache Kafka**
* **ActiveMQ**

✅ Example use case: `Order Service` publishes an event like `OrderPlaced`, and `Email Service` listens to send confirmation emails.

**Why asynchronous is important:**

It **decouples services** further, improves **resilience**, and allows **event sourcing** or **event-driven architecture**.

---

# What is a FeignClient in Spring Cloud? How does it work internally? Can you give a usage example?

### Sol:

**FeignClient** is a declarative web service client provided by **Spring Cloud OpenFeign**.
It simplifies calling REST APIs between microservices by **writing just an interface** — no need to write `RestTemplate` logic manually.

#### Key Features:

* Declarative: Just define the method signatures in an interface.
* Spring-integrated: Works with `@Component`, `@Autowired`, etc.
* Eureka-integrated: Uses **service names** instead of hardcoded URLs.
* Supports fallback via **Resilience4j** or **Hystrix** (if enabled).

#### Example:

Suppose we have a **Student Service** and a **Book Service**. Student Service wants to fetch books for a student by calling Book Service.

```java
@FeignClient(name = "book-service")  // 'book-service' must be registered in Eureka
public interface BookClient {

    @GetMapping("/books/student/{id}")
    Book getBooksByStudentId(@PathVariable("id") int studentId);
}
```

And in your StudentService class:

```java
@Service
public class StudentService {

    @Autowired
    private BookClient bookClient;

    public Book fetchBook(int studentId) {
        return bookClient.getBooksByStudentId(studentId);
    }
}
```

#### How it works internally:

* Spring Cloud creates a **proxy object** at runtime using JDK Dynamic Proxy.
* It uses **Ribbon (or Spring Cloud LoadBalancer)** to resolve the actual instance of the service from **Eureka** (if discovery is enabled).
* Then it makes an HTTP request via an underlying HTTP client (like Apache HTTP Client).

#### Optional Enhancements:

* Add fallback with `@FeignClient(name="book-service", fallback = BookClientFallback.class)`
* Use `@EnableFeignClients` in your Spring Boot application class.

---

# What is service discovery in microservices? How does **Eureka** work? How do services register and discover each other?

### Sol:

**Service Discovery** in microservices helps services dynamically discover and communicate with each other without hardcoding hostnames or ports.

This becomes crucial when:

* Services scale **up/down dynamically**, and
* Instance IPs and ports **keep changing** (especially in cloud or containerized environments like Docker/Kubernetes).

#### What is Eureka?

**Eureka** is a service registry provided by **Netflix**, supported in **Spring Cloud Netflix**.

#### How Eureka Works:

1. **Service Registration:**

   * When a service (like `StudentService`) starts, it **registers itself with Eureka** using the `@EnableEurekaClient` annotation.
   * It sends metadata like `host`, `port`, and service name.
   * Eureka stores this info in its **registry**.

2. **Service Discovery:**

   * Services like `BookService` use Eureka to find the **current available instances** of another service.
   * This avoids hardcoding IPs or URLs.

3. **Self-Preservation and Heartbeats:**

   * Services send **heartbeat pings** to Eureka at regular intervals.
   * If a service fails to send heartbeats, it is eventually **deregistered**.
   * Eureka may temporarily retain stale info in **self-preservation mode** to avoid false negatives during network glitches.

4. **Load Balancing:**

   * With Spring Cloud LoadBalancer (or previously Ribbon), Eureka returns **multiple instances** of a service.
   * Requests are load-balanced across those instances — no manual setup needed.

#### Analogy:

Eureka is like a **dynamic phone book**, where services look up the "name" (`student-service`) and get all the live phone numbers (host\:port combos) for it.

#### Code-Level Annotations:

* Add to `application.yml` or `application.properties`:

```yaml
eureka.client.service-url.defaultZone=http://localhost:8761/eureka
```

* Register with Eureka:

```java
@SpringBootApplication
@EnableEurekaClient  // or @EnableDiscoveryClient
public class StudentServiceApp { }
```

* Use `@LoadBalanced` if using `RestTemplate`:

```java
@Bean
@LoadBalanced
public RestTemplate restTemplate() {
    return new RestTemplate();
}
```

---










