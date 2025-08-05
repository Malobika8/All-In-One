# ✅ Java 22 Final Feature: **Unnamed Patterns and Variables (`_`)**

---

## 🔹 What is it?

In Java 22, you can now use `_` as an **unnamed pattern** or **unnamed variable** when:

* You **don’t care about the value**
* You **don’t want to create a variable**

---

### ✅ Example 1: Ignore a value in a pattern

```java
record Point(int x, int y) {}

Object obj = new Point(5, 10);

if (obj instanceof Point(int x, _)) {
    System.out.println("X = " + x); // Ignores y completely
}
```

* `_` tells the compiler: “I don’t care about this value”
* No variable created for `y`
* Cleaner, avoids unused variable warnings

---

### ✅ Example 2: Ignore both values

```java
if (obj instanceof Point(_, _)) {
    System.out.println("It's some Point");
}
```

* Just checking type, no need for values at all

---

### ✅ Example 3: Ignore record field in `switch`

```java
static String check(Object obj) {
    return switch (obj) {
        case Point(_, int y) when y > 0 -> "Positive Y";
        case Point(_, _) -> "Some point";
        default -> "Unknown";
    };
}
```

---

## ✅ Example 4: Ignore method parameter (unnamed variable)

```java
void logUserActivity(String username, long _) {
    System.out.println("User: " + username);
}
```

* Ignores second parameter (e.g., timestamp)
* No variable created for `_`

---

## ✅ Why It’s Useful

| Use Case                 | Why `_` Helps                      |
| ------------------------ | ---------------------------------- |
| Unused method parameters | Avoids naming unused args          |
| Record patterns          | Deconstruct only what you need     |
| Switch with record match | Ignore unwanted fields cleanly     |
| Avoid warnings           | No “variable is never used” errors |

---

## 🧠 Summary

| Feature            | Benefit                        |
| ------------------ | ------------------------------ |
| `_` in patterns    | ✅ Ignore field during matching |
| `_` in method args | ✅ Skip unused parameters       |
| Cleaner code       | ✅ Reduces boilerplate          |
| Final in Java 22   | ✅ Not a preview feature        |

---

