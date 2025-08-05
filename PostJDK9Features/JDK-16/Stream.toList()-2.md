# ✅ Java 16 Feature: `Stream.toList()` (New Method)

---

## 🔹 What’s the problem it solves?

Before Java 16, to collect a `Stream` into a `List`, you had to write:

```java
List<String> names = stream.collect(Collectors.toList());
```

That’s:

* Verbose
* Requires importing `Collectors`
* Not very readable for beginners

---

## ✅ Java 16 added a **shortcut**:

```java
List<String> names = stream.toList();
```

### 🔸 It’s just:

```java
Stream<T>.toList()
```

No collector needed. Just call `.toList()` directly on the stream.

---

### ✅ Example:

```java
List<String> list = List.of("a", "bb", "ccc");

List<String> upper = list.stream()
    .map(String::toUpperCase)
    .toList();  // Java 16

System.out.println(upper);  // [A, BB, CCC]
```

---

## ✅ Important Notes

### 🔸 What kind of list is returned?

* **Immutable**
* Unmodifiable — like `List.of(...)`
* Will throw `UnsupportedOperationException` if you try to modify it

```java
List<String> result = list.stream().toList();
result.add("test");  // ❌ Throws exception
```

If you need a modifiable list:

```java
new ArrayList<>(stream.toList());
```

---

## 🧠 Summary

| Feature                               | Benefit                      |
| ------------------------------------- | ---------------------------- |
| `stream.collect(Collectors.toList())` | ✅ Still works                |
| `stream.toList()`                     | ✅ Cleaner, shorter, built-in |
| Returned list                         | ✅ Immutable (read-only)      |

---

