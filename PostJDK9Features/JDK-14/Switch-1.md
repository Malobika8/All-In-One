# ✅ Java 14 Feature: **Switch Expressions** (💯 Finalized in JDK 14)

This was a preview in Java 12 and 13 — now it’s **officially finalized** and ready for production.

---

## 🔹 What’s New?

### ✅ `switch` is now an **expression**, not just a statement.

That means:

* It can **return a value**
* You can use **arrow syntax (`->`)** for cleaner case blocks
* You can use **`yield`** to return multi-line blocks

---

## ✅ Example 1: Switch as an Expression

```java
int day = 2;

String result = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    default -> "Other day";
};

System.out.println(result); // "Tuesday"
```

---

## ✅ Example 2: Multi-line Case with `yield`

```java
int marks = 85;

String grade = switch (marks / 10) {
    case 10, 9 -> "A";
    case 8 -> "B";
    case 7 -> {
        System.out.println("Processing...");
        yield "C";
    }
    default -> "F";
};

System.out.println(grade);
```

---

## 🔥 Benefits Over Old `switch`:

| Old `switch` (statement)        | New `switch` (expression)           |
| ------------------------------- | ----------------------------------- |
| Verbose (`break`, fall-through) | Concise (`->`, no fall-through)     |
| No return value                 | Can return a value directly         |
| More error-prone                | Compile-time checked exhaustiveness |

---

Even though **switch expressions** are designed to return a value, you can still use them to **just perform actions like printing**, but the way you do it depends on whether you're using:

* A **traditional `switch` statement** (still supported)
* Or a **`switch` expression** (new in Java 14)

Let’s break it down.

## ✅ 1. If you only want to **perform side effects** (e.g., print), use **`switch` as a statement**, like before:

```java
int day = 2;

switch (day) {
    case 1 -> System.out.println("Monday");
    case 2 -> System.out.println("Tuesday");
    default -> System.out.println("Other day");
}
```

This is using **arrow syntax**, but the switch is not returning anything — just **executing code**.

✅ This is valid in Java 14+
✅ Still uses cleaner `->` syntax
❌ It's not an "expression", so no return value

---

## ✅ 2. If you're using a **`switch` expression**, but don't need the return value — just ignore it:

```java
int day = 2;

switch (day) {
    case 1 -> System.out.println("Monday");
    case 2 -> System.out.println("Tuesday");
    default -> System.out.println("Other day");
}
```

Looks the same — because **Java automatically detects** whether you are using switch as:

* a **statement** (if not assigned)
* or an **expression** (if assigned to a variable)

---

## ✅ Summary:

| Goal                 | How to do it                                    |
| -------------------- | ----------------------------------------------- |
| Just print/do action | Use `switch` as a **statement**                 |
| Return a value       | Use `switch` as an **expression** and assign it |
| Multi-line logic     | Use `{ ... yield value; }` for expressions      |

---

### 🧪 Final Example – Print based on score category

```java
int score = 80;

switch (score / 10) {
    case 10, 9 -> System.out.println("Excellent");
    case 8 -> System.out.println("Very Good");
    case 7 -> System.out.println("Good");
    default -> System.out.println("Needs Improvement");
}
```

---
