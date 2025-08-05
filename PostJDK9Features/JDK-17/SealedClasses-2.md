# ✅ Java 17 Feature: **Sealed Classes** (💯 Finalized)

---

## 🔹 What are Sealed Classes?

A **sealed class** is a class (or interface) that **restricts which other classes can extend or implement it**.

### 🔐 Why?

* To enforce **strict control over inheritance**
* To make your design more **secure, explicit, and predictable**
* Useful in **domain modeling**, especially with pattern matching

---

### ✅ Syntax:

```java
public sealed class Shape
    permits Circle, Rectangle {}
```

Then, the permitted classes must be:

```java
public final class Circle extends Shape {}
public final class Rectangle extends Shape {}
```

---

## ✅ Use Case Example

### 🔸 Model a closed set of types:

```java
public sealed class Shape permits Circle, Rectangle {}

public final class Circle extends Shape {
    double radius;
}

public final class Rectangle extends Shape {
    double width, height;
}
```

Now:

* No other class can extend `Shape` unless it's listed in `permits`
* The compiler enforces this
* You can **safely use pattern matching** and **switch expressions** knowing all possible types

---

## ✅ Benefits of Sealed Classes:

| Benefit                           | Why it matters                     |
| --------------------------------- | ---------------------------------- |
| Controlled inheritance            | Only allowed subclasses can extend |
| Works with pattern matching       | Enables exhaustiveness checking    |
| Safer than open inheritance       | Prevents misuse of APIs            |
| Good for modeling algebraic types | Useful in business/domain logic    |

---

## ✅ Keywords You Can Use:

A class extending a sealed class must be one of:

| Modifier     | Meaning                         |
| ------------ | ------------------------------- |
| `final`      | Cannot be extended further      |
| `sealed`     | Can define its own permits list |
| `non-sealed` | Can be extended by anyone       |

---

## 🧠 Example with All Three

```java
public sealed class Animal permits Dog, Cat, Other {}

public final class Dog extends Animal {}
public final class Cat extends Animal {}
public non-sealed class Other extends Animal {}  // ✅ open to extension
```

---

## 🧠 Why use sealed classes?

Imagine a domain where you only want a few well-defined subtypes:

* PaymentMethod: `CreditCard`, `PayPal`, `UPI`
* Shape: `Circle`, `Rectangle`, `Square`
* Command: `StartCommand`, `StopCommand`

> ✅ Sealed classes make your type hierarchy **closed and safe**.

---

## ✅ 1. Are `Dog` and `Cat` sealed by default?

> ❌ No, they are **not sealed by default**.

### In a sealed class hierarchy, the **direct subclasses** must be:

* Marked as `final`, `sealed`, or `non-sealed`

Let’s revisit the example:

```java
public sealed class Animal permits Dog, Cat, Mouse {}

public final class Dog extends Animal {}          // ✅ allowed
public sealed class Cat extends Animal {}         // ✅ allowed
public non-sealed class Mouse extends Animal {}   // ✅ allowed

// ❌ NOT allowed:
public class Bear extends Animal {}               // ❌ Must declare `final`, `sealed`, or `non-sealed`
```

### 🧠 Why is this required?

Because Java wants you to **explicitly declare** the **intent** of each subclass:

* Is it final? (no one else can extend it)
* Is it sealed? (continue sealing the hierarchy)
* Is it non-sealed? (open up for extension)

This ensures **full control** over the inheritance tree.

---

## ✅ Recap — Key Rules for Sealed Classes:

| Rule                                                             | Explanation                      |
| ---------------------------------------------------------------- | -------------------------------- |
| Sealed class must list all allowed subclasses                    | `permits Dog, Cat`               |
| All subclasses must be in the **same package or file**           | Required for compiler visibility |
| Each subclass must be marked: `final`, `sealed`, or `non-sealed` | Enforced by compiler             |
| No other class may extend the sealed class                       | ✅ Compiler prevents it           |

---

## ✅ What if permitted subclasses are in a **different package**?

### 🔒 **By default, that’s NOT allowed**.

Java’s sealed classes **require that:**

> **All permitted subclasses must be either:**
>
> * In the **same package**, or
> * Declared in the **same source file** as the sealed class

---

## ❌ So this is illegal:

```java
// In package: animals.base
package animals.base;

public sealed class Animal permits animals.types.Dog {}
```

```java
// In package: animals.types
package animals.types;

public final class Dog extends animals.base.Animal {}
```

✅ Even though `Dog` is in the `permits` list, this will cause a **compilation error**:

```
class Dog is not allowed to extend sealed class Animal
```

---

## ✅ How to fix it:

### You must ensure **both**:

1. The subclass is in the **same package** as the sealed class
2. The subclass is listed in the `permits` clause

---

### OR ✅ You can declare all classes in the **same `.java` file**:

```java
// Animal.java
public sealed class Animal permits Dog, Cat {}

final class Dog extends Animal {}
final class Cat extends Animal {}
```

Even though they're not public, this works because:

* They're in the **same source file**
* They're listed in `permits`

---

## 🧠 Why does Java restrict this?

Because:

* The compiler must be able to **see and validate** that all permitted subclasses:

  * Exist
  * Extend the sealed class
  * Declare themselves as `final`, `sealed`, or `non-sealed`

That’s **only possible if they’re in the same package or file** — otherwise Java can’t guarantee the hierarchy is enforced.

---

## ✅ Summary:

| Rule                                                       | Required? | Notes                                  |
| ---------------------------------------------------------- | --------- | -------------------------------------- |
| Subclasses must be in `permits` list                       | ✅ Yes     | Or compilation fails                   |
| Subclasses must be in **same package** or **same file**    | ✅ Yes     | Or compiler can’t verify the hierarchy |
| Subclasses must declare `final`, `sealed`, or `non-sealed` | ✅ Yes     | No implicit defaults                   |

---
