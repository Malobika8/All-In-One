# ✅ **CompletableFuture Quick Summary Sheet**

---

## 🔹 Basic Methods

| Method             | Purpose                                | Return Type               | Notes                                   |
| ------------------ | -------------------------------------- | ------------------------- | --------------------------------------- |
| `supplyAsync()`    | Run task asynchronously, return result | `CompletableFuture<T>`    | Accepts `Supplier<T>`                   |
| `runAsync()`       | Run async task with no return          | `CompletableFuture<Void>` | Accepts `Runnable`                      |
| `join()` / `get()` | Get result (blocking)                  | `T`                       | `join()` = unchecked; `get()` = checked |

---

## 🔹 Chaining

| Method          | Input Function Type        | Returns                     | Use Case                                   |
| --------------- | -------------------------- | --------------------------- | ------------------------------------------ |
| `thenApply()`   | `T → R`                    | `CompletableFuture<R>`      | Transform result                           |
| `thenCompose()` | `T → CompletableFuture<R>` | `CompletableFuture<R>`      | Chain dependent tasks                      |
| `thenCombine()` | `(T, U) → R`               | `CompletableFuture<R>`      | Combine results of **independent** futures |
| `allOf(...)`    | `CompletableFuture<?>...`  | `CompletableFuture<Void>`   | Wait for all to complete                   |
| `anyOf(...)`    | `CompletableFuture<?>...`  | `CompletableFuture<Object>` | Return first completed                     |

---

## 🔹 Error Handling

| Method            | Handles Success | Handles Error | Can Transform? | Consumes Exception? | Notes                    |
| ----------------- | --------------- | ------------- | -------------- | ------------------- | ------------------------ |
| `exceptionally()` | ❌ No            | ✅ Yes         | ✅ (fallback)   | ✅ Yes               | Error recovery only      |
| `handle()`        | ✅ Yes           | ✅ Yes         | ✅ Yes          | ✅ Yes               | Unified success + error  |
| `whenComplete()`  | ✅ Yes           | ✅ Yes         | ❌ No           | ❌ No                | For logging/side-effects |

---

## 🔹 Real-World Patterns

### ✅ Dependent Flow

```java
cf1.thenCompose(result1 -> cf2(result1))
```

### ✅ Parallel Tasks

```java
CompletableFuture.allOf(cf1, cf2).thenApply(v -> {
    return combine(cf1.join(), cf2.join());
});
```

### ✅ Fallbacks

```java
cf.exceptionally(ex -> fallbackValue);
```

---

## 🔹 Notes on Return Types

| Method        | Returns New Future? | Nested Future? | Flattened? |
| ------------- | ------------------- | -------------- | ---------- |
| `thenApply`   | ✅ Yes               | ❌ No           | ❌ No       |
| `thenCompose` | ✅ Yes               | ✅ Yes          | ✅ Yes      |

---

