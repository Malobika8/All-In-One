## 🔄 Java 9: **Stream API Improvements**

Java 9 added **4 useful methods** to the `Stream` interface:

| Method                           | Purpose                                                  |
| -------------------------------- | -------------------------------------------------------- |
| `takeWhile(Predicate)`           | Take elements until predicate fails                      |
| `dropWhile(Predicate)`           | Drop elements while predicate holds, then take the rest  |
| `ofNullable(T)`                  | Create a stream of 0 or 1 element                        |
| `iterate(seed, predicate, next)` | Enhanced version of `iterate` with termination condition |

---

### ✅ 1. `takeWhile(Predicate)`

```java
List<Integer> nums = List.of(1, 2, 3, 6, 4, 2, 1);
List<Integer> result = nums.stream()
    .takeWhile(n -> n < 5)
    .collect(Collectors.toList());
```

**Output:** `[1, 2, 3]`

> 🧠 It stops as soon as it finds the first element **not matching** the predicate (`6 >= 5`), and does **not resume**.

---

### ✅ 2. `dropWhile(Predicate)`

```java
List<Integer> result = nums.stream()
    .dropWhile(n -> n < 5)
    .collect(Collectors.toList());
```

**Output:** `[6, 4, 2, 1]`

> 🧠 Opposite of `takeWhile` — drops elements until the predicate **fails**, then takes the rest.

---

### ✅ 3. `ofNullable(T element)`

```java
Stream<String> s = Stream.ofNullable(null);
System.out.println(s.count()); // 0
```

```java
Stream<String> s2 = Stream.ofNullable("hello");
System.out.println(s2.count()); // 1
```

> 🧠 Very useful when dealing with **potentially null** values without manually checking for null.

---

### ✅ 4. `Stream.iterate(seed, predicate, next)`

```java
Stream<Integer> stream = Stream.iterate(1, n -> n <= 10, n -> n + 2);
stream.forEach(System.out::print); // 13579
```

> 🧠 Unlike the old version, this one lets you add a **termination condition** directly!

---

### Question:

Given this list:

```java
List<String> words = List.of("ant", "bee", "cat", "dog", "elephant", "fox");
```

Use `takeWhile` to collect all words **with length <= 3** & stop as soon as one word is longer than 3 characters.

```
words.stream()
     .takeWhile(str -> str.length() <= 3)
     .forEach(System.out::println);
```
