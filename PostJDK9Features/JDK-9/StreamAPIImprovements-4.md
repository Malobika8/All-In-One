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

---

### Question:

You're given a list of numbers:

```java
List<Integer> numbers = List.of(2, 4, 6, 7, 9, 10, null, 12, 14);
```

Your goal is to:

1. **Filter out nulls** safely using `Stream.ofNullable(...)`
2. **Drop** all even numbers from the start using `dropWhile(...)`
3. **Then take** numbers **< 12** using `takeWhile(...)`
4. Print the final result.

⚠️ Rules:

* You **must use** `Stream.ofNullable(...)` to handle potential `null` values.
* You can use flatMap or any technique you find suitable.
* Output should be printed using `forEach(System.out::println)`

**`ofNullable(null)`** is a **static method** of `Stream`, not of a Stream instance. 

```java
List<Integer> numbers = List.of(2, 4, 6, 7, 9, 10, null, 12, 14);

numbers.stream()
       .flatMap(Stream::ofNullable)                        // Step 1: skip nulls safely
       .dropWhile(num -> num % 2 == 0)                     // Step 2: drop even numbers from start
       .takeWhile(num -> num < 12)                         // Step 3: take numbers less than 12
       .forEach(System.out::println);                      // Step 4: print
```

#### Explanation:

* `Stream::ofNullable` → safely ignores `null` values
* `dropWhile(num -> num % 2 == 0)` drops 2, 4, 6 — but **stops dropping at 7**
* `takeWhile(num -> num < 12)` takes 7, 9, 10 → but stops at 12 (which fails condition)

#### Output:

```
7
9
10
```

