## ⚡ Java 9: **Compact Strings**

This is not a language feature — it's a **JVM-level performance improvement**.

---

### 🧠 Background (Before Java 9):

In Java 8 and earlier, every `String` was backed by a `char[]`:

```java
String str = "abc"; 
// Internally stored as: char[] {'a', 'b', 'c'}
```

Each `char` in Java uses **2 bytes** (UTF-16).
Even if you're using only ASCII characters (like `a`, `b`, `c`), you still waste memory by using 2 bytes per character.

---

### ✅ What Changed in Java 9?

Strings are now stored using a **byte\[]** instead of `char[]`, and:

* If your string uses only **Latin-1 (ASCII)** characters → stored as **1 byte per char**
* If your string needs **Unicode** → falls back to UTF-16 (2 bytes)

This optimization is called the **Compact String** feature.

---

### 📦 Internally:

* Java 9 replaces `char[]` with a `byte[]` + `coder`
* The `coder` tells the JVM whether the string is **Latin-1** or **UTF-16**

---

### 🔍 Benefit:

* Saves memory for most real-world strings (which are ASCII)
* Improves cache efficiency and speed
* No change to how you write or use Strings — totally backward compatible

---

### ✅ Example:

You write:

```java
String s = "Hello";
```

In Java 8:

* Stored as `char[]` → 10 bytes (5 chars × 2 bytes)

In Java 9:

* Stored as `byte[]` → 5 bytes (1 byte per char)
  → ✅ \~50% memory savings

---

### 🧪 Do you need to change anything in code?

**No.** This is 100% internal.

You keep writing:

```java
String s = "abc";
```

The JVM is now just smarter about how to **store** it.

---

