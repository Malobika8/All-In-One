# ✅ JDK 16 — Most Important Finalized Feature: **Records**

---

## 🔹 What is a Record?

A **record** is a special Java class meant to be:

* **Immutable**
* **Concise**
* Used mainly to hold **data**

It automatically provides:

* `private final` fields
* Constructor
* `getters` (without the `get` prefix)
* `equals()`, `hashCode()`, and `toString()`
  → all generated for you!

---

### 🔸 Before Java 16 (Verbose POJO):

```java
public class Person {
    private final String name;
    private final int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String name() { return name; }
    public int age() { return age; }

    @Override public boolean equals(Object o) { ... }
    @Override public int hashCode() { ... }
    @Override public String toString() { ... }
}
```

---

### ✅ Java 16 — Records:

```java
public record Person(String name, int age) {}
```

That’s it. Done. 🎉

---

### ✅ How to use:

```java
Person p = new Person("John", 30);

System.out.println(p.name());  // John
System.out.println(p.age());   // 30
System.out.println(p);         // Person[name=John, age=30]
```

---

## ✅ Features of Records:

| Feature                   | Record Does It? | Notes                 |
| ------------------------- | --------------- | --------------------- |
| Constructor               | ✅               | Auto-generated        |
| Getters (like `name()`)   | ✅               | Named like fields     |
| `equals()` / `hashCode()` | ✅               | Based on field values |
| `toString()`              | ✅               | Clean format          |
| `final` fields            | ✅               | Immutable by default  |

---

### ✅ Common Use Cases:

* DTOs (Data Transfer Objects)
* Response objects (REST)
* Value types (Key-Value pairs, config, etc.)
* Return multiple values from a method

---

## ✅ Limitations:

| Limitation             | Why?                          |
| ---------------------- | ----------------------------- |
| Can't extend classes   | Records are `final`           |
| All fields are `final` | Immutability enforced         |
| No custom setters      | You can’t change field values |

You **can**:

* Add custom methods
* Add static fields/methods
* Do validation in compact constructors

---

### ✅ Compact Constructor Example:

```java
public record Person(String name, int age) {
    public Person {
        if (age < 0) throw new IllegalArgumentException("Age can't be negative");
    }
}
```

---

## 🧠 Summary

| Feature   | Benefit                              |
| --------- | ------------------------------------ |
| `record`  | Reduces boilerplate for data classes |
| Finalized | ✅ Yes, in JDK 16                     |
| Interview | ✅ Common in modern Java questions    |
| Usage     | DTOs, responses, small value objects |

---

# ✅ Part 1: Practical Examples of Records

---

## 🔹 A. Value Type: Key-Value Pair or Config Object

```java
public record Config(String key, String value) {}

Config config = new Config("timeout", "30s");
System.out.println(config.key());    // timeout
System.out.println(config.value());  // 30s
```

> Great for small, immutable data like environment config, headers, key-value pairs, etc.

---

## 🔹 B. Returning Multiple Values from a Method

Let’s say you want to return **both sum and average** from a method.

### ✅ Step 1: Define a `record`

```java
public record Stats(int sum, double average) {}
```

### ✅ Step 2: Return it from a method

```java
public class Calculator {
    public static Stats calculate(int[] nums) {
        int sum = Arrays.stream(nums).sum();
        double avg = Arrays.stream(nums).average().orElse(0);
        return new Stats(sum, avg);
    }
}
```

### ✅ Usage:

```java
Stats stats = Calculator.calculate(new int[]{10, 20, 30});
System.out.println(stats.sum());     // 60
System.out.println(stats.average()); // 20.0
```

> 🔥 Cleaner than returning a Map or Object\[], and safer than returning nulls or side effects.

---

# ✅ Part 2: Custom Methods, Static Fields/Methods, Validation

---

## 🔹 A. Add Custom Methods

```java
public record Rectangle(int length, int width) {
    public int area() {
        return length * width;
    }
}
```

✅ Usage:

```java
Rectangle r = new Rectangle(5, 3);
System.out.println(r.area()); // 15
```

---

## 🔹 B. Add Static Fields or Methods

```java
public record MathConstants(double pi) {
    public static final MathConstants DEFAULT = new MathConstants(Math.PI);

    public static MathConstants halfPi() {
        return new MathConstants(Math.PI / 2);
    }
}
```

✅ Usage:

```java
System.out.println(MathConstants.DEFAULT.pi());     // 3.1415...
System.out.println(MathConstants.halfPi().pi());    // 1.5707...
```

---

## 🔹 C. Validation with Compact Constructor

```java
public record User(String name, int age) {
    public User {
        if (name == null || name.isBlank())
            throw new IllegalArgumentException("Name cannot be blank");
        if (age < 0)
            throw new IllegalArgumentException("Age cannot be negative");
    }
}
```

✅ Usage:

```java
User u = new User("Alice", 25);     // OK
User invalid = new User("", -5);    // ❌ Throws IllegalArgumentException
```

---

# ✅ Part 3: Why are Records Immutable?

### 🔒 Key Reason: **Design goal is to model data as values, not objects with behavior**

## ✅ Record = Final Data Structure

| Feature                | Explanation                              |
| ---------------------- | ---------------------------------------- |
| `final class`          | You can't extend it                      |
| `private final` fields | Compiler generates them for you          |
| No setters             | You can’t reassign fields after creation |

```java
public record Person(String name, int age) {}

// Under the hood → like this:
final class Person {
    private final String name;
    private final int age;
    // + constructor, accessors, etc.
}
```

### 🚫 You can’t do:

```java
person.age = 30;  // ❌ Not allowed
```

---

## ✅ Why make them immutable?

* 🔐 **Thread-safe by default**
* 🚫 Prevents accidental mutation
* 🧠 Encourages functional, predictable code
* ✅ Ideal for DTOs, APIs, serialization

---

### 🧠 Think of `record` like a better, built-in:

* DTO (Data Transfer Object)
* Lombok `@Data` class (but cleaner, safer)
* Kotlin `data class`

---

### ✅ Why Records Are Immutable

1. **Purpose**:
   Records are designed to represent **data as a value** — just like:

   * A `Point(x, y)`
   * A `Name(first, last)`
   * A `Response(status, message)`

   👉 These things **should not change once created**. They are fixed facts.

2. **Language-level immutability**:

   * Fields are automatically `private final`
   * No setters allowed
   * You can’t override field access (unless you do hacks)

3. **Benefits of immutability**:

   * Thread-safety
   * Safer code (no side effects)
   * Ideal for:

     * DTOs
     * REST APIs
     * Database rows
     * Caching
     * Return values

