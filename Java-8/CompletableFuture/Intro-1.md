## 🔰 1. What is `CompletableFuture`?

### ✅ Definition:

`CompletableFuture` is a class in `java.util.concurrent` that represents a **future result of an asynchronous computation**. It was introduced in **Java 8**.

### ❗Why we need it?

Before Java 8:

* We used `Future<T>` from `ExecutorService`
* But `Future` was **blocking** – you had to call `get()` and wait
* Couldn’t chain multiple async tasks easily

`CompletableFuture` solves these by:

* Running tasks **asynchronously**
* **Non-blocking** chaining (thenApply, thenAccept, etc.)
* Combining multiple futures

---

## 🔧 2. How to create a simple `CompletableFuture`?

### ✅ Example: Supply something asynchronously

```java
import java.util.concurrent.CompletableFuture;

public class Main {
    public static void main(String[] args) {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            return "Hello, World!";
        });

        // Block and get the result
        String result = future.join();  // or use future.get()
        System.out.println(result); // Output: Hello, World!
    }
}
```

---

## 🧠 Interview Q1: What's the difference between `get()` and `join()`?

| Method   | Throws Checked Exception                       | Blocks? |
| -------- | ---------------------------------------------- | ------- |
| `get()`  | Yes (InterruptedException, ExecutionException) | Yes     |
| `join()` | No (wraps exceptions in `CompletionException`) | Yes     |

📝 *Use `join()` if you don’t want to handle checked exceptions.*

---

## 🔄 3. Non-blocking - How to consume result without `get()` or `join()`?

Use `thenAccept()` or `thenApply()`

### ✅ Example: Print result when available

```java
CompletableFuture.supplyAsync(() -> "Hello")
    .thenAccept(result -> System.out.println("Result: " + result));
```

🧠 **thenAccept** takes a **Consumer** — accepts result but doesn’t return anything.

---

### ✅ Example: Modify result with `thenApply`

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> "hello");

future
    .thenApply(str -> str.toUpperCase()) // transforms result
    .thenAccept(System.out::println);    // prints HELLO
```

🧠 **thenApply** takes a **Function** — accepts result and returns a new value.

---

## 🔄 4. Chaining tasks

### ✅ Example: Chain multiple stages

```java
CompletableFuture.supplyAsync(() -> "java")
    .thenApply(str -> str + " 8")
    .thenApply(String::toUpperCase)
    .thenAccept(System.out::println); // Output: JAVA 8
```

---

## 🤝 5. Combining two futures

### ✅ thenCombine()

```java
CompletableFuture<String> future1 = CompletableFuture.supplyAsync(() -> "Hello");
CompletableFuture<String> future2 = CompletableFuture.supplyAsync(() -> "World");

future1
    .thenCombine(future2, (a, b) -> a + " " + b)
    .thenAccept(System.out::println); // Output: Hello World
```

🧠 `thenCombine` is used when both futures are **independent** and you want to use **both results**.

---

## ⏱️ 6. Running multiple futures and waiting for all

### ✅ `CompletableFuture.allOf(...)`

```java
CompletableFuture<String> f1 = CompletableFuture.supplyAsync(() -> "A");
CompletableFuture<String> f2 = CompletableFuture.supplyAsync(() -> "B");

CompletableFuture<Void> all = CompletableFuture.allOf(f1, f2);

all.thenRun(() -> {
    System.out.println("All done!");
    System.out.println("F1 = " + f1.join());
    System.out.println("F2 = " + f2.join());
});
```

🧠 `allOf()` returns a `CompletableFuture<Void>` — it doesn’t give results directly, you need to call `.join()` or `.get()` on individual futures.

---

## ❓ Questions (Basic)

1. **What is the difference between `Future` and `CompletableFuture`?**
2. **What is the use of `supplyAsync()`?**
3. **What is the difference between `thenApply` and `thenAccept`?**
4. **How do you combine two `CompletableFutures`?**
5. **What is the purpose of `CompletableFuture.allOf()`?**

---

# CompletableFuture.supplyAsync()

By default, **`CompletableFuture.supplyAsync()`** uses the **ForkJoinPool.commonPool()**, and the threads in that pool are **daemon threads**, not user threads.

💡 **Daemon threads**

* JVM does **not** wait for daemon threads to finish.
* When only daemon threads are left running, the JVM exits immediately.

💡 **User threads**

* JVM waits for them to finish before shutting down.

So in our code:

```java
final int num = 4;
CompletableFuture<Integer> cf = CompletableFuture.supplyAsync(() -> num * num);
cf.thenApply(no -> 2 * no)
  .thenAccept(no -> System.out.println(no));
```

If the main thread exits before the async computation finishes, and since `supplyAsync()` runs on daemon threads by default, our program **might terminate before printing anything**.

✅ **To prevent that**, we can:

* Either call `cf.join()` (waits for completion), or
* Use a custom Executor with user threads:

  ```java
  ExecutorService executor = Executors.newFixedThreadPool(2);
  CompletableFuture.supplyAsync(() -> num * num, executor)
      .thenApply(no -> 2 * no)
      .thenAccept(System.out::println);
  executor.shutdown();
  ```

