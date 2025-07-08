# ✅ QUIZ: CompletableFuture Concepts

---

## ❓ **Q1. What is the difference between `thenApply()` and `thenCompose()`?**

**Example**:

```java
CompletableFuture<String> cf = CompletableFuture.supplyAsync(() -> "data");

cf.thenApply(...);  
cf.thenCompose(...);
```

What’s the key difference in their behavior?

### Solution

**thenApply vs thenCompose**

| Feature        | `thenApply`                         | `thenCompose`                         |
| -------------- | ----------------------------------- | ------------------------------------- |
| Purpose        | Transforms the result               | Chains dependent async tasks          |
| Input Function | `T -> R`                            | `T -> CompletableFuture<R>`           |
| Output         | `CompletableFuture<R>`              | `CompletableFuture<R>` (flattened)    |
| Typical Use    | Add logic after result is available | Run a new async task using the result |

✅ Use `thenApply` when you're just mapping a result.
✅ Use `thenCompose` when the next step itself returns a `CompletableFuture`.

---

### ✅ Example:

```java
// thenApply: result mapping
cf.thenApply(data -> data.length()); // CompletableFuture<Integer>

// thenCompose: chaining another async call
cf.thenCompose(data -> fetchDetails(data)); // CompletableFuture<Details>
```

---

## ❓ **Q2. What does CompletableFuture.allOf(...) return, and how do you extract the actual results?**

### Solution

**`CompletableFuture.allOf(...)`**

| Aspect              | Explanation                                                      |
| ------------------- | ---------------------------------------------------------------- |
| Return Type         | `CompletableFuture<Void>`                                        |
| Purpose             | Wait for **all** futures to complete                             |
| How to get results? | Use `.join()` or `.get()` on the **original individual futures** |
| How to transform?   | Chain with `.thenApply(...)` on the `allOf(...)` result          |

---

### ✅ Example:

```java
CompletableFuture<String> f1 = ...;
CompletableFuture<Integer> f2 = ...;

CompletableFuture<Void> all = CompletableFuture.allOf(f1, f2);

CompletableFuture<String> result = all.thenApply(v -> {
    String s = f1.join();
    int n = f2.join();
    return s + " - " + n;
});
```

---

## ❓ **Q3. What's the difference between `exceptionally`, `handle`, and `whenComplete` in terms of error handling and return value?**

### Solution

**`exceptionally` vs `handle` vs `whenComplete`**

| Feature          | `exceptionally`                   | `handle`                             | `whenComplete`                          |
| ---------------- | --------------------------------- | ------------------------------------ | --------------------------------------- |
| Purpose          | Handle errors only                | Handle both **success and failure**  | Observe success or error (side-effects) |
| Handles success? | ❌ No                              | ✅ Yes                                | ✅ Yes                                   |
| Handles error?   | ✅ Yes                             | ✅ Yes                                | ✅ Yes                                   |
| Return type      | Must return same type as original | Can return **any type**              | Return is ignored (`void` lambda)       |
| Modifies result? | ✅ Yes (on error only)             | ✅ Yes (both paths)                   | ❌ No                                    |
| Consumes error?  | ✅ Yes (prevents further throwing) | ✅ Yes                                | ❌ No (error still thrown on `.join()`)  |
| Use case         | Fallback when error happens       | Unified error/success transformation | Logging, auditing, cleanup              |

---

### ✅ Examples:

```java
// exceptionally
future.exceptionally(ex -> fallback);

// handle
future.handle((result, ex) -> ex != null ? fallback : transform(result));

// whenComplete
future.whenComplete((result, ex) -> {
    if (ex != null) log(ex);
    else log(result);
});
```

---

## ❓ **Q4. What is the purpose of `thenCombine()` and how is it different from `thenCompose()`?**

### Solution

**`thenCombine()` vs `thenCompose()`**

| Feature           | `thenCombine()`                                   | `thenCompose()`                                             |
| ----------------- | ------------------------------------------------- | ----------------------------------------------------------- |
| Purpose           | Combine **two independent** futures               | Chain **dependent** futures                                 |
| Both futures run? | ✅ Yes — in parallel                               | ❌ No — second runs after the first                          |
| Input Futures     | `CompletableFuture<A>` and `CompletableFuture<B>` | `CompletableFuture<A>` then leads to `CompletableFuture<B>` |
| Combination Logic | Takes two results: `(a, b) -> result`             | Takes result from first to create second                    |
| Return            | `CompletableFuture<R>`                            | `CompletableFuture<R>`                                      |
| Use Case          | Merge results like data + pricing, etc.           | Fetch user, then settings for user                          |

---

### ✅ Example: `thenCombine`

```java
CompletableFuture<String> name = getName();
CompletableFuture<Integer> age = getAge();

CompletableFuture<String> result = name.thenCombine(age, (n, a) ->
    "Name: " + n + ", Age: " + a);
```

---

### ✅ Example: `thenCompose`

```java
CompletableFuture<User> user = getUserById("1");

CompletableFuture<Settings> settings = user.thenCompose(u ->
    getSettingsForUser(u));
```

---


## ❓ **Q5. What is the output type of this code and why?**

```java
CompletableFuture<String> cf = CompletableFuture.supplyAsync(() -> "hello");
CompletableFuture<Integer> result = cf.thenApply(str -> str.length());
```

What is the type of `result` and how is it determined?

### Solution

* `cf` holds a `String`
* `thenApply(...)` transforms that `String` into an `Integer` using `.length()`
* So the return type of `thenApply(...)` is `CompletableFuture<Integer>`

---

### ✅ Extraction:

```java
Integer len = result.join(); // or result.get();
System.out.println(len);     // Output: 5
```

---

### 🔁 Summary:

| Method      | Transformation       | Output Type                 |
| ----------- | -------------------- | --------------------------- |
| `thenApply` | `T → R`              | `CompletableFuture<R>`      |
| `join()`    | Extracts final value | `R` (blocks until complete) |

---

## ❓ **Q6. Real-world scenario: CompletableFuture flow**

Suppose you are building a user dashboard service:

* Step 1: Fetch a user by ID → `CompletableFuture<User>`
* Step 2: Fetch the user's settings (language) → `CompletableFuture<Settings>`
  (depends on Step 1)
* Step 3: Log the result or error
* Step 4: If user fetch fails, return `User("Guest")`
  If settings fetch fails, return `Settings("English")`

---

### ❓ Your Task:

Which CompletableFuture methods will you use **at each step** and why?

(Hint: think about `thenCompose`, `exceptionally`, `handle`, `whenComplete`...)

### Solution

**Real-World CompletableFuture Flow**

### 🧩 Scenario Steps and Methods to Use:

| Step | Action                         | Method Used     | Why                                                                |
| ---- | ------------------------------ | --------------- | ------------------------------------------------------------------ |
| 1️⃣  | Fetch user by ID               | `exceptionally` | To catch error and return fallback `User("Guest")`                 |
| 2️⃣  | Fetch settings using user      | `thenCompose`   | Because it depends on the result of the previous async call        |
| 3️⃣  | Handle error in settings fetch | `handle`        | To catch exceptions and return fallback `Settings("English")`      |
| 4️⃣  | Final logging                  | `whenComplete`  | To log final outcome (success or failure) without modifying result |

---

### ✅ Flow Summary:

```java
CompletableFuture<User> cfUser = fetchUserById("1")
    .exceptionally(ex -> {
        System.out.println("User fetch failed");
        return new User("Guest");
    });

CompletableFuture<String> result = cfUser.thenCompose(user ->
    fetchSettingsForUser(user)
        .handle((settings, ex) -> {
            if (ex != null) {
                System.out.println("Settings fetch failed for " + user.name());
                return new Settings("English");
            }
            return settings;
        })
        .thenApply(settings ->
            "User " + user.name() + " uses " + settings.language()
        )
).whenComplete((res, ex) ->
    System.out.println("Final log: " + res)
);

System.out.println("Final Output: " + result.join());
```

---

