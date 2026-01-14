# Q11. Can we override a private method? Can we override a static method? Explain why.

### ❌ Can we override a `private` method?

**NO. We cannot override a private method.**

### Why?

* `private` methods are **NOT inherited**
* If a method is not inherited, it **cannot be overridden**

What happens instead?

```java
class A {
    private void show() {}
}

class B extends A {
    private void show() {} // ❌ NOT overriding
}
```

👉 This is a **completely new method**, unrelated to `A.show()`.

> “Private methods cannot be overridden because they are not inherited.”

## ❌ Can we override a `static` method?

**NO. Static methods cannot be overridden either.**

### What actually happens?

This is called **method hiding**, not overriding.

```java
class A {
    static void display() {}
}

class B extends A {
    static void display() {} // method hiding
}
```

* Method selection is based on **reference type**
* No runtime polymorphism

```java
A obj = new B();
obj.display(); // calls A.display()
```

| Method Type        | Can Override? | Why                                          |
| ------------------ | ------------- | -------------------------------------------- |
| `private`          | ❌ No          | Not inherited                                |
| `static`           | ❌ No          | Belongs to class, not object (method hiding) |
| `final`            | ❌ No          | Prevents modification                        |
| `public/protected` | ✅ Yes         | Proper inheritance                           |

> “Private methods cannot be overridden because they are not inherited.
> Static methods also cannot be overridden; they are hidden, since method resolution is done at compile time based on reference type.”

---

# Q12. What is the difference between `final`, `finally`, and `finalize()`?

### `final`

* Used with **variables, methods, and classes**
* Meaning:

  * **final variable** → value cannot be changed
  * **final method** → cannot be overridden
  * **final class** → cannot be extended

Example:

```java
final int x = 10;
final class Immutable {}
```
### `finally`

* Used with `try–catch`
* Code inside `finally`:

  * **Always executes**, whether exception occurs or not
  * Used for **cleanup logic** (closing DB connections, streams)

⚠️ Minor exception:

* `finally` may not execute if:

  * JVM crashes
  * `System.exit()` is called

Example:

```java
try {
    // risky code
} finally {
    // cleanup
}
```

### `finalize()`

* A method of `Object` class
* Called by **Garbage Collector** before object destruction
* Used earlier for resource cleanup

⚠️ Important (Modern Java):

* **Deprecated since Java 9**
* **Unreliable**
* Should NOT be used
* Replaced by:

  * `try-with-resources`
  * Explicit `close()` methods

> “`final` prevents modification, `finally` ensures cleanup, and `finalize()` was a GC hook that is now deprecated and should be avoided.”

---

# Q13. Can `finally` block execute without a `catch` block?

A finally block can exist without a catch, but it must be associated with a try block.

---

# Q14. What is the order of execution of constructors and instance blocks in Java inheritance?

Example:

```java
class A {
    A() {
        System.out.println("A constructor");
    }
}

class B extends A {
    B() {
        System.out.println("B constructor");
    }
}
```

**What will be printed when we do:**

```java
new B();
```

Execution Flow for new B()

- Memory allocated for B
- B() constructor starts
- Implicit super() call
- A() constructor executes
- Control returns to B() constructor
- B() constructor executes

In Java, parent constructors are always executed before child constructors, and super() is implicitly added if not explicitly written.

---

# Q15. What if parent has no default constructor?

Then the child must explicitly call a parameterized super(...), or compilation fails.

---

# Q16. What is the order of execution of: Static blocks, Instance initializer blocks, Constructors. Explain the order clearly.

1️⃣ **Static blocks**
2️⃣ **Instance initializer blocks**
3️⃣ **Constructors**

## Why this order?

### 1️⃣ Static blocks

* Executed **once**
* When the class is **loaded into JVM**
* Before any object is created

```java
static {
    System.out.println("static");
}
```

### 2️⃣ Instance initializer blocks

* Executed **every time an object is created**
* Executed **before the constructor**
* Used for common initialization logic

```java
{
    System.out.println("instance block");
}
```

### 3️⃣ Constructors

* Executed after instance blocks
* Used for object-specific initialization

```java
Constructor() {
    System.out.println("constructor");
}
```

## Example

```java
class Test {
    static {
        System.out.println("static");
    }

    {
        System.out.println("instance block");
    }

    Test() {
        System.out.println("constructor");
    }
}
```

Output:

```
static
instance block
constructor
```

> “Static blocks execute at class loading time, instance initializer blocks execute before constructors during object creation.”

---

# Q17. Are instance initializer blocks inherited? Will they execute in parent–child inheritance? Explain briefly.

### Are instance initializer blocks inherited?

No, they are not inherited.

* Just like constructors, instance initializer blocks **belong to the class itself**
* They are **not inherited** by child classes

### Will they execute in parent–child inheritance?

Yes, they do execute — but only for their own class.

### Explanation

When you create a child object:

1. Parent class **instance initializer block executes**
2. Parent constructor executes
3. Child class **instance initializer block executes**
4. Child constructor executes

## Example

```java
class Parent {
    {
        System.out.println("Parent instance block");
    }

    Parent() {
        System.out.println("Parent constructor");
    }
}

class Child extends Parent {
    {
        System.out.println("Child instance block");
    }

    Child() {
        System.out.println("Child constructor");
    }
}
```

```java
new Child();
```

Output:

```
Parent instance block
Parent constructor
Child instance block
Child constructor
```

Instance initializer blocks are not inherited, but they do execute as part of object creation for each class in the inheritance hierarchy.


---

# Q18. What is immutability in Java? How do you create an immutable class?

## What is Immutability?

> **Immutability means that once an object is created, its state cannot be changed.**
> Any modification results in the creation of a **new object**.

Example:

```java
String s = "abc";
s = s.concat("d"); // new object created
```

## Why Immutability is Important

* Thread-safe by default
* Safer for caching
* Predictable behavior
* Used heavily in:

  * `String`
  * Wrapper classes
  * `LocalDate`, `LocalTime`

## Rules to Create an Immutable Class

To make a class immutable:

1️⃣ **Make the class `final`**
→ Prevent subclassing

2️⃣ **Make all fields `private` and `final`**

3️⃣ **Do not provide setters**

4️⃣ **Initialize fields only via constructor**

5️⃣ **For mutable fields, return defensive copies**

## Immutable Class Example

```java
final class Employee {

    private final int id;
    private final String name;
    private final List<String> skills;

    public Employee(int id, String name, List<String> skills) {
        this.id = id;
        this.name = name;
        this.skills = new ArrayList<>(skills); // defensive copy
    }

    public int getId() {
        return id;
    }

    public String getName() {
        return name;
    }

    public List<String> getSkills() {
        return new ArrayList<>(skills); // defensive copy
    }
}
```

Immutability means object state cannot change after creation. To achieve it, we make the class final, fields private and final, avoid setters, and use defensive copies for mutable fields.

---

# Q19. Is `String` immutable because it is `final`? Explain the real reason.

### 1️⃣ Internal state cannot be modified

* `String` stores characters in a **private final internal array**
* There are **no methods** that modify this array

```java
private final byte[] value; // (or char[] in older versions)
```

### 2️⃣ No setters

* All String methods (`concat`, `replace`, `substring`)
  → **return a new String**, never modify the existing one
  
### 3️⃣ String Pool Safety

* Strings are **cached** in the String Constant Pool
* If Strings were mutable:

  * One change would affect **all references**
* Immutability makes pooling safe

### 4️⃣ Thread Safety

* Immutable objects are **thread-safe by default**
* No synchronization needed

### 5️⃣ Security

* Used in:

  * Class loading
  * File paths
  * Network connections
* Mutability could lead to **security vulnerabilities**

## Why `final` Is Still Used

* Prevents subclass from:

  * Adding setters
  * Breaking immutability contract

👉 `final` **supports** immutability, but **does not create it**.

String is immutable not just because it is final, but because its internal state cannot be modified, it has no setters, and immutability ensures thread safety, security, and safe string pooling.”


---

# Q20. Where are String literals and `new String()` objects stored in memory? Explain String Pool vs Heap.

### String Literal

```java
String s1 = "java";
String s2 = "java";
```

* `"java"` is stored in **String Constant Pool (inside Heap)**
* `s1` and `s2` point to the **same object**

### `new String()`

```java
String s3 = new String("java");
```

What happens:

1. JVM checks SCP → `"java"` exists
2. A **new String object is created in Heap**
3. `s3` points to this new object

So:

* Literal → SCP (Heap)
* `new String()` → Heap (outside SCP)

## String Modification

```java
String s = "java";
s = s.concat("8");
```

* `"java8"` is created:

  * In SCP **only if it doesn’t already exist**
* Original `"java"` remains unchanged
* `s` now points to `"java8"`

## Objects Created with `new`

Every `new` keyword:

* Creates a **new object in Heap**
* Even if an identical object already exists

> “String literals are stored in the String Constant Pool, which is part of the Heap.
> When we use `new String()`, a new object is always created in the Heap.
> Strings are immutable, so any modification creates a new String object, and the String Pool helps reuse literals to save memory.”

---





