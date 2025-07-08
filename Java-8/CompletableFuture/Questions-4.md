# **Question 1: `exceptionally`**

### 🔧 Task:

* Simulate a failure in a method (like `fetchUserById`)
* Use `exceptionally` to recover with a fallback user
* Print the name

---

### 🧩 Starter Code (Fill it in):

```java
public class Main {
    public static void main(String[] args) {
        CompletableFuture<User> future = CompletableFuture.supplyAsync(() -> fetchUserById("1"))
            // TODO: use exceptionally to handle failure
            ;

        System.out.println("Result: " + future.join().name());
    }

    static User fetchUserById(String id) {
        sleep(1000);
        if (true) throw new RuntimeException("User not found");
        return new User("Malobika");
    }

    static void sleep(long millis) {
        try { Thread.sleep(millis); } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
}
```

### 🧠 Goal:

* If exception happens, return `new User("FallbackUser")`
* So output should be:
  `Result: FallbackUser`

---

### Solution

```
public static void main(String[] args) throws ExecutionException, InterruptedException, TimeoutException {
        CompletableFuture<User> future = CompletableFuture.supplyAsync(() -> fetchUserById("1"))
                .exceptionally(ex -> {
                    System.out.println("Exception: " + ex.getMessage());
                    return new User("Fallback User");
                });

        System.out.println("User: " + future.join());
    }

    static User fetchUserById(String id) {
        sleep(1000);
        if (true) throw new RuntimeException("User not found");
        return new User("Malobika");
    }

    static void sleep(long millis) {
        try {
            Thread.sleep(millis);
        } catch (InterruptedException ignored) {
        }
    }

    record User(String name) {
    }
```

# **Question 2: `handle`**

### 🔹 Purpose:

`handle()` lets you deal with **both**:

* ✅ **Success** → access the result
* ❌ **Failure** → handle the exception

You can return a final value in both cases.

---

### 🎯 Task:

* Simulate an error in `fetchUserById()`
* Use `.handle(...)` to:

  * If success: return `"User is <name>"`
  * If failure: return `"Recovered from error"`

---

### 🧩 Starter Code:

```java
public class Main {
    public static void main(String[] args) {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> fetchUserById("1"))
            .handle((user, ex) -> {
                // TODO: handle both success and exception
                return null;
            });

        System.out.println("Result: " + future.join());
    }

    static User fetchUserById(String id) {
        sleep(1000);
        if (true) throw new RuntimeException("User not found");
        return new User("Malobika");
    }

    static void sleep(long millis) {
        try {
            Thread.sleep(millis);
        } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
}
```

---

### ✅ Expected Output:

```
Result: Recovered from error
```

But if there's no error, it should say:

```
Result: User is Malobika
```

### Solution

```
public static void main(String[] args) throws ExecutionException, InterruptedException, TimeoutException {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> fetchUserById("1"))
                .handle((result, ex) -> {
                    if(ex != null){
                        return "Result: Recovered from error";
                    }
                    else{
                        return "Result: User is " + result.name();
                    }
                });

        System.out.println(future.join());
    }

    static User fetchUserById(String id) {
        sleep(1000);
        if (true) throw new RuntimeException("User not found");
        return new User("Malobika");
    }

    static void sleep(long millis) {
        try {
            Thread.sleep(millis);
        } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
```

# **Question 3: `whenComplete`**

### 🔹 Purpose:

* Runs **after** a `CompletableFuture` completes
* Lets you **observe** both success and failure
* ❗ **Does not change** the result or handle the error

---

### 🎯 Task:

* Simulate an exception in `fetchUserById()`
* Use `whenComplete()` to:

  * Log success (`User fetched: <name>`)
  * Log error (`Error occurred: <message>`)
* Still call `.join()` — and notice that the exception is **not handled**

---

### 🧩 Starter Code:

```java
public class Main {
    public static void main(String[] args) {
        CompletableFuture<User> future = CompletableFuture.supplyAsync(() -> fetchUserById("1"))
            .whenComplete((user, ex) -> {
                // TODO: log success or failure
            });

        System.out.println("Result: " + future.join());
    }

    static User fetchUserById(String id) {
        sleep(1000);
        if (true) throw new RuntimeException("User not found");
        return new User("Malobika");
    }

    static void sleep(long millis) {
        try {
            Thread.sleep(millis);
        } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
}
```

---

### ✅ Your Goal:

* Log the error inside `whenComplete`
* Observe that `.join()` still throws the exception — unlike `handle` or `exceptionally`

---

### Solution

```
public static void main(String[] args) throws ExecutionException, InterruptedException, TimeoutException {
        CompletableFuture<User> future = CompletableFuture.supplyAsync(() -> fetchUserById("1"))
                .whenComplete((result, ex) -> {
                    if(ex != null){
                        System.out.println("Error occurred: " + ex.getMessage());
                    }
                    else{
                        System.out.println("User fetched: " + result.name());
                    }
                });

        System.out.println(future.join());
    }

    static User fetchUserById(String id) {
        sleep(1000);
        if (true) throw new RuntimeException("User not found");
        return new User("Malobika");
    }

    static void sleep(long millis) {
        try {
            Thread.sleep(millis);
        } catch (InterruptedException ignored) {}
    }

    record User(String name) {}
```

# FYI
## ✅ Final Comparison Cheat Sheet

| Feature         | Handles Success | Handles Exception | Can Modify Result | Consumes Exception |
| --------------- | --------------- | ----------------- | ----------------- | ------------------ |
| `exceptionally` | ❌ No            | ✅ Yes             | ✅ Yes             | ✅ Yes              |
| `handle`        | ✅ Yes           | ✅ Yes             | ✅ Yes             | ✅ Yes              |
| `whenComplete`  | ✅ Yes           | ✅ Yes             | ❌ No              | ❌ No               |

---

## ✅ **What Can Be Returned in `exceptionally`, `handle`, and `whenComplete`**

| Method          | Purpose                                      | Return Value Type                                                 | Can Change Type? | Notes                                                       |
| --------------- | -------------------------------------------- | ----------------------------------------------------------------- | ---------------- | ----------------------------------------------------------- |
| `exceptionally` | Handle only **exceptions**                   | Must return the **same type** as the original `CompletableFuture` | ❌ No             | Used for error recovery. Cannot access the success result.  |
| `handle`        | Handle **both success & error**              | Can return a **different type** (transforms the result)           | ✅ Yes            | Think of it as `try-catch + map` in one step.               |
| `whenComplete`  | Just **observe** result or error (log/audit) | Must return `void` (you return nothing)                           | ❌ No             | Does **not change or replace** the result. It just watches. |

---

### 🔧 Detailed Breakdown:

#### ✅ `exceptionally(ex -> fallbackValue)`

* Use only for **errors**.
* Return a fallback of the **same type**.
* Example:

  ```java
  CompletableFuture<User> future = ... 
      .exceptionally(ex -> new User("Fallback"));  // Must return User
  ```

---

#### ✅ `handle((result, ex) -> transformedValue)`

* Handles both **success and error**
* Can return **any type you want**
* Example:

  ```java
  CompletableFuture<String> future = ... // original returns User
      .handle((user, ex) -> {
          if (ex != null) return "Recovered from error";
          else return "User is " + user.name();  // Returns String
      });
  ```

---

#### ✅ `whenComplete((result, ex) -> { side-effect })`

* Does **not** change or replace the result
* Only used for **logging or final actions**
* Return type must be `void`
* Exception is **not consumed**
* Example:

  ```java
  CompletableFuture<User> future = ...
      .whenComplete((user, ex) -> {
          if (ex != null) System.out.println("Failed");
          else System.out.println("Fetched: " + user.name());
      });
  ```

---

## ✅ Quick Summary for Your Notes

```java
// ✅ exceptionally: only on error, must return same type
CompletableFuture<T> = ...exceptionally(ex -> T);

// ✅ handle: on success or error, can return different type
CompletableFuture<R> = ...handle((T result, Throwable ex) -> R);

// ✅ whenComplete: only side-effects (log etc.), doesn't change result
CompletableFuture<T> = ...whenComplete((T result, Throwable ex) -> void);
```

---

