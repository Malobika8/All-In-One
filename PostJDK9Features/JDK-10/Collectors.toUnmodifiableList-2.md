## 🔒 Java 10: `Collectors.toUnmodifiableList()`

Also: `toUnmodifiableSet()`, `toUnmodifiableMap()`

---

### 🧠 Why was this introduced?

In Java 9, we got:

```java
List.of("a", "b", "c"); // ✅ immutable
```

But when collecting from a stream:

```java
List<String> result = list.stream()
    .filter(s -> s.length() > 3)
    .collect(Collectors.toList()); // ❌ this is mutable
```

Java 10 added **immutable collection collectors** — so now you can collect directly into an **unmodifiable** collection.

---

### ✅ Example:

```java
List<String> list = List.of("apple", "banana", "fig");

List<String> result = list.stream()
    .filter(s -> s.length() > 4)
    .collect(Collectors.toUnmodifiableList());

result.add("grape"); // ❌ Throws UnsupportedOperationException
```

---

### 📌 Also available:

* `Collectors.toUnmodifiableSet()`
* `Collectors.toUnmodifiableMap(keyMapper, valueMapper)`

These are safe, concise, and enforce immutability right at collection time.

---

### Question:

Write code that:

1. Creates a `List<String>` of `"a"`, `"bb"`, `"ccc"`, `"dddd"`
2. Filters all strings with length > 2
3. Collects them into an **unmodifiable list**
4. Tries to add `"eeee"` (catch and print the exception)

```
import java.util.*;
import java.util.stream.Collectors;

public class Main {
    public static void main(String[] args) {
        List<String> list = List.of("a", "bb", "ccc", "dddd");

        List<String> result = list.stream()
                .filter(str -> str.length() > 2)
                .collect(Collectors.toUnmodifiableList());

        System.out.println("Filtered List: " + result);

        try {
            result.add("eeee"); // ❌ will throw exception
        } catch (UnsupportedOperationException ex) {
            System.out.println("Caught exception: " + ex);
        }
    }
}
```
