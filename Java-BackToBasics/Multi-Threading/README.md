## Process

A process is an independent program in execution.
It has its own memory space and system resources.
A process can contain one or more threads.

## Thread

A thread is the smallest unit of execution within a process.
Multiple threads inside a process share the same memory and resources but execute different tasks concurrently.

## Race conditions in Java can be prevented using:

1️⃣ synchronized keyword

- Can be applied on method or block
- Ensures only one thread executes the critical section at a time
- Uses intrinsic monitor lock

2️⃣ Explicit Locks (ReentrantLock)

From java.util.concurrent.locks
- More flexible than synchronized
- Supports:
  - tryLock()
  - fairness policy
  - interruptible locks
- Must manually release lock in finally block

3️⃣ Atomic Classes

From java.util.concurrent.atomic
- AtomicInteger
- AtomicLong
- AtomicReference

They use CAS (Compare-And-Swap) internally. Very efficient, no blocking.

4️⃣ Using Concurrent Collections

- Instead of: HashMap Use: ConcurrentHashMap
- Instead of: ArrayList Use: CopyOnWriteArrayList

5️⃣ Immutability

If objects are immutable:

- No shared mutable state
- No race condition
  Example: String, Wrapper classes

Race conditions can be avoided by ensuring proper synchronization, using lock mechanisms, atomic variables, concurrent collections, or by designing immutable objects.

## Deadlock

Two or more threads are permanently blocked because each is waiting for a resource held by another.

## Does `notifyAll()` wake all waiting threads?

It wakes **all threads waiting on that object's monitor**.

But important nuance:
* They all move from WAITING → BLOCKED
* They compete to re-acquire the monitor
* Only one acquires it at a time

They do NOT all run simultaneously.

## Do `wait()`, `notify()`, `notifyAll()` come from `Object`?

Yes. They belong to `java.lang.Object`.

## Why can’t they be used with explicit (extrinsic) locks like `ReentrantLock`?

Because:

* `wait/notify` work with the **intrinsic monitor lock**
* `synchronized` uses the object’s monitor

But `ReentrantLock` does NOT use object monitors. It uses a completely different locking mechanism built on **AbstractQueuedSynchronizer (AQS)**.

So instead of:

```
wait() / notify()
```

With `ReentrantLock`, we use:

```
Condition.await()
Condition.signal()
Condition.signalAll()
```

Example:

```java
ReentrantLock lock = new ReentrantLock();
Condition condition = lock.newCondition();

lock.lock();
try {
    condition.await();
} finally {
    lock.unlock();
}
```

So:

Intrinsic lock → wait/notify
Explicit lock → await/signal


