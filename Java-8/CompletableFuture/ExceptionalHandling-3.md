# Intro
## ✅ PART 1: `exceptionally`

### 🔹 Purpose:

Provide a **fallback result** when something goes wrong.

### 🔧 Syntax:

```java
future.exceptionally(ex -> {
    System.out.println("Something went wrong: " + ex);
    return fallbackValue;
});
```

---

### ✅ Example:

```java
public class Main {
    public static void main(String[] args) {
        CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
            if (true) throw new RuntimeException("DB error");
            return "Success!";
        });

        String result = future
            .exceptionally(ex -> {
                System.out.println("Caught: " + ex);
                return "Fallback result";
            })
            .join();

        System.out.println("Result = " + result);
    }
}
```

### 🧾 Output:

```
Caught: java.lang.RuntimeException: DB error
Result = Fallback result
```

---

## ✅ PART 2: `handle`

### 🔹 Purpose:

Handle both **success and failure** in the same place.

### 🔧 Syntax:

```java
future.handle((result, exception) -> {
    if (exception != null) {
        return "fallback";
    } else {
        return result + " modified";
    }
});
```

---

### ✅ Example:

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    if (true) throw new RuntimeException("API failed");
    return "Success!";
});

String result = future.handle((res, ex) -> {
    if (ex != null) {
        System.out.println("Handled: " + ex);
        return "Handled fallback";
    }
    return res;
}).join();

System.out.println("Result = " + result);
```

---

## ✅ PART 3: `whenComplete`

### 🔹 Purpose:

Just **observe the result** (success or failure), like logging, without modifying anything.

### 🔧 Syntax:

```java
future.whenComplete((res, ex) -> {
    if (ex != null) log(ex);
    else log(res);
});
```

---

### ✅ Example:

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> "Hello")
    .whenComplete((res, ex) -> {
        if (ex != null)
            System.out.println("Failed with: " + ex);
        else
            System.out.println("Completed with: " + res);
    });

System.out.println("Result = " + future.join());
```

---

## 🧠 Summary Table

| Method          | Handles Error? | Modifies Result? | Use Case                |
| --------------- | -------------- | ---------------- | ----------------------- |
| `exceptionally` | ✅ Yes          | ✅ Yes            | Provide fallback result |
| `handle`        | ✅ Yes          | ✅ Yes            | Unified success/failure |
| `whenComplete`  | ✅ Yes          | ❌ No             | Just log or audit       |

---

# Difference
## 🔍 `whenComplete` vs `exceptionally` vs `handle`

### ✅ 1. `whenComplete`

* **Observation only** — you can log the exception, but **you can't replace the result**.
* The exception is **still propagated** if you call `.join()` or `.get()` afterward.
* Think of it like a **side-effect hook**.

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    throw new RuntimeException("boom");
}).whenComplete((res, ex) -> {
    System.out.println("In whenComplete");
    if (ex != null) System.out.println("Caught in whenComplete: " + ex);
});

future.join();  // ❌ Throws RuntimeException here!
```

> ✅ **So yes — `join()` will still throw the error.**

---

### ✅ 2. `exceptionally`

* Used to **recover from failure**.
* If an exception occurs, it runs your function and **returns a fallback value**.
* It **consumes** the exception — `.join()` will **not throw**.

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    throw new RuntimeException("boom");
}).exceptionally(ex -> {
    System.out.println("Handled in exceptionally");
    return "Recovered";
});

System.out.println("Result: " + future.join());  // ✅ No exception, prints "Recovered"
```

---

### ✅ 3. `handle`

* Similar to `exceptionally` but handles **both success and failure**.
* You can return an alternative or transform the result.
* It also **consumes** the exception.

```java
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    throw new RuntimeException("boom");
}).handle((res, ex) -> {
    if (ex != null) {
        System.out.println("Handled in handle");
        return "Handled fallback";
    }
    return res;
});

System.out.println("Result: " + future.join());  // ✅ No exception, prints "Handled fallback"
```

---

## ✅ Summary Table

| Feature         | Handles Success | Handles Failure | Can Replace Value | Consumes Exception  |
| --------------- | --------------- | --------------- | ----------------- | ------------------- |
| `whenComplete`  | ✅ Yes           | ✅ Yes           | ❌ No              | ❌ No (still throws) |
| `exceptionally` | ❌ No            | ✅ Yes           | ✅ Yes             | ✅ Yes               |
| `handle`        | ✅ Yes           | ✅ Yes           | ✅ Yes             | ✅ Yes               |

---

