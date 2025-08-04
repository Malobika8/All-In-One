## 🧱 **Module System (Project Jigsaw)**

This was the **biggest architectural change** since Java started.

---

### 🧠 Why was it introduced?

Before Java 9, the JDK had become **monolithic**:

* Applications depended on everything inside the JDK.
* There was no standard way to divide large apps into **independent modules**.
* Java applications had **no true encapsulation** at the module level.

Java 9 introduced a **module system** to solve this.

---

### 🔍 What is a Module in Java 9?

A **module** is a **self-contained unit of code** with:

* Its own **name**
* A list of **dependencies (other modules)**
* A list of **packages it exports**

Each module has a special file:

```
module-info.java
```

---

### 📦 Example:

Suppose we have a module named `com.example.hello`.

```java
// file: module-info.java
module com.example.hello {
    exports com.example.hello.api;
}
```

* `exports` means we allow **other modules** to access that package.
* If a package is not exported, it’s **hidden** from others (encapsulation!).

---

### 📚 Key Keywords

| Keyword    | Purpose                                               |
| ---------- | ----------------------------------------------------- |
| `module`   | Declares a module                                     |
| `requires` | Declares dependency on another module                 |
| `exports`  | Makes a package accessible to other modules           |
| `opens`    | Allows reflection access (for frameworks like Spring) |

---

### ✅ Qestion

You're creating a module named `com.user.app` that depends on another module called `com.utils.helper`.

1. How will you write the `module-info.java` for `com.user.app`?
2. If you want to expose a package `com.user.api` to others, what should you write?

#### 🔁 Let’s break down

```java
module com.user.app {
    requires com.utils.helper;   // You’re declaring dependency
    exports com.user.api;        // You’re exposing only the necessary part
}
```

This is **clean**, **modular**, and **encapsulated**.

In old Java, anyone could access any class from any package. With modules, you now **control visibility** at a higher level.

---

### ⚠️ Important Notes:

1. If you don’t `exports` a package, **other modules cannot access it** — not even via reflection (unless you use `opens`).
2. `requires transitive` — means any module that uses your module will also get the dependency you’re requiring. Useful for API libraries.

---

### 🧪 A Quick Check

Suppose your module depends on `java.sql` and you also want to allow reflection into a package `com.user.internal` (e.g. for Spring or Jackson).
👉 What would your `module-info.java` look like?

```java
module com.user {
    requires java.sql;               // You depend on Java's SQL module
    opens com.user.internal;         // You allow reflective access (e.g. for frameworks)
}
```

> 🧠 `opens` is **not the same as `exports`**:

* `exports` allows **compile-time access** to public types.
* `opens` allows **runtime reflective access** (needed by frameworks).

You can even combine them like:

```java
exports com.user.api;
opens com.user.internal;
```

---

### 🧠 Final Recap on Module System:

| Feature               | Purpose                                                 |
| --------------------- | ------------------------------------------------------- |
| `module-info.java`    | Declares dependencies & visibility                      |
| `requires`            | Declares dependency                                     |
| `exports`             | Makes packages public to other modules                  |
| `opens`               | Allows reflection (without exposing it at compile time) |
| `requires transitive` | Makes a dependency also available to your users         |

---
