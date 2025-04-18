# Future VS CompletableFuture

> *“If I never call `get()`, `Future` is non-blocking.”*

✔️ Yes, if you just submit a task and **never block on it**, you're not blocking anything.

```java
Future<String> future = executor.submit(() -> longTask());
// Doing other stuff — no blocking here
```

This is true.

BUT… here’s where the fuss comes from:

---

## 🤔 The Core Issue: `Future` Doesn’t Let You Do Anything With the Result *Unless* You Block

So the real difference is this:

| Feature                           | `Future`                    | `CompletableFuture`         |
|----------------------------------|-----------------------------|-----------------------------|
| Can run async task               | ✅                          | ✅                          |
| Can retrieve result **non-blockingly** | ❌ You must call `get()`     | ✅ via callbacks (`then...`) |
| Can react to result automatically | ❌ No built-in mechanism     | ✅ Fully event-driven         |

So even though you **can avoid blocking** with `Future` (by never calling `get()`), you also **can’t do anything useful** unless you:

- Block for the result  
**OR**
- Manually check with `isDone()` in a loop (which becomes polling, which is inefficient)

---

## 🧪 Let's Compare

### With `Future` (non-blocking attempt):

```java
Future<String> future = executor.submit(() -> "Hi");

while (!future.isDone()) {
    // Polling (not efficient)
    Thread.sleep(100);
}

System.out.println(future.get()); // still ends up blocking briefly
```

👎 This is **not elegant**, and you end up doing manual polling.

---

### With `CompletableFuture`:

```java
CompletableFuture
    .supplyAsync(() -> "Hi")
    .thenApply(msg -> msg + " there!")
    .thenAccept(System.out::println);
```

👍 No polling, no blocking. Logic flows reactively.

---

## 🔁 Analogy Time

Let’s say you order a pizza 🍕.

- With `Future`: You keep calling the shop every 5 minutes — "Is it ready yet? Is it ready yet?"  
  (That's polling via `isDone()` + blocking on `get()`)

- With `CompletableFuture`: The shop sends you a text when it’s ready and **your phone triggers a pizza party** 🎉  
  (That’s `thenAccept()` reacting when the result is done)

---

## 🔥 TL;DR

| Myth                        | Truth                                                       |
|-----------------------------|--------------------------------------------------------------|
| “Future is non-blocking”    | Only **if you don’t call `get()`**, but then it’s **useless** |
| “CompletableFuture is better” | Yes — because it lets you **chain, compose, and react** to results without blocking |

---

So the **fuss** is not about whether Future can avoid blocking.  
It's about how **limited and manual** it becomes if you try to use it in non-blocking ways — and how **much smoother** `CompletableFuture` makes the same job.

# Completable Future

## ✅ What is `CompletableFuture`?

`CompletableFuture` is part of `java.util.concurrent`, introduced in **Java 8**.  
It represents a **future result** of an asynchronous computation, and unlike `Future`, it’s:

- **Non-blocking**
- **Composable**
- **Chainable**
- **Reactive**

---

## 🧠 Why Do We Need It?

`Future` is limited:
- You must block using `get()`
- No callbacks
- No chaining or combining

`CompletableFuture` solves this by letting you:
- **Run async code**
- **Attach actions** when the result is ready
- **Chain and combine** tasks
- **Handle errors** functionally

---

## 🔨 Creating `CompletableFuture`

### 1. **Manually**
```java
CompletableFuture<String> future = new CompletableFuture<>();
// later...
future.complete("Hello");
```

### 2. **Run async tasks**
```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> "Hello");
```

- `runAsync()` → for `Runnable` (returns `CompletableFuture<Void>`)
- `supplyAsync()` → for `Supplier<T>` (returns `CompletableFuture<T>`)

---

## 🧱 Core Operations

### ✅ `thenApply()`
Transforms the result.
```java
CompletableFuture<String> greeting = CompletableFuture
    .supplyAsync(() -> "Hello")
    .thenApply(str -> str + " World");
```

### ✅ `thenAccept()`
Consumes the result.
```java
.thenAccept(System.out::println);
```

### ✅ `thenRun()`
Runs a task without using the result.
```java
.thenRun(() -> System.out.println("Done!"));
```

---

## 🔄 Chaining Async Tasks

### ✅ `thenCompose()`

Used when one task depends on another's result.

```java
CompletableFuture<User> userFuture = CompletableFuture
    .supplyAsync(() -> fetchUserId())
    .thenCompose(id -> CompletableFuture.supplyAsync(() -> fetchUser(id)));
```

📌 Think: **flatMap for async**  
If `thenApply()` returns a `CompletableFuture`, you get a nested future.  
`thenCompose()` unwraps it.

---

## 🔗 Combining Multiple Futures

### ✅ `thenCombine()`
Run tasks in parallel, then combine results.

```java
CompletableFuture<String> f1 = CompletableFuture.supplyAsync(() -> "Hello");
CompletableFuture<String> f2 = CompletableFuture.supplyAsync(() -> "World");

f1.thenCombine(f2, (a, b) -> a + " " + b)
  .thenAccept(System.out::println); // Hello World
```

### ✅ `thenAcceptBoth()`
Like `thenCombine`, but returns `CompletableFuture<Void>`

---

## 👯‍♂️ Waiting for Multiple Futures

### ✅ `CompletableFuture.allOf(...)`

```java
CompletableFuture<String> f1 = ...
CompletableFuture<Integer> f2 = ...
CompletableFuture<Void> all = CompletableFuture.allOf(f1, f2);

all.thenRun(() -> {
    // all completed
    String result1 = f1.join(); // get() would throw checked exceptions
    Integer result2 = f2.join();
});
```

### ✅ `CompletableFuture.anyOf(...)`

Wait for **first to complete**.

```java
CompletableFuture<Object> any = CompletableFuture.anyOf(f1, f2);
```

---

## 💥 Exception Handling

### ✅ `exceptionally()`
Fallback on error.

```java
CompletableFuture<String> future = CompletableFuture
    .supplyAsync(() -> {
        if (true) throw new RuntimeException("Fail");
        return "Success";
    })
    .exceptionally(ex -> "Fallback");
```

### ✅ `handle()`
Handle success or failure together.

```java
.handle((result, ex) -> {
    if (ex != null) return "Error";
    return result;
});
```

### ✅ `whenComplete()`
Side effects (like logging)

```java
.whenComplete((result, ex) -> {
    if (ex != null) log(ex);
    else log(result);
});
```

---

## 🕓 Timeout Handling

```java
future.orTimeout(3, TimeUnit.SECONDS);     // Java 9+
future.completeOnTimeout("fallback", 3, TimeUnit.SECONDS);
```

---

## 😴 Blocking Methods

Use **only if necessary**:

| Method     | Description                     |
|------------|---------------------------------|
| `get()`    | Waits and throws checked exception |
| `join()`   | Waits and throws unchecked exception |
| `getNow(default)` | Returns immediately if complete |
| `isDone()` | Check if complete               |

---

## 🧪 Real Use Case: Parallel Calls + Composition

```java
CompletableFuture<User> userFuture = CompletableFuture.supplyAsync(() -> fetchUser());
CompletableFuture<Settings> settingsFuture = CompletableFuture.supplyAsync(() -> fetchSettings());

CompletableFuture<Void> both = CompletableFuture.allOf(userFuture, settingsFuture);

both.thenRun(() -> {
    User u = userFuture.join();
    Settings s = settingsFuture.join();
    renderDashboard(u, s);
});
```

---

## 🧠 Summary Table

| Concept              | Use |
|----------------------|-----|
| `runAsync` / `supplyAsync` | Run background tasks |
| `thenApply` / `thenAccept` | Transform / consume result |
| `thenCompose` | Chain dependent async calls |
| `thenCombine` / `allOf` | Parallel + merge |
| `exceptionally` / `handle` | Error handling |
| `get()` / `join()` | Blocking retrieval (avoid if possible) |
| `orTimeout()` | Timeout built-in (Java 9+) |

---

## 🧭 Advanced Bonus (Optional)

- `CompletableFuture.delayedExecutor(...)` – delay execution
- `Executor` injection – customize thread pools
- Pipelines of tasks
- Using with reactive APIs (Spring WebClient, etc.)

---

## 🚀 Final Thoughts

`CompletableFuture` makes Java **truly async & reactive**, and replaces most `Future` use cases.

If you ever find yourself:
- Blocking with `get()` – try chaining instead
- Waiting for many tasks – use `allOf`
- Doing async steps – try `thenCompose`

---
