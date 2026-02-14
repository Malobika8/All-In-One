# 🔥 What is AtomicInteger?

`AtomicInteger` is a class from:

```
java.util.concurrent.atomic
```

It allows you to perform operations like increment, decrement, compare-and-set **atomically** — meaning:

> The operation happens as a single indivisible step.

---

## ⚠️ Why normal increment is dangerous?

```java
count++;
```

This is NOT atomic.

It internally does:

1. Read value
2. Increment
3. Write back

If two threads do this at same time → race condition.

---

## ✅ AtomicInteger Example

```java
import java.util.concurrent.atomic.AtomicInteger;

AtomicInteger count = new AtomicInteger(0);

count.incrementAndGet();
```

This operation is:

✔ Thread-safe
✔ Non-blocking
✔ No synchronized
✔ No explicit locking

---

## 🧠 How Does It Work?

It uses something called:

> CAS (Compare And Swap)

Internally it says:

* If current value == expected value
* Then update it
* Else retry

This happens at CPU instruction level.

No locking.
Very fast.
Used heavily in high-performance systems (banks love this).

---

## 🔥 Why is this powerful?

Instead of:

```java
synchronized void increment() {
    count++;
}
```

You can write:

```java
count.incrementAndGet();
```

And it is thread-safe without blocking.

---

## ⚡ When to Use AtomicInteger?

* Counters
* Statistics
* Simple shared numeric state
* High concurrency systems

---

## 🚨 Important Limitation

AtomicInteger works well for **single variable operations**.

If you need:

```
if(count > 5) then update another variable
```

Then atomic alone is not enough.
You may still need synchronization.

---
