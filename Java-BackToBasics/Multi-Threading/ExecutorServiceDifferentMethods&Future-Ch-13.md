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


# Future

## ❓ The Core Question

> "If computation happens in the future, how does `submit()` immediately return a `Future`? What exactly does `Future` return?"

**Short Answer**:  
The `submit()` method starts the computation *in the background*, and immediately gives you a `Future` — which is just a **placeholder** for the result that will be ready **later**.

Let’s see this in action.

---

## 🛍️ Analogy: Ordering Food at a Restaurant

- You go to a restaurant and order a pizza. 🍕
- They give you a **token (like a number)** — it doesn’t contain the pizza, it just **represents** the fact that your pizza is being made.
- You wait for your number to be called. That’s when you get the actual pizza.

➡️ That **token** is your `Future`.  
➡️ The **chef** is your `ExecutorService`.  
➡️ The **pizza** is the **result** of the background computation.

---

## 🧪 Code Example

```java
ExecutorService executor = Executors.newSingleThreadExecutor();

Future<String> future = executor.submit(() -> {
    Thread.sleep(3000);  // Simulate slow work
    return "Hello";
});

System.out.println("I got the Future immediately!");

// Now we wait for the actual result
String result = future.get();  // blocks until the task finishes
System.out.println("The result is: " + result);
```

### 🔍 What happened:

1. `submit()` asks the executor to run the task asynchronously.
2. `submit()` **immediately** returns a `Future<String>` object.
   - That object doesn't contain the result yet.
   - It just knows: "Okay, this task has been submitted. I'll let you check on it later."
3. The task runs in a **background thread**.
4. When you call `future.get()`, it blocks until the task completes and returns the actual result `"Hello"`.

---

## ⚙️ What Is the Future Actually Holding?

A `Future<T>` is just an object with these capabilities:
- `get()` — wait and return the result
- `isDone()` — check if the task is finished
- `cancel()` — try to cancel the task

So it holds:
- A **reference to the task**
- A way to **query or retrieve the result later**
- A **state**: pending, running, done, or cancelled

It's like a **promise** — "I promise I’ll get you this result when it’s ready."

---

## ✅ Final Summary

| Thing                    | Explanation                                                                 |
|--------------------------|-----------------------------------------------------------------------------|
| `submit()`               | Starts the task in the background                                           |
| Returns a `Future<T>`    | A placeholder (or token) for the result                                     |
| `get()`                  | Blocks until the actual result is ready                                     |
| Why immediate return?    | You're not getting the result — you're getting a *promise* of future result |

---

## 🧠 What is `Future`?

`Future` is an interface in `java.util.concurrent` introduced in **Java 5**.

> It represents the **result of an asynchronous computation**, which **may not be available yet**.

So:
- You **submit a task** to an executor.
- It runs **in the background**.
- You get a `Future<T>` back.
- You can use the future to:
  - Wait for the result (`get()`)
  - Check if the task is done (`isDone()`)
  - Cancel the task (`cancel()`)

---

## 🛠 How to Use `Future`

### 🔹 Step-by-step Example

```java
ExecutorService executor = Executors.newSingleThreadExecutor();

Future<Integer> future = executor.submit(() -> {
    Thread.sleep(2000); // simulate delay
    return 42;
});

System.out.println("Doing other work...");

// Block until result is ready
Integer result = future.get();
System.out.println("Result: " + result);

executor.shutdown();
```

---

## 🧰 Methods in the `Future` Interface

| Method                      | What It Does                                                    |
|-----------------------------|------------------------------------------------------------------|
| `get()`                     | Waits (blocks) until the task is done, then returns the result  |
| `get(long timeout, TimeUnit unit)` | Waits up to a timeout, or throws `TimeoutException`         |
| `isDone()`                  | Returns `true` if the task is finished                          |
| `isCancelled()`             | Returns `true` if the task was cancelled                        |
| `cancel(boolean mayInterruptIfRunning)` | Attempts to cancel the task                        |

---

## 💥 Important Characteristics

### 1. 🔒 Blocking Nature

`get()` **blocks the current thread** until the task is complete.  
That means it's **not truly non-blocking or reactive**.

---

### 2. 🚫 No Chaining

Unlike `CompletableFuture`, `Future` cannot say:
> “After this finishes, do something else.”

You have to write it manually.

---

### 3. ⛔ No Built-in Exception Handling

If the task throws an exception, calling `get()` throws `ExecutionException`.  
You must unwrap the actual cause from it.

```java
try {
    future.get();
} catch (ExecutionException e) {
    Throwable actualException = e.getCause();
}
```

---

## 🧠 Under the Hood: How `Future` Works

- You **submit** a `Callable` or `Runnable` to an `ExecutorService`.
- It returns a `Future` immediately.
- The actual task is run in a thread pool thread.
- Once finished, the `Future` contains the result (or exception).

---

## 🧪 Real-World Use Case

Let’s say you’re doing 3 things in parallel: load user info, load settings, and load notifications.

```java
Future<User> userFuture = executor.submit(() -> loadUser());
Future<Settings> settingsFuture = executor.submit(() -> loadSettings());
Future<List<Notification>> notifFuture = executor.submit(() -> loadNotifications());

// Wait for all
User user = userFuture.get();
Settings settings = settingsFuture.get();
List<Notification> notifs = notifFuture.get();
```

---

## 🚧 Limitations of `Future`

1. ❌ No chaining (like `thenApply`, `thenCombine`)
2. ❌ No built-in async composition
3. ❌ Blocks the thread on `get()`
4. ❌ Harder to handle exceptions
5. ❌ Not reactive or functional
6. ❌ No progress monitoring (e.g., no partial updates)

---

## ✅ When to Use `Future`

- Simple, one-off async tasks
- Where blocking is acceptable
- When working in older Java versions (pre-Java 8)

---

## 🔄 Future vs CompletableFuture

| Feature                 | `Future`                 | `CompletableFuture`          |
|-------------------------|--------------------------|-------------------------------|
| Introduced in           | Java 5                   | Java 8                        |
| Non-blocking            | ❌ get() blocks           | ✅ fully non-blocking          |
| Chaining support        | ❌                       | ✅ (`thenApply`, `thenCombine`) |
| Composition of tasks    | ❌                       | ✅                             |
| Exception handling      | ❌                       | ✅ (`exceptionally`, `handle`) |
| Reactive style support  | ❌                       | ✅                             |
| Progress updates        | ❌                       | ❌ (still limited)             |

---

## 🧠 Final Summary

- `Future` is a **basic building block** for async programming in Java.
- It's **safe, easy, and simple**, but also **limited**.
- Great for **legacy** code or **simple parallelism**.
- For advanced async workflows, **use `CompletableFuture`** instead.

---
