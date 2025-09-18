# 1. The `Subscriber<T>` interface

In Reactive Streams (`org.reactivestreams.Subscriber` or `java.util.concurrent.Flow.Subscriber`), a Subscriber must implement **4 methods**:

```java
public interface Subscriber<T> {
    void onSubscribe(Subscription subscription); // called once, when subscribing
    void onNext(T item);                         // called for each item
    void onError(Throwable throwable);           // called if error occurs
    void onComplete();                           // called when publisher is done
}
```

* **onSubscribe**: Receives a `Subscription`. You must use it to request items (`request(n)`).
* **onNext**: Handles each item received.
* **onError**: Handles errors.
* **onComplete**: Called when Publisher finishes.

<img width="1021" height="103" alt="Screenshot 2025-09-18 at 6 54 00 PM" src="https://github.com/user-attachments/assets/1c4621bf-8c89-4200-9563-3dd56b33e617" />
<img width="718" height="257" alt="Screenshot 2025-09-18 at 6 54 06 PM" src="https://github.com/user-attachments/assets/f8e53328-6de6-452d-b9c6-cd8cf94a0830" />
<img width="1127" height="641" alt="Screenshot 2025-09-18 at 7 07 14 PM" src="https://github.com/user-attachments/assets/7e01faee-d4f1-4fc7-8147-ea9944d2758f" />

---

## 2. Creating Our Own Subscriber

<img width="764" height="358" alt="Screenshot 2025-09-18 at 7 11 13 PM" src="https://github.com/user-attachments/assets/0284a915-fd50-4921-a8f2-3661818a1823" />
<img width="797" height="303" alt="Screenshot 2025-09-18 at 7 11 22 PM" src="https://github.com/user-attachments/assets/356779a7-7d20-4cb1-a4ea-eb974ac3c961" />
<img width="790" height="523" alt="Screenshot 2025-09-18 at 7 12 02 PM" src="https://github.com/user-attachments/assets/28340c44-6ae2-4848-b119-2ffccd5d6ac3" />
<img width="714" height="581" alt="Screenshot 2025-09-18 at 7 13 00 PM" src="https://github.com/user-attachments/assets/a1bf0078-05c4-44fd-86f9-46916f0758af" />

### Here’s a simple custom Subscriber example:

```java
import org.reactivestreams.Subscriber;
import org.reactivestreams.Subscription;

public class MySubscriber implements Subscriber<Integer> {

    private Subscription subscription;
    private int count = 0;
    private final int requestSize = 2; // how many items to request at a time

    @Override
    public void onSubscribe(Subscription subscription) {
        this.subscription = subscription;
        System.out.println("Subscribed!");
        subscription.request(requestSize); // request first batch
    }

    @Override
    public void onNext(Integer item) {
        System.out.println("Received: " + item);
        count++;
        if (count % requestSize == 0) {
            System.out.println("Requesting next " + requestSize + " items...");
            subscription.request(requestSize); // request more when ready
        }
    }

    @Override
    public void onError(Throwable throwable) {
        System.err.println("Error occurred: " + throwable.getMessage());
    }

    @Override
    public void onComplete() {
        System.out.println("All items received. Completed!");
    }
}
```

---

## 3. Using This Subscriber with a Flux

```java
import reactor.core.publisher.Flux;

public class CustomSubscriberDemo {
    public static void main(String[] args) {
        Flux<Integer> flux = Flux.range(1, 10); // emits 1 to 10

        flux.subscribe(new MySubscriber());
    }
}
```

---

## 4. Output (Example)

```
Subscribed!
Received: 1
Received: 2
Requesting next 2 items...
Received: 3
Received: 4
Requesting next 2 items...
Received: 5
Received: 6
Requesting next 2 items...
Received: 7
Received: 8
Requesting next 2 items...
Received: 9
Received: 10
Requesting next 2 items...
All items received. Completed!
```

---

## 5. Why This Is Useful?

* By writing your own `Subscriber`, you **control the flow of data** (backpressure).
* You decide **how many items to request** at a time.
* Prevents memory overflow if the Publisher is very fast.

---

✅ So in short:

* You implement `Subscriber<T>`.
* Use `onSubscribe` to **request items**.
* Handle each item in `onNext`.
* React to completion or errors in `onComplete` / `onError`.

