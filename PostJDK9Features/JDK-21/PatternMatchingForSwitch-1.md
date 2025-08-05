# ✅ Java 21 Final Feature: **Pattern Matching for `switch`**

---

## 🔹 What is it?

This enhancement allows you to:

* Use **types directly in `switch` cases**
* Combine it with **pattern matching and guards**
* Write **safer, cleaner, and more expressive `switch`** logic

---

## 🧠 Why it’s powerful

* Supports **type checking + casting** in one step
* Allows **null-safe** switching
* Works with **sealed classes** for exhaustive checking
* Replaces messy `if-else` chains

---

## ✅ Example 1: Pattern Matching with Types

```java
static String format(Object obj) {
    return switch (obj) {
        case Integer i -> "Integer: " + (i * 2);
        case String s -> "String: " + s.toUpperCase();
        case null     -> "It's null!";
        default       -> "Unknown type";
    };
}
```

### ✅ Explanation:

* `Integer i` → if it's an `Integer`, bind to `i`
* `String s` → binds and casts automatically
* `null` → safe to handle
* `default` → fallback for unmatched types

---

## ✅ Example 2: Add a Guard (`when` clause)

```java
static String describeNumber(Number n) {
    return switch (n) {
        case Integer i when i > 0 -> "Positive int";
        case Integer i            -> "Zero or negative int";
        case Double d when d.isNaN() -> "Not a number";
        case null                 -> "Null number";
        default                   -> "Some other number type";
    };
}
```

> ✅ `when` adds an extra condition
> ✅ Type + condition = clean and precise branching

---

## ✅ Example 3: With a Sealed Class Hierarchy

```java
sealed interface Shape permits Circle, Rectangle {}

record Circle(double radius) implements Shape {}
record Rectangle(double width, double height) implements Shape {}

static double area(Shape shape) {
    return switch (shape) {
        case Circle c    -> Math.PI * c.radius() * c.radius();
        case Rectangle r -> r.width() * r.height();
    };
}
```

> ✅ No `default` needed — compiler checks exhaustiveness thanks to `sealed`

---

## 🚀 Key Benefits:

| Feature                 | Benefit                          |
| ----------------------- | -------------------------------- |
| `case Type var`         | ✅ Automatic casting              |
| `case null`             | ✅ Null-safe switches             |
| `case Type t when cond` | ✅ Add guards (conditional cases) |
| Sealed class support    | ✅ Exhaustiveness check           |
| No fall-through         | ✅ Safer than traditional switch  |

---
