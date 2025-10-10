# thenCombine VS thenCombineAsync

### 🔹 `thenCombine`

* Suppose you have:

```java
cf1.thenCombine(cf2, (a, b) -> a + b)
```

* Behavior:

  1. `cf1` and `cf2` run independently on their threads (maybe common pool threads or custom executor).
  2. **Whichever future completes last** (either `cf1` or `cf2`) — that thread immediately runs the combining function `(a, b) -> a + b`.
* ✅ This is **synchronous** in the sense that it runs on an existing thread — no extra thread is created.

### 🔹 `thenCombineAsync`

* Now with:

```java
cf1.thenCombineAsync(cf2, (a, b) -> a + b)
```

* Behavior:

  1. `cf1` and `cf2` run independently.
  2. Once both are complete, the combining function `(a, b) -> a + b` is **scheduled asynchronously** in:

     * **ForkJoinPool.commonPool** by default, or
     * **Custom executor** if you provide one.
* ✅ This guarantees the combining runs **in a separate thread** (not necessarily the thread that completed the last future).

### 🔹 Visualization

```
cf1 ---> [thread A] -----\
                           \
                            --> thenCombine --> runs on LAST completing thread (A or B)
cf2 ---> [thread B] -----/

cf1 ---> [thread A] -----\
                           \
                            --> thenCombineAsync --> runs in ForkJoinPool (maybe thread C)
cf2 ---> [thread B] -----/
```

### 🔹 Key takeaway

* **thenCombine** → no extra thread, runs on completing thread of the last future.
* **thenCombineAsync** → extra thread from common pool (or your executor), truly asynchronous.

---

# **Problem 1: Combine Two Asynchronous Tasks**

Write a `CompletableFuture` example where:

* You fetch a `User` (simulate with a `supplyAsync`)
* You fetch the `UserSettings` (simulate similarly)
* Once both are available, combine the result and print:
  `"User: <name>, Settings: <language>"`

---

Here's a skeleton for you to fill in:

```java
import java.util.concurrent.*;

public class Main {
    public static void main(String[] args) throws Exception {
        CompletableFuture<User> userFuture = CompletableFuture.supplyAsync(() -> fetchUser());
        CompletableFuture<Settings> settingsFuture = CompletableFuture.supplyAsync(() -> fetchSettings());

        // Combine both futures here and print the final string
    }

    static User fetchUser() {
        // Simulate delay
        sleep(1000);
        return new User("Malobika");
    }

    static Settings fetchSettings() {
        sleep(1500);
        return new Settings("English");
    }

    static void sleep(long millis) {
        try { Thread.sleep(millis); } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
    record Settings(String language) {}
}
```

---

### Solution

```
public static void main(String[] args) throws ExecutionException, InterruptedException, TimeoutException {
        CompletableFuture<User> future1 = CompletableFuture.supplyAsync(() -> fetchUser());
        CompletableFuture<Settings> future2 = CompletableFuture.supplyAsync(() -> fetchSettings());

        future1.thenCombine(future2, (user, settings) -> "User: " + user +" , " + "Settings: " + settings)
                .thenAccept( str -> System.out.println(str)).join();
    }
    static User fetchUser() {
        // Simulate delay
        sleep(1000);
        return new User("Malobika");
    }

    static Settings fetchSettings() {
        sleep(1500);
        return new Settings("English");
    }

    static void sleep(long millis) {
        try { Thread.sleep(millis); } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
    record Settings(String language) {}
```

# Problem 2: `thenCompose`

Try chaining two async calls where the **second one depends on the result of the first**.

---

### **Problem 2: thenCompose**

* Fetch a user by ID.
* Then, fetch settings for that user (pass `User` to second method).
* Use `thenCompose()` to chain them.
* Finally, print `"<name>'s language is <language>"`

Here’s a starter for you:

```java
public static void main(String[] args) {
    CompletableFuture<String> result =
        fetchUserById("u123")
        .thenCompose(user -> fetchSettingsForUser(user))
        .thenApply(settings -> user.name() + "'s language is " + settings.language()); // fix this line

    result.thenAccept(System.out::println).join();
}

static CompletableFuture<User> fetchUserById(String id) {
    return CompletableFuture.supplyAsync(() -> {
        sleep(1000);
        return new User("Malobika");
    });
}

static CompletableFuture<Settings> fetchSettingsForUser(User user) {
    return CompletableFuture.supplyAsync(() -> {
        sleep(1000);
        return new Settings("English");
    });
}

record User(String name) {}
record Settings(String language) {}
```

### Solution

```
public static void main(String[] args) throws ExecutionException, InterruptedException, TimeoutException {
        CompletableFuture<User> cfUser = fetchUserById("1");
        CompletableFuture<Settings> cfSettings = cfUser.thenCompose(user -> fetchSettingsForUser(user));

        System.out.println(cfUser.join().name() + "'s language is " + cfSettings.join().language());
    }
    static CompletableFuture<User> fetchUserById(String id) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            return new User("Malobika");
        });
    }

    static CompletableFuture<Settings> fetchSettingsForUser(User user) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            return new Settings("English");
        });
    }

    static void sleep(long millis) {
        try { Thread.sleep(millis); } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
    record Settings(String language) {}
```

> `thenCompose` flattens nested `CompletableFuture` ?

- ✅ Yes! That is the **core purpose** of `thenCompose`.

---

### 🔍 Let’s compare:

#### Without `thenCompose`:

```java
CompletableFuture<CompletableFuture<Settings>> nested =
    fetchUserById("1").thenApply(user -> fetchSettingsForUser(user));
```

* `thenApply` wraps the returned future → `CompletableFuture<CompletableFuture<Settings>>`

---

#### With `thenCompose`:

```java
CompletableFuture<Settings> flat =
    fetchUserById("1").thenCompose(user -> fetchSettingsForUser(user));
```

* `thenCompose` **flattens** the future.
* So you get a clean `CompletableFuture<Settings>`

---

### 🔁 Analogy (like flatMap vs map in streams):

```java
Stream<String> map = list.stream().map(str -> someFunc(str));          // Stream<Stream<T>>
Stream<String> flat = list.stream().flatMap(str -> someFunc(str));     // Stream<T>
```

Same idea here:

* `thenApply` → gives `CompletableFuture<CompletableFuture<T>>`
* `thenCompose` → gives `CompletableFuture<T>`

---

### 📌 Summary:

| Method            | Input Function Returns       | Result                               |
| ----------------- | ---------------------------- | ------------------------------------ |
| `thenApply(fn)`   | `T` → `U`                    | `CompletableFuture<U>`               |
| `thenCompose(fn)` | `T` → `CompletableFuture<U>` | `CompletableFuture<U>` ✅ (flattened) |

---

# Problem 3: When to use thenCompose() vs thenApply()?

### Solution

| Case                                           | Method          | Result Type                        |
| ---------------------------------------------- | --------------- | ---------------------------------- |
| Return a **normal value** from lambda          | `thenApply()`   | `CompletableFuture<U>`             |
| Return a **new CompletableFuture** from lambda | `thenCompose()` | `CompletableFuture<U>` (flattened) |

## 🔁 Practice Question

Rewrite the same logic using thenApply() instead of thenCompose(). What happens? Why is it wrong?

### Solution

```
public static void main(String[] args) throws ExecutionException, InterruptedException, TimeoutException {
        CompletableFuture<User> cfUser = fetchUserById("1");
        CompletableFuture<CompletableFuture<Settings>> cfSettings = cfUser.thenApply(user -> fetchSettingsForUser(user));

        System.out.println(cfUser.join().name() + "'s language is " + cfSettings.join().join().language());
    }
    static CompletableFuture<User> fetchUserById(String id) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            return new User("Malobika");
        });
    }

    static CompletableFuture<Settings> fetchSettingsForUser(User user) {
        return CompletableFuture.supplyAsync(() -> {
            sleep(1000);
            return new Settings("English");
        });
    }

    static void sleep(long millis) {
        try { Thread.sleep(millis); } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
    record Settings(String language) {}
```

