## 🔒 Java 9: **Private Methods in Interfaces**

---

### 🧠 Why was this needed?

In Java 8, interfaces could have:

* `abstract` methods (default from earlier versions)
* `default` methods
* `static` methods

But sometimes, **default or static methods share common logic**.
Before Java 9, you had to **repeat code** or **move it to a utility class**.

👉 Java 9 lets you write **private methods** inside interfaces to reuse logic **internally**.

---

### ✅ Syntax:

```java
public interface MyInterface {
    
    default void show() {
        log("Inside show");
    }

    default void display() {
        log("Inside display");
    }

    private void log(String msg) {
        System.out.println(msg);
    }
}
```

🧩 `log()` is a private helper method. It's **not visible outside** the interface.

---

### 📌 Rules:

| Rule                                    | Explanation                                                              |
| --------------------------------------- | ------------------------------------------------------------------------ |
| ✅ Allowed in interfaces                 | Since Java 9 only                                                        |
| ❌ Cannot be abstract                    | Only method body is allowed                                              |
| ✅ Can be `private` or `private static`  | Use `private` in default methods, and `private static` in static methods |
| ❌ Cannot override in implementing class | It's hidden from classes implementing the interface                      |

---

### 🧪 Question

You have an interface `LoggerService` with two default methods: `logInfo()` and `logError()`.
Both should internally call a private method `writeLog(String msg)`.

```java
public interface LoggerService {

    default void logInfo() {
        writeLog("Inside logInfo");
    }

    default void logError() {
        writeLog("Inside logError");
    }

    private void writeLog(String msg) {
        System.out.println(msg);
    }
}
```

---

### Bonus: If you wanted to call it from a static method, you'd define:

```java
private static void writeLog(String msg) {
    System.out.println(msg);
}
```

And call it from a `static` method like:

```java
static void logStatic() {
    writeLog("Inside static log");
}
```

---


