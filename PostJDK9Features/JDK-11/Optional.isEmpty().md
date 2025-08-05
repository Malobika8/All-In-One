## ✅ Java 11 Feature: Enhancements to `Optional` – `isEmpty()`

---

### 🔹 What's new?

Java 11 added a simple but helpful method to `Optional<T>`:

```java
boolean isEmpty()
```

---

### ✅ Before Java 11:

To check if an `Optional` was **empty**, you had to write:

```java
if (!optional.isPresent()) {
    // do something
}
```

Or even worse:

```java
if (optional.isPresent() == false) {
    // old-school
}
```

---

### ✅ Java 11 makes it cleaner:

```java
if (optional.isEmpty()) {
    // much more readable
}
```

---

### ✅ Full Example:

```java
Optional<String> name = Optional.ofNullable(null);

if (name.isEmpty()) {
    System.out.println("Name is not present");
}
```

---

### ✅ Why it matters:

* Improves **code readability**
* Matches `Collection.isEmpty()` and `String.isEmpty()`
* Frequently used in **Stream filters**, conditionals, validations

---

### ✅ Works well with Stream filtering:

```java
List<Optional<String>> names = List.of(Optional.of("John"), Optional.empty());

names.stream()
     .filter(Optional::isPresent)    // Old way
     .map(Optional::get)
     .forEach(System.out::println);

names.stream()
     .filter(opt -> !opt.isEmpty())  // New way (slightly more readable in some cases)
     .map(Optional::get)
     .forEach(System.out::println);
```

---

### 🧠 Summary:

| Method        | Since   | Purpose                                 |
| ------------- | ------- | --------------------------------------- |
| `isPresent()` | Java 8  | Check if value is present               |
| `isEmpty()`   | Java 11 | Check if value is absent (cleaner code) |

---

