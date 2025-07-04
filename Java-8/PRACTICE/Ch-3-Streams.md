### 🧠 **Topic 7: Java 8 Streams – Introduction**

#### ✅ **For Notes:**

**Java 8 Streams** provide a way to perform **functional-style operations** on collections or arrays.
Think of a **Stream** as a pipeline of data — you can **filter**, **map**, **reduce**, **collect**, and more, without writing traditional loops.

---

### 🧾 **Key Concepts:**

| Concept                    | Meaning                                                             |
| -------------------------- | ------------------------------------------------------------------- |
| **Stream**                 | A sequence of elements supporting sequential & parallel operations  |
| **Source**                 | A collection, array, or I/O channel                                 |
| **Intermediate Operation** | Returns a new Stream (lazy) → e.g., `filter`, `map`, `sorted`       |
| **Terminal Operation**     | Triggers processing → e.g., `forEach`, `collect`, `count`, `reduce` |

#### 💡 Streams don’t store data — they **process** data.

---

### 🔄 **Common Methods:**

| Type         | Method Examples                                 |
| ------------ | ----------------------------------------------- |
| Intermediate | `filter()`, `map()`, `distinct()`, `sorted()`   |
| Terminal     | `forEach()`, `collect()`, `reduce()`, `count()` |

---

### 🔧 Stream Syntax Example:

```java
List<String> names = Arrays.asList("John", "Alice", "Bob");

names.stream()
     .filter(name -> name.startsWith("A"))
     .map(String::toUpperCase)
     .forEach(System.out::println);
```

---

### 🚀 Benefits of Streams:

* Functional style (concise & expressive)
* Easy to chain multiple operations
* Can be **parallelized** with `.parallelStream()`
* No external iteration (no for-loops)

---

# ✅ Now Let’s Practice!

### 💻 Question 1: Use Stream to Filter Even Numbers

Given:

```java
List<Integer> numbers = Arrays.asList(2, 5, 8, 11, 14, 17);
```

Task:

* Use `stream()` to filter only even numbers.
* Print them one by one.

Use `filter()` and `forEach()`.

### 💻 Question 2: Use map() to Square All Numbers

Given:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5);
```

Task:

* Use map() to square each number.
* Use forEach() to print the result.

## `collect()` – Gathering Stream Results**

The `collect()` method is used to **gather results** from a stream into a collection or summary result.

We typically use `Collectors` like:

* `Collectors.toList()`
* `Collectors.toSet()`
* `Collectors.joining()`
* `Collectors.groupingBy()`
* `Collectors.counting()`

---

### 💻 Question 3: Collect Squared Even Numbers into a List

Given:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
```

Task:

* Square each number.
* Keep only even squares.
* Collect the result into a `List<Integer>` and print it.

## Stream `reduce()` – Aggregation Operation**

The `reduce()` method is used when you want to combine all elements of a stream into a **single result** — like sum, min, max, or custom operations.

---

### 📌 **Common Use Cases of `reduce()`**

| Operation     | Example                           |
| ------------- | --------------------------------- |
| Sum           | Combine integers into total sum   |
| Product       | Multiply all numbers              |
| Min/Max       | Find smallest/largest value       |
| Custom reduce | Concatenate strings, find longest |

---

### 🧾 **Method Signatures:**

```java
Optional<T> reduce(BinaryOperator<T> accumulator)
T reduce(T identity, BinaryOperator<T> accumulator)
```

#### 🔍 What's the difference?

* `reduce(identity, accumulator)` → always returns a **non-null** result.
* `reduce(accumulator)` → returns an **Optional<T>** (because stream could be empty).

---

### 🔧 Example:

```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4);

int sum = nums.stream()
              .reduce(0, (a, b) -> a + b); // identity = 0

System.out.println(sum); // Output: 10
```

---

### 💻 **Question 4: Use `reduce()` to Find the Product of All Numbers**

Given:

```java
List<Integer> numbers = Arrays.asList(1, 2, 3, 4);
```

Task:

* Use `reduce()` to multiply all the numbers.
* Print the result.

# Questions

1. Sum of Even Numbers After Doubling (List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6);
)
2. Print Unique Uppercase Names Starting With 'A' (List<String> names = Arrays.asList("Alice", "Bob", "Alice", "Andrew", "Alex", "bob");
)
3. Create List of Name Lengths (List<String> names = Arrays.asList("Java", "Python", "C++", "Go");
)
4. Concatenate All Names with Comma (List<String> names = Arrays.asList("Anna", "Ben", "Cara");
)
5. Find the Longest String (List<String> names = Arrays.asList("Java", "SpringBoot", "AI", "Microservices");
)
6. Analyze Employee Salaries:
   
   Given a list of employees (name + salary), perform the following:

   - Keep only employees with salary > 50,000
   - Convert their names to uppercase
   - Sort by salary descending
   - Collect the result into a List<String> of names
   - Print the final list
  
   ```
    class Employee {
    String name;
    int salary;

    Employee(String name, int salary) {
        this.name = name;
        this.salary = salary;
    }

    public String getName() { return name; }
    public int getSalary() { return salary; }
    }

    List<Employee> employees = Arrays.asList(
    new Employee("Alice", 48000),
    new Employee("Bob", 52000),
    new Employee("Charlie", 61000),
    new Employee("Diana", 47000),
    new Employee("Eve", 71000)
    );

   ```
