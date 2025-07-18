# What is the difference between Collection and Stream in Java 8? When would you use one over the other?

### Sol:

* **Collection**:

  * A *Collection* (like `List`, `Set`, `Map`) is a data structure used to store and access elements.
  * Collections are **eager** in nature — they hold all the data in memory.

* **Stream**:

  * A *Stream* is a **pipeline of functional operations** that can process elements **lazily** from a data source (like a Collection).
  * It doesn't store data. Instead, it **pulls data from a source**, processes it, and optionally produces a result.
  * Streams support **declarative**, **functional-style programming** (e.g., map, filter, reduce).

#### When to use:

* Use **Collection** when you want to **store or access** elements repeatedly.
* Use **Stream** when you want to **process data** in a pipeline (filter/map/sort/etc.)—possibly with **parallelism** or **functional operations**.

---

# What is the difference between `map()` and `flatMap()` in Java Streams? When would you use each?

### Sol:

* **`map(Function<T, R>)`**:

  * Transforms each element of the stream **individually**.
  * It returns a **Stream of transformed elements**.
  * Example: `List<String> → Stream<Integer>` by doing `map(String::length)`.

* **`flatMap(Function<T, Stream<R>>)`**:

  * Flattens **nested structures** (i.e., a stream of streams → single stream).
  * Each element is transformed into a **Stream**, and all streams are then **flattened** into one.
  * Example: `List<List<Integer>>` → `Stream<Integer>`

#### Example:

```java
List<String> list = Arrays.asList("abc", "de");

list.stream()
    .map(str -> str.split(""))     // Stream<String[]>
    .flatMap(Arrays::stream)       // Stream<String>
    .forEach(System.out::println);
```

---

# Task:
You have a list of sentences:

```java
List<String> sentences = Arrays.asList("Java is cool", "Streams are powerful");
```

Write a Java Stream expression to extract **all words** from all sentences into a **single list** of words:

```java
// Output: ["Java", "is", "cool", "Streams", "are", "powerful"]
```

### Sol:

```
List<String> sentences = Arrays.asList("Java is cool", "Streams are powerful");
        
        sentences.stream()
            .map(str -> str.split(" "))
            .flatMap(str -> Arrays.stream(str))
            .forEach(System.out::println);
```

---

# What is the difference between filter() and map() in Streams? When would you use each one?

### Sol:

* **`filter(Predicate<T>)`**:

  * Used to **exclude elements** based on a condition.
  * Keeps only the elements that match the predicate.
  * Example: `filter(name -> name.startsWith("A"))`

* **`map(Function<T, R>)`**:

  * Used to **transform elements** of the stream.
  * Returns a new stream with each element **converted** or **modified**.
  * Example: `map(name -> name.toUpperCase())`

#### Example:

```java
List<String> names = Arrays.asList("Alice", "Bob", "Andrew");

List<String> result = names.stream()
    .filter(name -> name.startsWith("A"))     // keeps Alice, Andrew
    .map(String::toUpperCase)                 // transforms to UPPERCASE
    .collect(Collectors.toList());

System.out.println(result); // Output: [ALICE, ANDREW]
```

---

# `filter()` + `map()` – Basic Transformation

Given the list of employee names:

```java
List<String> names = Arrays.asList("Ankit", "Bob", "Akash", "John", "Arun");
```

Write a Stream expression to:

1. Filter out names that **start with "A"**
2. Convert them to **uppercase**
3. Collect and return the result as a **List<String>**

### Sol:

```
import java.util.*;
import java.util.stream.*;

public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Ankit", "Bob", "Akash", "John", "Arun");

        List<String> list = names.stream()
            .filter(str -> str.startsWith("A"))
            .map(String::toUpperCase)
            .collect(Collectors.toList());

        list.forEach(System.out::println);
    }
}
```

---







