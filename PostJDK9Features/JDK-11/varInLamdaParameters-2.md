## **`var` in Lambda Parameters**

---

### 🔙 Background:

In Java 10, you could use `var` for **local variables**:

```java
var name = "Java"; // inferred as String
```

In Java 11, you can now also use `var` in **lambda parameters**, like this:

```java
list.forEach((var item) -> System.out.println(item));
```

---

### 🔍 Why is this useful?

It lets you:

* Add **annotations** to lambda parameters (like `@Nonnull`)
* Use a **consistent style** if other parameters already use `var`
* Add **types explicitly** without switching back to `String`, `Integer`, etc.

---

### ✅ Examples:

```java
List<String> list = List.of("apple", "banana");

list.forEach((var fruit) -> System.out.println(fruit.toUpperCase()));
```

🧠 But note:

* You **must** use `var` for **all** parameters, or for **none**

```java
// Valid
(var x, var y) -> ...

// ❌ Invalid (mixed types)
(var x, y) -> ...   // ❌ Compile error
```

---

### Question:

Write code that:

1. Creates a list of strings: `"hello"`, `"world"`
2. Uses a lambda with `var` to print each string in uppercase

```
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<String> list = List.of("hello", "world");

        list.stream().forEach((var str) -> System.out.println(str.toUpperCase()));
    }
}
```

## ❓ So, if this works:

```java
list.stream().forEach(str -> System.out.println(str));
```

Why do we even need:

```java
list.stream().forEach((var str) -> System.out.println(str));
```

Most of the Time, You **Don't Need `var`**. The **type is inferred automatically** by the compiler in most lambdas.
That’s why this is totally fine and preferred for **simplicity**:

```java
str -> System.out.println(str);
```

---

## ✅ So why was `var` added in Java 11 for lambdas?

### 🧠 1. **Adding annotations to lambda parameters**

Suppose you’re using a validation framework or want to add annotations like `@Nonnull`, `@NotBlank`, etc.

Without `var`, you **can’t annotate**:

```java
str -> System.out.println(str);               // ❌ no place for annotation
```

With `var`, you can:

```java
(var @Nonnull str) -> System.out.println(str);  // ✅ now you can annotate!
```

---

### 🧠 2. **Consistency with other code**

When you already use `var` elsewhere:

```java
var name = "Malobika";
var list = List.of("a", "b");

// now using var in lambda feels consistent
list.forEach((var x) -> System.out.println(x));
```

This is **stylistic**, not functional — some teams prefer it.

---

### 🧠 3. **Future-Proofing / Explicitness**

Some developers or codebases want **explicit visibility** of the inferred type without writing `String str`.
Using `var` makes it **obvious** that the type is inferred.

---

### ✅ Summary:

| Use Case                            | Do You Need `var`?             |
| ----------------------------------- | ------------------------------ |
| Normal lambda                       | ❌ No                           |
| Adding annotations                  | ✅ Yes                          |
| Code style preference               | ✅ Maybe                        |
| Multiple parameters with annotation | ✅ Yes (must use `var` for all) |

---

