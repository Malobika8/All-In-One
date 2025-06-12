## ✅ 1. `ClassNotFoundException`

### 🔹 **Checked Exception**

### 🔍 Meaning:

> **You tried to load a class by name (usually using reflection or Class.forName)**, but it wasn't found **at runtime** in the classpath.

---

### 🧠 When does it happen?

* You explicitly try to load a class by name, like:

```java
Class.forName("com.example.MyClass");
```

If `MyClass` is **not available in the classpath at runtime**, you get:

```
java.lang.ClassNotFoundException: com.example.MyClass
```

> It’s **checked**, so you **must handle or declare it**.

---

### ✅ Common use cases where this occurs:

* JDBC driver loading
* Reflection-based frameworks (Spring, Hibernate)
* Classloaders

---

## ✅ 2. `NoClassDefFoundError`

### 🔹 **Unchecked (Error)**

### 🔍 Meaning:

> The class **was present at compile time**, but **not available at runtime** — JVM cannot find the `.class` file when trying to load it.

---

### 🧠 When does it happen?

* You compiled your code successfully.
* But at runtime, the `.class` file is missing or corrupted, or its dependency chain is broken.

```java
MyClass obj = new MyClass();  // Looks fine at compile time
```

But if `MyClass.class` is missing from the classpath at runtime, you get:

```
java.lang.NoClassDefFoundError: com/example/MyClass
```

---

## 🆚 Key Differences

| Feature           | `ClassNotFoundException`                            | `NoClassDefFoundError`                                                 |
| ----------------- | --------------------------------------------------- | ---------------------------------------------------------------------- |
| Type              | Checked Exception                                   | Runtime Error (unchecked)                                              |
| When it occurs    | When trying to **dynamically load** a class by name | When JVM **can’t find** a class that was available during compile time |
| Triggered by      | Reflection (`Class.forName()`)                      | Regular class usage                                                    |
| Cause             | Class not in classpath at runtime                   | Class missing or broken at runtime                                     |
| Requires handling | ✅ Yes                                               | ❌ No (unrecoverable)                                                   |

---

## 🧪 Example to trigger both:

```java
public class Test {
    public static void main(String[] args) throws Exception {
        Class.forName("com.missing.Driver");  // 👈 ClassNotFoundException

        MissingClass obj = new MissingClass();  // 👈 NoClassDefFoundError if MissingClass.class is gone
    }
}
```

---

## ✅ Quick Tip:

* `ClassNotFoundException`: You asked for the class, it **was never there**.
* `NoClassDefFoundError`: The class **was there before**, but **now it’s gone** at runtime.

---
