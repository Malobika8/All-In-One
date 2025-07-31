## 🔷 `Function<T, R>` Recap

This is a **functional interface** in `java.util.function`:

```java
@FunctionalInterface
public interface Function<T, R> {
    R apply(T t);
    
    // Default methods (very useful!)
    default <V> Function<V, R> compose(Function<? super V, ? extends T> before) { ... }
    default <V> Function<T, V> andThen(Function<? super R, ? extends V> after) { ... }
    static <T> Function<T, T> identity() { ... }
}
```

---

## ✅ Core Method

```java
R apply(T t);
```

This is the **single abstract method**, used to transform a value from type `T` to type `R`.

---

## 🟦 Why are `default` methods like `compose()` and `andThen()` useful?

They allow you to **chain functions together**, while still keeping the interface functional.

---

### 🔁 `andThen()`

```java
Function<Integer, Integer> multiplyBy2 = x -> x * 2;
Function<Integer, Integer> add10 = x -> x + 10;

Function<Integer, Integer> combined = multiplyBy2.andThen(add10);
System.out.println(combined.apply(5));  // Output: 20
```

* `andThen()` means:

  * First do: `multiplyBy2` → `5 * 2 = 10`
  * Then do: `add10` → `10 + 10 = 20`

---

### 🔁 `compose()`

```java
Function<Integer, Integer> multiplyBy2 = x -> x * 2;
Function<Integer, Integer> add10 = x -> x + 10;

Function<Integer, Integer> combined = multiplyBy2.compose(add10);
System.out.println(combined.apply(5));  // Output: 30
```

* `compose()` means:

  * First do: `add10` → `5 + 10 = 15`
  * Then do: `multiplyBy2` → `15 * 2 = 30`

---

## 📌 So what's the role of `default` here?

* Java uses **default methods** to let functional interfaces have **built-in, reusable logic** (like function chaining) without losing their "functional" status.
* This avoids writing repetitive code to combine functions manually.

---

### 🔧 Also: `Function.identity()`

```java
Function<String, String> identityFn = Function.identity();
System.out.println(identityFn.apply("Java")); // "Java"
```

It returns the **input as-is**.

---

## 🧠 Summary

| Method       | Purpose                           |
| ------------ | --------------------------------- |
| `apply()`    | Main function logic               |
| `andThen()`  | Chain another function **after**  |
| `compose()`  | Chain another function **before** |
| `identity()` | Return the input unchanged        |

---

