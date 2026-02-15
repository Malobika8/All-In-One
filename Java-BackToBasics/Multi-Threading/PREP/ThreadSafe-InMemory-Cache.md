# Question

In a banking application, how would you design a thread-safe in-memory cache?

Think about:
- Read-heavy workload
- Occasional updates
- High concurrency
- Performance

The real concern is performance trade-off under write-heavy load.

### The Real Design Thinking

In a banking in-memory cache:

### Characteristics:

* Read-heavy
* Occasional updates
* High concurrency
* Consistency critical
* Low latency required

## Option 1: ReentrantReadWriteLock

Pros:

* Multiple readers allowed
* Writers exclusive
* Predictable behavior
* Easier to reason about
* Reentrant

Cons:

* All reads still acquire read lock
* Slightly more contention

Safe, stable, production-friendly.

## Option 2: StampedLock

Pros:

* Optimistic read = no blocking
* Very high throughput in read-heavy workloads

Cons:

* Not reentrant
* More complex
* If writes are frequent → optimistic reads fail often
* Then performance benefit disappears

So your reasoning was correct:
If writes are frequent, optimistic locking advantage reduces.

In real banking systems, we usually use something else.

## The Better Answer: ConcurrentHashMap

For a cache, instead of manually managing locks:

We typically use:

```
ConcurrentHashMap
```

Why?

* Lock striping / CAS-based mechanisms
* Highly optimized
* No global lock
* Reads are mostly non-blocking
* Writes are fine-grained

It scales better than RW locks in most cases.

### How would you design thread-safe in-memory cache?

> We would use ConcurrentHashMap as the underlying storage since it provides high concurrency with fine-grained locking. For read-heavy workloads, it allows non-blocking reads. If additional atomic operations are required, I would use computeIfAbsent or atomic methods provided by the map. Only if I need strict read-write control beyond map operations would I consider ReentrantReadWriteLock.

If:

* Cache entries expire
* Need eviction (LRU, LFU)
* Need size-based eviction

Then we use libraries like:

* Caffeine (high-performance cache)
* Guava Cache

In real financial systems, reinventing cache manually is avoided.

---

# Suppose: Two threads call: Why is this dangerous even with ConcurrentHashMap? And what is the correct way?

```
if (!map.containsKey(key)) {
    map.put(key, computeValue());
}
```

ConcurrentHashMap makes **individual operations thread-safe**,
but NOT **compound operations**.

Use:

```java
map.computeIfAbsent(key, k -> computeValue());
```

Why? - Because `computeIfAbsent` is atomic. Only one thread computes the value. Other threads wait and reuse result.

### Why This Works

Internally:

* It locks only the bucket (not whole map)
* Ensures atomic check + compute + insert

High concurrency.
Correct logic.
No duplicate computation.

### Why is containsKey + put dangerous in ConcurrentHashMap?

> Because although ConcurrentHashMap provides thread-safe individual operations, the combination of containsKey and put is not atomic. This can lead to a race condition where multiple threads compute and insert the same value. The correct approach is to use computeIfAbsent, which ensures atomic check-and-insert.

---

# Suppose `computeValue()`:

* Takes 5 seconds
* Makes a DB call
* Is expensive

What performance issue might happen with `computeIfAbsent()`? And how would you design around it?

Since computeIfAbsent ensures atomicity, it may block threads if computeValue is expensive. That is the real issue.

### What Actually Happens Internally

When you do:

```java
map.computeIfAbsent(key, k -> computeValue());
```

If `computeValue()` takes 5 seconds:

* The thread computing it holds the bucket lock.
* Other threads requesting same key:

  * Will block until computation finishes.

This can reduce throughput significantly. Especially in high-load systems.

## 🎯 Store Future Instead of Value

Instead of storing:

```
Map<K, V>
```

Store:

```
Map<K, CompletableFuture<V>>
```

### Pattern:

```java
ConcurrentHashMap<K, CompletableFuture<V>> map = new ConcurrentHashMap<>();

public V get(K key) {
    CompletableFuture<V> future = map.computeIfAbsent(key, k ->
        CompletableFuture.supplyAsync(() -> computeValue(k))
    );

    return future.join();
}
```

## Why This Is Better

1️⃣ Only one computation starts.
2️⃣ Other threads don't recompute.
3️⃣ No long blocking inside map lock.
4️⃣ Work is delegated to thread pool.

This is how high-scale caching systems are designed.

### Why This Matters in Banking Systems

Imagine:

* 1000 threads request same account data.
* DB call takes 3 seconds.

Without this pattern:

→ 1000 DB calls.

With naive computeIfAbsent:

→ Threads blocked holding internal map lock.

With CompletableFuture approach:

→ 1 DB call
→ 999 threads wait on same future
→ Better resource utilization

> For expensive computations, we would avoid performing long-running tasks inside computeIfAbsent. Instead, I would store a CompletableFuture as the value so that only one computation is triggered, and other threads can asynchronously wait for the result without blocking map internals.

