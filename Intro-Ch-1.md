# 1. What is Reactive Programming?

At its core:

👉 **Reactive Programming** is about handling **asynchronous data streams** (events, messages, API responses, user actions, etc.) in a **non-blocking**, **event-driven** way.

Instead of asking:

> "Give me the data now, and I’ll wait until you’re done."

Reactive says:

> "Whenever new data is available, notify me, and I’ll react to it."

That’s why it’s called **reactive**.

---

## 2. Why Do We Need Reactive Programming?

Traditional Java (imperative style):

* A thread makes a request → blocks (waits) until data is ready.
* Threads are limited resources → scaling becomes hard (especially with 1000s of requests).

Reactive Programming:

* Threads don’t block.
* Work continues in background.
* When the result is ready, it "pushes" the data to whoever subscribed.
* This allows **high scalability with fewer threads**.

---

## 3. Reactive Streams in Java

Reactive Streams is a **standard specification** (introduced in Java 9) for **asynchronous stream processing with non-blocking backpressure**.

Key interfaces (from `java.util.concurrent.Flow` in Java 9):

1. **Publisher<T>**

   * Produces data (events/items).
   * Think of it like a "source".

2. **Subscriber<T>**

   * Consumes data.
   * Think of it like a "sink".

3. **Subscription**

   * A contract between Publisher and Subscriber.
   * Manages demand (how much data subscriber can handle).

4. **Processor\<T,R>**

   * Both Publisher & Subscriber.
   * Used for data transformations (like a pipeline).

---

## 4. How Reactive Streams Work (Step-by-Step)

Imagine a pipeline:

```
Publisher -> Subscription -> Subscriber
```

1. **Subscriber subscribes** to Publisher.
2. **Publisher creates Subscription** and sends it to Subscriber.
3. **Subscriber requests N items** via Subscription (backpressure mechanism).
4. **Publisher sends data items** (up to N).
5. **Subscriber consumes items** and can request more.
6. If an error happens, Publisher notifies the Subscriber.
7. When Publisher has no more data, it calls `onComplete()`.

---

## 5. Backpressure (VERY IMPORTANT)

* Backpressure = **Subscriber controls the flow**.
* Prevents Subscriber from being overwhelmed.
* Example:

  * Subscriber asks for 5 items.
  * Publisher won’t push more than 5 until Subscriber asks again.

This is what makes **Reactive Streams different** from a simple async callback.

---

## 6. Example in Java (Using Flow API)

Here’s a minimal example with Java 9’s `Flow`:

```java
import java.util.concurrent.Flow;
import java.util.concurrent.SubmissionPublisher;

public class ReactiveExample {
    public static void main(String[] args) throws InterruptedException {
        // Publisher
        SubmissionPublisher<String> publisher = new SubmissionPublisher<>();

        // Subscriber
        Flow.Subscriber<String> subscriber = new Flow.Subscriber<>() {
            private Flow.Subscription subscription;

            @Override
            public void onSubscribe(Flow.Subscription subscription) {
                this.subscription = subscription;
                subscription.request(1); // request first item
            }

            @Override
            public void onNext(String item) {
                System.out.println("Received: " + item);
                subscription.request(1); // request next item
            }

            @Override
            public void onError(Throwable throwable) {
                System.err.println("Error: " + throwable);
            }

            @Override
            public void onComplete() {
                System.out.println("Done");
            }
        };

        // Subscriber subscribes
        publisher.subscribe(subscriber);

        // Publish some items
        publisher.submit("Hello");
        publisher.submit("Reactive");
        publisher.submit("World");

        publisher.close();

        // Wait for subscriber to consume
        Thread.sleep(1000);
    }
}
```

### Output:

```
Received: Hello
Received: Reactive
Received: World
Done
```

---

## 7. Real-World Reactive Libraries in Java

* **Project Reactor (Spring WebFlux uses this)** → `Mono`, `Flux`
* **RxJava** → `Observable`, `Flowable`
* Both implement **Reactive Streams** under the hood.

Example with Reactor:

```java
Flux.just("A", "B", "C")
    .map(String::toLowerCase)
    .subscribe(System.out::println);
```

Output:

```
a
b
c
```

---

✅ So in short:

* Reactive Programming = working with async data streams.
* Reactive Streams = Java standard (`Publisher`, `Subscriber`, `Subscription`, `Processor`).
* Backpressure = Subscriber controls flow.
* Libraries like **Reactor** and **RxJava** implement this in real applications.

