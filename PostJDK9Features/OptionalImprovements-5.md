## ☑️ Java 9: **Enhancements to `Optional` API**

---

Java 8 introduced `Optional<T>` to avoid `null` references.
In **Java 9**, it got **three very useful additions**:

---

### ✅ 1. `ifPresentOrElse(Consumer, Runnable)`

Runs a block if a value is present; otherwise, runs something else.

#### 🔍 Example:

```java
Optional<String> name = Optional.of("Malobika");

name.ifPresentOrElse(
    val -> System.out.println("Value: " + val),
    () -> System.out.println("Value is absent")
);
```

If `Optional.empty()`, it will print: `Value is absent`.

---

### ✅ 2. `Optional.or(Supplier<Optional>)`

Provides a fallback Optional **if the original is empty**.

#### 🔍 Example:

```java
Optional<String> value = Optional.empty();

String result = value
    .or(() -> Optional.of("Default"))
    .get();

System.out.println(result); // Default
```

---

### ✅ 3. `Optional.stream()`

This allows you to use `Optional` in **Stream pipelines**.

#### 🔍 Example:

```java
Optional<String> name = Optional.of("Java");

name.stream()
    .map(String::toUpperCase)
    .forEach(System.out::println);
```

If the optional is empty, the stream is empty too — very handy for **flatMap + optional pipelines**.

---

### Question:

You have:

```java
Optional<String> input = Optional.ofNullable(null);
```

Write code that:

1. Prints `"Received: <value>"` if value is present
2. Prints `"No value received"` if not
3. Uses only **Java 9+ methods** (`ifPresentOrElse`, not `isPresent()`)

```java
Optional<String> name = Optional.ofNullable(null);

name.ifPresentOrElse(
    val -> System.out.println("Received: " + val),
    () -> System.out.println("No value received")
);
```

#### 🧠 Breakdown:

* ✅ `val -> ...` → Runs when value is present
* ✅ `() -> ...` → Runs when Optional is empty

---


