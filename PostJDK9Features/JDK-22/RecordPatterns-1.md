# ✅ Java 22 Final Feature: **Record Patterns**

---

## 🔹 What is a Record Pattern?

A **record pattern** lets you:

* **Deconstruct a record** directly into its fields
* **Extract field values** during `instanceof` or `switch`
* Avoid manual getters, casting, or boilerplate

---

## ✅ Example 1: Deconstruct a record

### Record definition:

```java
public record Point(int x, int y) {}
```

### Traditional way (Java 16+):

```java
if (obj instanceof Point p) {
    System.out.println(p.x() + ", " + p.y());
}
```

---

### ✅ With Record Pattern (Java 22):

```java
if (obj instanceof Point(int x, int y)) {
    System.out.println(x + ", " + y);  // 🚀 Clean access, no getters!
}
```

> You **deconstruct** the record directly in the pattern!
> No need to call `.x()` and `.y()`.

---

## ✅ Example 2: Record Pattern in `switch`

```java
static String printPoint(Object obj) {
    return switch (obj) {
        case Point(int x, int y) -> "X = " + x + ", Y = " + y;
        case null                -> "null";
        default                  -> "Not a point";
    };
}
```

* ✅ If `obj` is a `Point`, it’s deconstructed and matched
* ✅ If not, goes to default

---

## ✅ Example 3: Nesting with Record Patterns

```java
public record Address(String city, String country) {}
public record Person(String name, int age, Address address) {}
```

Now:

```java
static String describePerson(Object obj) {
    return switch (obj) {
        case Person(String name, int age, Address(String city, String country))
            -> name + " (" + age + ") lives in " + city + ", " + country;
        default -> "Unknown";
    };
}
```

> ✅ You can deconstruct **nested records** inline
> Super expressive!

---

## 🔐 Requirements for Record Patterns

| Requirement                       | Explanation                      |
| --------------------------------- | -------------------------------- |
| Must be a `record`                | Only works with `record` types   |
| Field types must match            | Compiler enforces field matching |
| Works with `instanceof`, `switch` | Both supported                   |

---

## ✅ When to Use Record Patterns

| Use Case                           | Why It’s Better                             |
| ---------------------------------- | ------------------------------------------- |
| REST APIs (e.g., request/response) | Deconstruct body directly                   |
| Domain models                      | Cleanly extract values                      |
| Switch logic on value objects      | Exhaustive, readable, pattern-based control |
| Combine with sealed classes        | Exhaustive pattern matching                 |

---

## 🧠 Summary

| Feature               | Benefit                                |
| --------------------- | -------------------------------------- |
| Record patterns       | ✅ Deconstruct data without boilerplate |
| Works in `switch`     | ✅ Clean pattern-based flow             |
| Works in `instanceof` | ✅ No casting or accessors needed       |
| Nesting supported     | ✅ Deconstruct complex structures       |

---

