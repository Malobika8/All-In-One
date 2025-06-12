## 🔥 TRICKY INTERFACE vs ABSTRACT CLASS QUESTIONS

---

### ❓1. Can an abstract class have **no abstract methods**?

✅ **Yes**, it can.

```java
abstract class A {
    void sayHi() {
        System.out.println("Hi");
    }
}
```

> Abstract class just means: **you can’t instantiate it directly** — not that it must contain abstract methods.

---

### ❓2. Can an interface have **constructors**?

❌ **No**, interfaces **cannot have constructors** because they **cannot be instantiated**.

---

### ❓3. Can an interface have a **static block**?

❌ **No**, static blocks are not allowed in interfaces.

But: you **can** have `static` methods and `static final` variables.

---

### ❓4. What is the **default modifier** for methods in an interface?

Before Java 8:

* Methods are implicitly `public abstract`

Since Java 8:

* You can also have `default` and `static` methods (with bodies)

Since Java 9:

* You can have `private` methods (for internal helper use)

---

### ❓5. Can an abstract class implement an interface **without overriding all methods**?

✅ **Yes**, but only if the abstract class is also marked `abstract`.

```java
interface A {
    void show();
}

abstract class B implements A {
    // No override yet — still legal
}
```

---

### ❓6. Can you declare an interface as `final`?

❌ **No** — because you **cannot extend a final type**, and interfaces are meant to be extended.

> You’ll get a compile-time error:
> `Illegal modifier for the interface A; only public & abstract are permitted`

---

### ❓7. Can an abstract class have a `main` method and be run?

✅ **Yes**. Even though you can't instantiate it, the class can have a `main` method and can be executed.

```java
abstract class Test {
    public static void main(String[] args) {
        System.out.println("You can run me!");
    }
}
```

---

### ❓8. Can an interface extend a class?

❌ **No** — interfaces can only **extend other interfaces**, not classes.

---

### ❓9. Can a class be both `abstract` and `final`?

❌ **No** — they contradict each other.

* `abstract`: needs to be subclassed
* `final`: cannot be subclassed

---

### ❓10. Can an interface extend multiple interfaces with the same default method?

✅ **Yes**, but any class that implements the extending interface **must resolve the conflict**.

---

### ❓11. What happens if two interfaces define the same method signature without a body?

✅ No problem — it's as if only one abstract method exists.

```java
interface A { void run(); }
interface B { void run(); }
interface C extends A, B {}  // ✅ Legal
```

But if both define **default methods**, it must be resolved.

---

### ❓12. Can abstract classes have private abstract methods?

❌ **No** — abstract methods must be overridden, and `private` methods can’t be accessed by subclasses.

---

## 💡 Bonus Brain-Teasers

### 🧠 Can an interface be empty?

✅ **Yes** — it’s called a **marker interface**, like `Serializable` or `Cloneable`.

---

### 🧠 Can you declare a variable of an abstract class type?

✅ **Yes** — you just can’t instantiate it.

```java
abstract class Animal {}
Animal a;  // ✅ valid
a = new Animal();  // ❌ compile-time error
```

---

