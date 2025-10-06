# Backpressure — a friendly deep dive (for beginners)

**Backpressure** is the mechanism that lets a *slow consumer* tell a *fast producer* “please slow down — I can only handle N items right now.” Without it, fast producers can overwhelm consumers (memory blowups, high latency, dropped data).

We'll try to understand with analogies, the Reactive Streams contract, what actually happens under the hood, code examples (Project Reactor / Reactive Streams), common strategies, and practical tips.

---

# 1) Intuition & analogies

* Think of a faucet (producer) filling a sink (consumer). If the faucet runs too fast, the sink overflows. Backpressure = the sink telling the faucet to reduce flow.
* Or think of a highway: cars (events) flow from on-ramps (producers) into a busy city (consumer). If the city can only process 10 cars/sec, you need traffic lights (backpressure) or else gridlock happens.

Key idea: *demand signalling* — the consumer signals how many items it can accept; the producer respects that demand.

---

# 2) The Reactive Streams contract (the pieces)

Reactive Streams defines four roles/interfaces:

* **Publisher<T>** — the data source (can produce 0..N items).
* **Subscriber<T>** — the consumer that receives items.
* **Subscription** — the link between Publisher and Subscriber. Subscriber receives a `Subscription` in `onSubscribe(…)` and uses it to request items or cancel.
* **Processor** — both a Subscriber and Publisher (transformer).

Important method: `subscription.request(long n)` — the **demand signal**. The subscriber asks for `n` items. The publisher must not send more than `n` `onNext` calls until more is requested. (`request(Long.MAX_VALUE)` means “unbounded”, i.e., no backpressure.)

Note: calling `request(0)` or a non-positive value is illegal per the spec — it should be avoided.

---

# 3) Push vs Pull and where backpressure fits

* **Push model**: producer pushes items to the consumer as soon as they are available (like traditional callbacks). If producer is faster than consumer, things pile up.
* **Pull model**: consumer pulls items when it’s ready (requests). Reactive Streams uses a *push-after-pull* hybrid: the producer pushes items **only up to** what the consumer requested. So the consumer *controls* rate.

---

# 4) What happens if there is no backpressure?

* Unbounded buffering: memory grows → OOM.
* Increased latency and GC pressure.
* Data loss (if a system chooses to drop messages to cope).
* Unexpected behaviour in downstream systems (e.g., DB overload).

So backpressure is about *stability* and *predictability* of your reactive pipeline.

---

# 5) How backpressure looks in practice (sequence)

Simple sequence:

1. `publisher.subscribe(subscriber)`
2. `subscriber.onSubscribe(subscription)`
3. `subscriber` calls `subscription.request(5)` → demand = 5
4. `publisher` sends up to 5 `onNext(item)` calls
5. When subscriber needs more, it calls `request(more)` again
6. Or the subscriber calls `subscription.cancel()` to stop

This keeps producer emissions bounded by downstream demand.

---

# 6) A tiny Java example (custom Subscriber requesting 1 item at a time)

```java
import org.reactivestreams.*;

public class PrintSubscriber implements Subscriber<Integer> {
    private Subscription subscription;

    @Override
    public void onSubscribe(Subscription s) {
        this.subscription = s;
        // request first item
        s.request(1);
    }

    @Override
    public void onNext(Integer item) {
        System.out.println("Processing " + item);
        // simulate slow processing
        try { Thread.sleep(200); } catch (InterruptedException e) { Thread.currentThread().interrupt(); }
        // request next item only when ready
        subscription.request(1);
    }

    @Override
    public void onError(Throwable t) { t.printStackTrace(); }

    @Override
    public void onComplete() { System.out.println("Done"); }
}
```

Usage with Reactor:

```java
Flux.range(1, 1000).subscribe(new PrintSubscriber());
```

Here the `PrintSubscriber` processes one element at a time — the `Flux` will not blast all 1000 items into memory.

### Extending Base Subscriber

<img width="814" height="424" alt="Screenshot 2025-09-19 at 8 05 45 PM" src="https://github.com/user-attachments/assets/287955e4-af8e-4f9e-8f6f-bce1bed9dfd7" />
<img width="818" height="475" alt="Screenshot 2025-09-19 at 8 06 53 PM" src="https://github.com/user-attachments/assets/551bcb2d-b855-45d4-9ee2-25c793afa42c" />
<img width="1102" height="270" alt="Screenshot 2025-09-19 at 8 21 54 PM" src="https://github.com/user-attachments/assets/accace53-0857-4c1d-ab71-002209c9e3e6" />

