# 1. What is Project Reactor?

👉 **Project Reactor** is a **Reactive Programming library for the JVM**.
It implements the **Reactive Streams specification** and provides powerful APIs (`Flux`, `Mono`) to handle **asynchronous, non-blocking, event-driven streams** of data.

Think of it as:

* **Java Stream API** but for **async + infinite data**
* **RxJava’s cousin** (similar concepts, different ecosystem)
* The **foundation for Spring WebFlux** (reactive web framework in Spring Boot)

---

## 2. Why Do We Need Reactor?

Traditional programming (blocking):

* Each request → takes up a thread.
* Threads wait (DB calls, API calls, file IO).
* If you have 1000 requests, you need 1000 threads.
* **Scaling is limited.**

Reactor (non-blocking):

* Uses **event loop model** (like Node.js).
* A few threads can handle **thousands of requests**.
* Instead of blocking, Reactor **reacts** when data is available.

👉 Perfect for **microservices**, **APIs**, **real-time systems**.

---

## 3. Core Concepts in Project Reactor

### a) **Publisher types**:

* **Mono<T>** → A publisher that emits **0 or 1** item.
  (Think: a single result → like Optional or Future).
* **Flux<T>** → A publisher that emits **0…N** items.
  (Think: a stream/list of values, possibly infinite).

### b) **Operators** (like in Java Stream):

* Transform: `map`, `flatMap`, `filter`
* Combine: `merge`, `zip`, `concat`
* Handle errors: `onErrorReturn`, `retry`
* Control flow: `take`, `skip`, `delayElements`

### c) **Subscriber**:

* Reactor provides default subscribers (via `.subscribe()`),
  but you can create your own for custom backpressure control.

---

## 4. Example (Mono & Flux)

### Mono (single value):

```java
import reactor.core.publisher.Mono;

public class MonoExample {
    public static void main(String[] args) {
        Mono.just("Hello Reactor")
            .map(String::toUpperCase)
            .subscribe(System.out::println); // Subscriber consumes
    }
}
```

Output:

```
HELLO REACTOR
```

---

### Flux (multiple values):

```java
import reactor.core.publisher.Flux;

public class FluxExample {
    public static void main(String[] args) {
        Flux.range(1, 5)
            .map(n -> n * n)
            .subscribe(System.out::println);
    }
}
```

Output:

```
1
4
9
16
25
```

---

## 5. How It Differs from Java Streams

| Feature      | Java Streams             | Project Reactor (Flux/Mono)               |
| ------------ | ------------------------ | ----------------------------------------- |
| Data type    | `Stream<T>`              | `Flux<T>` / `Mono<T>`                     |
| Sync/Async   | Synchronous (blocking)   | Asynchronous (non-blocking)               |
| Size         | Finite only              | Finite or infinite                        |
| Backpressure | ❌ Not supported          | ✅ Supported                               |
| Laziness     | Yes                      | Yes (nothing happens until `subscribe()`) |
| Use case     | In-memory collection ops | Reactive APIs, WebFlux, messaging, IO     |

---

## 6. Where Is Reactor Used?

* **Spring WebFlux** → non-blocking REST APIs (instead of Spring MVC).
* **R2DBC** → Reactive Database Connectivity (non-blocking DB calls).
* **Messaging** → Kafka, RabbitMQ, WebSockets.
* **Real-time pipelines** → Data streams, event-driven apps.

---

✅ So in short:

* **Project Reactor = a Reactive Programming library for Java.**
* Provides **Flux** (0…N items) and **Mono** (0/1 item).
* Asynchronous, non-blocking, supports backpressure.
* Forms the foundation of **Spring WebFlux** and reactive microservices.

---

