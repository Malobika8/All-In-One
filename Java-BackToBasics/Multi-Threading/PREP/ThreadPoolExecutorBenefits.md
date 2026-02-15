# Why is `Executors.newFixedThreadPool()` discouraged in production?

Because it uses:

```java
new LinkedBlockingQueue<Runnable>()
```

Without a capacity limit.

That means:

👉 Unbounded queue.

If tasks come faster than threads can process:

* Queue grows infinitely
* Memory increases
* Eventually → OutOfMemoryError

Very dangerous in production systems.

# Production-Grade Approach

Instead of:

```java
Executors.newFixedThreadPool(10);
```

We prefer:

```java
new ThreadPoolExecutor(
    corePoolSize,
    maximumPoolSize,
    keepAliveTime,
    TimeUnit.SECONDS,
    new ArrayBlockingQueue<>(100),
    new ThreadPoolExecutor.AbortPolicy()
);
```

Now:

* Bounded queue
* Rejection policy defined
* Better back-pressure control

> Because the Executors utility methods create thread pools with unbounded queues, which can lead to uncontrolled memory growth under heavy load. In production systems, it is safer to use ThreadPoolExecutor directly with a bounded queue and a defined rejection policy.

# Suppose we configure:

* corePoolSize = 2
* maximumPoolSize = 4
* queue capacity = 2

If 7 tasks are submitted quickly, what happens step by step? Explain task allocation flow carefully.

### First — What Is The Queue For?

The queue exists because:

👉 Threads are expensive to create.
👉 We don’t immediately create new threads for every task.

The queue is a **buffer between task submission and thread execution**.

## How ThreadPoolExecutor Actually Works (Important)

When a new task is submitted:

### Step 1️⃣

If running threads < corePoolSize
→ Create new thread and run task immediately.

### Step 2️⃣

If running threads ≥ corePoolSize
→ Task goes into queue.

### Step 3️⃣

If queue is full AND running threads < maximumPoolSize
→ Create new thread (beyond core pool).

### Step 4️⃣

If queue is full AND running threads = maximumPoolSize
→ Task is rejected (RejectionPolicy).

This order is VERY important.

## Now Let’s Apply Your Scenario

Config:

* corePoolSize = 2
* maximumPoolSize = 4
* queue capacity = 2

Submit 7 tasks quickly.

### 🟢 Task 1

Threads = 0 < 2
→ Create Thread 1
Running threads = 1

### 🟢 Task 2

Threads = 1 < 2
→ Create Thread 2
Running threads = 2

Now core pool is full.

### 🟢 Task 3

Threads = 2
→ Goes into queue (queue size = 1)

### 🟢 Task 4

Threads = 2
→ Goes into queue (queue size = 2, full)

### 🟢 Task 5

Queue full
Threads (2) < max (4)
→ Create Thread 3
Running threads = 3

### 🟢 Task 6

Queue still full
Threads (3) < max (4)
→ Create Thread 4
Running threads = 4

### 🔴 Task 7

Queue full
Threads = max (4)
→ Task rejected

Rejection policy decides what happens.

## Final State

* 4 threads running
* 2 tasks waiting in queue
* 1 task rejected

The queue is NOT useless.

It:

* Absorbs bursts
* Prevents too many thread creations
* Helps manage load

---

## Why Not Just maxPoolSize = 10 and no queue?

Because:

Without queue:

* Every burst creates threads
* Context switching increases
* Memory pressure increases

With queue:

* Short spikes handled smoothly
* Threads reused efficiently

In high-load banking systems:

Choosing:

* corePoolSize
* maxPoolSize
* queue capacity

Is critical for stability.

Once the core threads are busy and the queue is full, the pool creates additional threads up to maxPoolSize. If the maximum limit is reached, the RejectedExecutionHandler decides what to do — either throw exception, run in caller thread, or discard tasks. In production systems, we usually configure a bounded queue with an explicit rejection policy to avoid memory issues.
