### 🧠 **Topic 11: `Optional` – Null Safety in Java 8**

Java's `NullPointerException` (NPE) is one of the most common runtime errors.
To make null handling safer and more expressive, Java 8 introduced the `Optional<T>` class.

---

### 📌 **What is `Optional<T>`?**

It’s a **container object** that may or may not contain a non-null value.

---

### ✅ **Core Methods of Optional**

| Method                       | Purpose                                                      |
| ---------------------------- | ------------------------------------------------------------ |
| `Optional.of(value)`         | Create Optional with **non-null** value (throws NPE if null) |
| `Optional.ofNullable(value)` | Create Optional from nullable value (safe)                   |
| `Optional.empty()`           | Represents an empty Optional                                 |
| `isPresent()`                | Returns true if value exists                                 |
| `get()`                      | Gets the value (⚠️ may throw NoSuchElementException)         |
| `ifPresent(Consumer)`        | Executes code if value is present                            |
| `orElse(defaultValue)`       | Returns value or default                                     |
| `orElseGet(Supplier)`        | Lazy version of `orElse()`                                   |
| `orElseThrow()`              | Throws if value not present                                  |
| `map(Function)`              | Transform the value                                          |
| `flatMap(Function)`          | Same as `map` but avoids nesting Optionals                   |

---

### 🧾 **Why use Optional?**

* Avoids `null` checks
* Promotes functional-style programming
* Makes the possibility of absence **explicit**

---

### 💡 Example:

```java
Optional<String> opt = Optional.of("Java");
opt.ifPresent(str -> System.out.println(str.toUpperCase())); // Output: JAVA
```

---

### ✅ Let's Practice!

### 💻 **Question 1: Create an Optional and Print If Present**

Task:

1. Create an `Optional<String>` using `Optional.ofNullable()`.
2. If the value is present, print it in uppercase using `ifPresent()`.

Test with both `"hello"` and `null`.

### 💻 Question 2: Use orElse() to Provide a Default Value

Task:

1. Create an Optional<String> from a null value.
2. Use orElse() to return "default" if value is not present.

Print the result.

### 💻 Question 3: Use map() with Optional

Task:

1. Create an Optional<String> from "java".
2. Use map() to convert it to uppercase.

Print the final result using get().

Perfect! Here's one more **real-world-style misc challenge** to lock in everything before we dive into `Collectors.groupingBy()`.

---

## 💻 **Misc Challenge: Student Score Analysis**

#### Given:

```java
class Student {
    String name;
    int score;

    Student(String name, int score) {
        this.name = name;
        this.score = score;
    }

    public String getName() { return name; }
    public int getScore() { return score; }
}

List<Student> students = Arrays.asList(
    new Student("Alice", 82),
    new Student("Bob", 67),
    new Student("Charlie", 90),
    new Student("David", 45),
    new Student("Eva", 75)
);
```

---

### 🧠 Task:

1. Filter students who scored **75 or above**
2. Sort them in **descending order of score**
3. Map to their **name in uppercase**
4. Collect and print the list of names

🧾 Expected Output:

```
[CHARLIE, ALICE, EVA]
```

