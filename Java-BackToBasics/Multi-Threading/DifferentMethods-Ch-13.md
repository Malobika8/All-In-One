Let’s go **method by method** through the key interfaces of Java’s Executor framework — especially `ExecutorService` and its extension `ScheduledExecutorService`.

- What each method does  
- When and why to use it  
- Key return values or exceptions  
- Simple examples (where helpful)

---

## 🔧 1. `Executor` interface – Basic level

```java
void execute(Runnable command)
```

- **Description**: Submits a task for execution.
- **Returns**: `void` (you can't track the task's progress or result)
- **Use case**: Fire-and-forget background task.

```java
Executor executor = Executors.newSingleThreadExecutor();
executor.execute(() -> System.out.println("Running..."));
```

---

## 🚀 2. `ExecutorService` – Most common interface

```java
Future<?> submit(Runnable task)
<T> Future<T> submit(Callable<T> task)
<T> Future<T> submit(Runnable task, T result)
```

### ✅ `submit(...)`

- **Use**: Run a task and get a `Future` to retrieve result or manage it.
- `Runnable`: Returns a `Future<?>`
- `Callable`: Returns `Future<T>` with result
- `Runnable with result`: Returns a `Future<T>` with a predefined result

```java
Future<Integer> future = executor.submit(() -> 10 + 20); // Callable
System.out.println(future.get()); // 30
```

---

### ✅ `invokeAll(Collection<Callable<T>> tasks)`

- **Use**: Submits **multiple tasks** at once, waits for **all** to complete.
- **Returns**: List of `Future<T>` in the same order as input.
- **Blocking**: YES

```java
List<Callable<Integer>> tasks = List.of(
    () -> 1, () -> 2, () -> 3
);
List<Future<Integer>> results = executor.invokeAll(tasks);
```

---

### ✅ `invokeAny(Collection<Callable<T>> tasks)`

- **Use**: Submits multiple tasks, returns result of **first successfully completed**.
- **Returns**: `T` (not a `Future`)
- **Blocking**: YES
- **Cancels remaining tasks**

```java
int result = executor.invokeAny(List.of(
    () -> 1, () -> 2, () -> 3
));
System.out.println(result); // First one that completes
```

---

### ✅ `shutdown()`

- **Use**: Initiates an **orderly shutdown** – no new tasks accepted, but already submitted ones are executed.
- **Note**: Doesn’t block; use `awaitTermination` to wait.

---

### ✅ `shutdownNow()`

- **Use**: Tries to **stop everything immediately**.  
- Returns a list of tasks that were **awaiting execution** (not yet running).
- Running tasks may or may not stop.

---

### ✅ `isShutdown()`

- **Returns**: `true` if `shutdown()` or `shutdownNow()` was called.

---

### ✅ `isTerminated()`

- **Returns**: `true` if executor has fully shut down and all tasks are finished.

---

### ✅ `awaitTermination(long timeout, TimeUnit unit)`

- **Use**: Waits for executor to **terminate or timeout** after shutdown is called.

```java
executor.shutdown();
executor.awaitTermination(1, TimeUnit.MINUTES);
```

---

## ⏱️ 3. `ScheduledExecutorService` – For timed tasks

Extends `ExecutorService` and adds scheduling abilities:

```java
ScheduledFuture<?> schedule(Runnable command, long delay, TimeUnit unit)
ScheduledFuture<?> schedule(Callable<V> callable, long delay, TimeUnit unit)
```

- **Use**: Delays execution of a task
- **Returns**: `ScheduledFuture`

---

### 🔁 `scheduleAtFixedRate(...)`

```java
scheduleAtFixedRate(Runnable command, long initialDelay, long period, TimeUnit unit)
```

- **Starts after** `initialDelay`, runs repeatedly every `period`.
- If a task takes longer than the period → the next one starts **immediately** after.

---

### 🔁 `scheduleWithFixedDelay(...)`

```java
scheduleWithFixedDelay(Runnable command, long initialDelay, long delay, TimeUnit unit)
```

- **Starts after** `initialDelay`
- Then runs next task **after a fixed delay** from the **end** of the previous task

---

## 🧠 Example to Compare

```java
ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(1);

// Fixed Rate (every 5s no matter how long the task takes)
scheduler.scheduleAtFixedRate(() -> {
    System.out.println("Fixed Rate: " + System.currentTimeMillis());
}, 0, 5, TimeUnit.SECONDS);

// Fixed Delay (5s after previous finishes)
scheduler.scheduleWithFixedDelay(() -> {
    System.out.println("Fixed Delay: " + System.currentTimeMillis());
}, 0, 5, TimeUnit.SECONDS);
```

---

## 🛑 Shutdown Example (Full Lifecycle)

```java
ExecutorService executor = Executors.newFixedThreadPool(2);

executor.submit(() -> System.out.println("Running task..."));

executor.shutdown(); // initiate shutdown
if (!executor.awaitTermination(5, TimeUnit.SECONDS)) {
    executor.shutdownNow(); // force shutdown if it doesn't finish
}
```

---

## ✅ Summary Table

| Method                      | Interface             | Use For                               | Returns           |
|-----------------------------|------------------------|----------------------------------------|--------------------|
| `execute(Runnable)`        | Executor               | Fire-and-forget task                   | void               |
| `submit(...)`              | ExecutorService        | Task with result (Callable/Runnable)   | Future             |
| `invokeAll(...)`           | ExecutorService        | Run many, wait for all                 | List<Future>       |
| `invokeAny(...)`           | ExecutorService        | Run many, take first successful result | T (result)         |
| `shutdown()`               | ExecutorService        | Start graceful shutdown                | void               |
| `shutdownNow()`            | ExecutorService        | Force shutdown                         | List<Runnable>     |
| `schedule(...)`            | ScheduledExecutorService | Delay task                            | ScheduledFuture    |
| `scheduleAtFixedRate(...)`| ScheduledExecutorService | Repeat task (fixed rate)              | ScheduledFuture    |
| `scheduleWithFixedDelay(...)` | ScheduledExecutorService | Repeat task (fixed delay)             | ScheduledFuture    |

---
