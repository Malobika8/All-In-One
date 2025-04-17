**Java Executor Framework**

- What it is
- The types of `ExecutorService`
- Related interfaces and classes
- Real-life use cases
- Comparison tables
- Gotchas and best practices

---

## 🧠 1. What is the Executor Framework?

Java's **Executor Framework** is a powerful API introduced in Java 5 to manage thread execution more easily and efficiently.

Instead of manually creating threads, you:
> ✅ Define tasks  
> ✅ Submit them to an **Executor**  
> ✅ Let the framework manage the threads  

All of this lives under the `java.util.concurrent` package.

---

## 🧩 2. Core Interfaces in the Executor Framework

| Interface           | Purpose |
|---------------------|---------|
| `Executor`          | Basic interface with `execute(Runnable)` |
| `ExecutorService`   | Advanced interface for managing tasks and lifecycle |
| `ScheduledExecutorService` | Extends `ExecutorService` for scheduling delayed or periodic tasks |

---

## 🏗️ 3. Main Implementations via `Executors` Factory

Java provides **factory methods** in the `Executors` class to create common types of executors.

### 1. `newFixedThreadPool(int n)`
- Creates a thread pool with a **fixed number** of threads.
- If all threads are busy, new tasks wait in a queue.

🔧 Use Case: Handling a constant load of background tasks.

```java
ExecutorService pool = Executors.newFixedThreadPool(4);
```

---

### 2. `newSingleThreadExecutor()`
- Uses **only one thread** to execute tasks.
- Tasks are executed **sequentially** in the order they are submitted.

🔧 Use Case: Logging, serialization, or tasks that must never run in parallel.

```java
ExecutorService pool = Executors.newSingleThreadExecutor();
```

---

### 3. `newCachedThreadPool()`
- Creates **new threads as needed**, but **reuses** idle threads.
- If threads are idle for 60 seconds, they are removed.

🔧 Use Case: Short-lived asynchronous tasks; bursty traffic.

```java
ExecutorService pool = Executors.newCachedThreadPool();
```

---

### 4. `newScheduledThreadPool(int corePoolSize)`
- Supports **delayed** or **periodic** task execution (like cron jobs).

🔧 Use Case: Repeating tasks, polling, scheduled backups.

```java
ScheduledExecutorService pool = Executors.newScheduledThreadPool(2);
```

---

### 5. `newWorkStealingPool()`
- Uses multiple queues and threads to **steal work** from others.
- Uses **ForkJoinPool** under the hood.

🔧 Use Case: When you have **many short-lived subtasks** (e.g., parallel processing).

```java
ExecutorService pool = Executors.newWorkStealingPool();
```

---

## 🧱 4. Related Classes

| Class / Interface        | Description |
|--------------------------|-------------|
| `Future<T>`              | Represents the result of an async computation |
| `Callable<T>`            | Like `Runnable`, but returns a result |
| `CompletionService<T>`   | Combines Executor and BlockingQueue to get results as they complete |
| `ForkJoinPool`           | A type of pool optimized for recursive parallelism |
| `ThreadPoolExecutor`     | The actual class behind `Executors.newFixedThreadPool`, etc. |
| `ScheduledThreadPoolExecutor` | Behind `ScheduledExecutorService` |

---

## 🔬 5. Bonus: Internals of `ThreadPoolExecutor`

`Executors.newFixedThreadPool()` and friends are just **wrappers**. They return a `ThreadPoolExecutor`.

Key constructor parameters:
```java
ThreadPoolExecutor(
    int corePoolSize,
    int maximumPoolSize,
    long keepAliveTime,
    TimeUnit unit,
    BlockingQueue<Runnable> workQueue
)
```

🧠 You can customize:
- Thread limits
- Queue behavior
- Rejection policies (what to do when the queue is full)

---

## 🛠️ 6. ScheduledExecutorService Example

```java
ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(1);

// Runs once after 2 seconds
scheduler.schedule(() -> System.out.println("Delayed Task"), 2, TimeUnit.SECONDS);

// Runs every 1 second after initial delay of 3 seconds
scheduler.scheduleAtFixedRate(() -> System.out.println("Repeating Task"), 3, 1, TimeUnit.SECONDS);
```

---

## ⚖️ Comparison Table

| Type                   | Threads | Queue | Grows? | Used For |
|------------------------|---------|-------|--------|----------|
| FixedThreadPool        | Fixed   | Yes   | No     | Regular background work |
| SingleThreadExecutor   | 1       | Yes   | No     | Sequential tasks |
| CachedThreadPool       | Dynamic | No    | Yes    | Bursty, short tasks |
| ScheduledThreadPool    | Fixed   | Yes   | No     | Timed tasks |
| WorkStealingPool       | Dynamic | Local | Yes    | Parallelism / ForkJoin |

---

## 🧠 Best Practices & Gotchas

| Tip | Why |
|-----|-----|
| Always `shutdown()` the executor | Or your app may hang due to non-daemon threads |
| Prefer `submit()` over `execute()` if return value is needed | Returns a `Future` |
| Don’t use Executors in Android (use Kotlin Coroutines or other libs) | Executor threads might not behave well with the lifecycle |
| Customize `ThreadPoolExecutor` for advanced tuning | Like backpressure, priorities |
| Avoid unbounded queues blindly | Can lead to **OutOfMemoryError** |

---
