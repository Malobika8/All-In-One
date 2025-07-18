# What is CompletableFuture in Java? How is it different from a regular Future?

### Sol:

#### 🔹 `Future` (Pre-Java 8):

* Introduced in Java 5 via `ExecutorService`.
* You submit a task and get a `Future` back.
* But to get the result, you must call `.get()`, which is **blocking** — it waits until the task completes.
* Doesn’t support chaining or combining multiple tasks.
* No elegant way to handle exceptions.

#### 🔹 `CompletableFuture` (Java 8+):

* An enhancement over `Future` that allows:

  * **Non-blocking** asynchronous computation.
  * **Chaining** of dependent tasks (`thenApply`, `thenAccept`, etc.)
  * **Combining multiple futures** (`thenCombine`, `allOf`, `anyOf`)
  * **Exception handling** (`exceptionally`, `handle`, `whenComplete`)
* Supports **event-driven**, **callback-based** programming.
* Uses a **ForkJoinPool** by default, so you don’t need to manually manage threads.

| Feature            | Future        | CompletableFuture        |
| ------------------ | ------------- | ------------------------ |
| Blocking           | Yes (`get()`) | No (non-blocking chains) |
| Chaining           | ❌             | ✅ (`thenApply`, etc.)    |
| Combine Futures    | ❌             | ✅                        |
| Exception Handling | ❌             | ✅                        |
| Thread management  | Manual        | Auto via ForkJoinPool    |

---

# Write a piece of code that:

* Runs a task asynchronously that returns a String `"Hello"`
* Transforms the result to uppercase using `thenApply()`
* Prints the final result

### Sol:

```
CompletableFuture.supplyAsync(()->"Hello")
            .thenApply(str -> str.toUpperCase())
            .thenAccept(str -> System.out.println(str));
```

- ✅ supplyAsync() → used to run a task that returns a result (non-blocking)
- ✅ thenApply() → used to transform the result (String -> String)
- ✅ thenAccept() → used to consume the result (returns void)

---

# Write code that:
- Asynchronously runs a task that divides 10 by 0 (which throws an exception)
- Handle the exception using .exceptionally(...) and return "Failed" if any exception occurs
- Finally print the result

### Sol:

```
CompletableFuture.supplyAsync(() -> 10 / 0)
    .exceptionally(ex -> {
        System.out.println("Exception occurred: " + ex);
        return -1; // return a default int on failure
    })
    .thenAccept(result -> System.out.println("Result: " + result));
```

#### Explanation:
- supplyAsync() → returns CompletableFuture<Integer>
So .exceptionally(...) must return an Integer
If you want to return a string like "Failed", you should change your original task to return a String instead.

---

# Write a program that:
- Runs one async task to return "Hello"
- Runs another async task to return "World"
- Combine both using thenCombine() into: "Hello World"
- Print the final result

### Sol:

```
CompletableFuture<String> first = CompletableFuture.supplyAsync(()->"Hello");
        CompletableFuture<String> second = CompletableFuture.supplyAsync(()->"World");
        
        first.thenCombine(second, (a,b)->a + " " + b)
        .thenAccept(System.out::println);
```

---

# Write a program that:
- Async task returns a username: "malobika"
- Use that result to trigger another async task that returns a greeting: "Hello, malobika"
- Print the final greeting
- Use thenCompose() to chain them.

### Sol:

```
CompletableFuture<String> first = CompletableFuture.supplyAsync(() -> "malobika");

first.thenCompose(str ->
        CompletableFuture.supplyAsync(() -> "Hello " + str)
    )
    .thenAccept(System.out::println);
```

---

# Task:

You have two methods,

```
public static CompletableFuture<String> fetchUserId() {
    return CompletableFuture.supplyAsync(() -> "user123");
}

public static CompletableFuture<String> fetchUserDetails(String userId) {
    return CompletableFuture.supplyAsync(() -> "Details of " + userId);
}
```

####  Task:
- Call fetchUserId() asynchronously.
- Once the userId is received, call fetchUserDetails(userId) using thenCompose().
- Finally, print the result.

### Sol:

```
CompletableFuture<String> first = fetchUserId();
        first.thenCompose(id->fetchUserDetails(id))
        .thenAccept(System.out::println);
```

---

# Awesome! You're doing great. Let’s now tackle:

---

## 🔹 `CompletableFuture.allOf()` vs `anyOf()`

These are used when you want to **run multiple async tasks in parallel**.

---

# Use `CompletableFuture.allOf()`

Suppose you have 3 services that run in parallel:

```java
public static CompletableFuture<String> fetchName() {
    return CompletableFuture.supplyAsync(() -> "Malobika");
}

public static CompletableFuture<String> fetchRole() {
    return CompletableFuture.supplyAsync(() -> "Developer");
}

public static CompletableFuture<String> fetchLocation() {
    return CompletableFuture.supplyAsync(() -> "India");
}
```

#### Task:

* Run all three tasks in parallel using `CompletableFuture.allOf(...)`
* Wait for all to complete
* Collect and print the combined result like this:

```
Malobika - Developer - India
```

* Use `CompletableFuture.allOf(...)`
* Wait using `.join()`
* Then extract results from the original futures

### Sol:

```
CompletableFuture<String> nameFuture = fetchName();
CompletableFuture<String> roleFuture = fetchRole();
CompletableFuture<String> locationFuture = fetchLocation();

// Wait for all futures to complete
CompletableFuture<Void> allDone = CompletableFuture.allOf(nameFuture, roleFuture, locationFuture);

// When all are done, extract results and print
allDone.thenRun(() -> {
    String name = nameFuture.join();       // safe now because all have completed
    String role = roleFuture.join();
    String location = locationFuture.join();

    System.out.println(name + " - " + role + " - " + location);
});
```

---

# Task

You have these three fake services (simulate with delay):

```java
public static CompletableFuture<String> fetchFromServer1() {
    return CompletableFuture.supplyAsync(() -> {
        sleep(2000); // 2 seconds
        return "Server1 Response";
    });
}

public static CompletableFuture<String> fetchFromServer2() {
    return CompletableFuture.supplyAsync(() -> {
        sleep(1000); // 1 second
        return "Server2 Response";
    });
}

public static CompletableFuture<String> fetchFromServer3() {
    return CompletableFuture.supplyAsync(() -> {
        sleep(3000); // 3 seconds
        return "Server3 Response";
    });
}

public static void sleep(long ms) {
    try { Thread.sleep(ms); } catch (InterruptedException e) { }
}
```

#### Task:

* Use `anyOf()` to **wait for the fastest server**
* Print its result as soon as one responds

Expected output (after \~1 second):

```
Server2 Response
```

### Sol:

```
CompletableFuture.anyOf(fetchFromServer1(),fetchFromServer2(),fetchFromServer3())
        .thenAccept(System.out::println);
```

---

# Write a CompletableFuture that:

- Divides 10 / 0 (will throw an exception)
- Use .whenComplete() to log the error or result
- Then use .exceptionally() to return "Failed"
- Finally print the result

### Sol:

```
CompletableFuture.supplyAsync(() -> 10 / 0)
    .whenComplete((result, ex) -> {
        if (ex != null) {
            System.out.println("Exception occurred in whenComplete: " + ex.getMessage());
        } else {
            System.out.println("Computation result: " + result);
        }
    })
    .exceptionally(ex -> {
        System.out.println("Handled in exceptionally: " + ex.getMessage());
        return -1;
    })
    .thenAccept(result -> System.out.println("Final result: " + result));
```

---

# Write a CompletableFuture that:
- Performs 10 / 0 (throws exception)
- Use .handle() to check if an exception occurred
- If exception: return -1
- Else: return the result
- Finally print the returned value

### Sol:

```
CompletableFuture.supplyAsync(() -> 10 / 0)
    .handle((result, ex) -> {
        if (ex != null) {
            System.out.println("Exception handled in handle(): " + ex.getMessage());
            return -1;
        } else {
            return result;
        }
    })
    .thenAccept(System.out::println);
```

---
