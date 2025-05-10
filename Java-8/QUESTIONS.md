## 🚀 Roadmap: Java 8 Lambdas, Streams, and Method References

### ✅ Step 1: Java 8 Lambda Expressions

* **Concepts to Learn:**

  * What is a Lambda Expression?
  * Syntax and rules.
  * Functional interfaces (`Runnable`, `Callable`, `Comparator`, `Predicate`, etc.)
  * Lambda with and without return types.
  * Lambdas capturing local variables (effectively final concept).

* **Practice with:**

  * Sorting collections
  * Iterating lists
  * Filtering data
  * Replacing anonymous classes

---

### ✅ Step 2: Functional Interfaces (before Streams)

* **Important Interfaces:**

  * `Predicate<T>` - for conditions
  * `Function<T,R>` - for mapping
  * `Consumer<T>` - for processing
  * `Supplier<T>` - for providing values
  * `BiFunction`, `BiPredicate`, etc.

* **Practice:**

  * Writing your own functional interfaces.
  * Passing lambda to methods.

---

### ✅ Step 3: Java 8 Stream API

* **Concepts to Learn:**

  * What is Stream? Difference between Collection and Stream.
  * **Intermediate Operations:**

    * `map`, `filter`, `sorted`, `distinct`, `flatMap`
  * **Terminal Operations:**

    * `collect`, `forEach`, `reduce`, `count`, `min`, `max`, `anyMatch`
  * Stream creation:

    * From `List`, `Set`, `Map`
    * Using `Stream.of()`, `Arrays.stream()`
  * Lazy vs Eager evaluation.
  * Streams are single-use.
* **Practice:**

  * Convert `List<Integer>` → even numbers list.
  * Convert `List<String>` → uppercase names.
  * Find duplicates.
  * Group data using `Collectors.groupingBy`.
  * Sum/average/count using `Collectors`.

---

### ✅ Step 4: Method References

* **Concepts to Learn:**

  * Types:

    * Reference to a static method (`ClassName::staticMethod`)
    * Reference to an instance method (`instance::instanceMethod`)
    * Reference to a constructor (`ClassName::new`)
  * Difference between Lambda and Method Reference.

* **Practice:**

  * Replace lambdas with method references.
  * Sort using `String::compareToIgnoreCase`.
  * Use constructor references in stream `.map()`.

---

### ✅ Step 5: Advanced Stream API

* **Concepts to Learn:**

  * `Optional` with Streams.
  * `flatMap()` vs `map()`
  * Parallel Streams.
  * Collectors: `groupingBy`, `partitioningBy`, `joining`
  * Custom collectors.

* **Practice:**

  * Find 2nd highest salary.
  * Group employees by department.
  * Partition students by pass/fail.
  * Join names with comma-separated string.

---

## 📚 List of Must-Practice Interview Questions

### 🔥 Lambda Expressions

1. Write a lambda to sort a list of names in reverse order.
2. Replace an anonymous `Runnable` with lambda.
3. Write a lambda that multiplies 2 numbers.
4. How does lambda capture variables? Why they must be *effectively final*?
5. Write a lambda to filter out nulls from a list.

### 🔥 Functional Interfaces

6. Implement `Predicate<String>` to check if string starts with "A".
7. Use `Function<Integer, String>` to convert number to string.
8. Pass a `Consumer` to print every element of list.
9. Write your own functional interface and use it with lambda.
10. Use `Supplier` to generate random numbers.

### 🔥 Stream Basics

11. Convert a list of integers to a list of their squares.
12. Filter names starting with letter "S".
13. Sort a list of employees by salary.
14. Find the maximum number from a list.
15. Count elements greater than 50 in a list.

### 🔥 Advanced Stream

16. Find duplicate elements in list using Stream.
17. Group employees by department using `groupingBy`.
18. Find the employee with the highest salary.
19. Convert `List<String>` to comma-separated `String`.
20. Flatten a list of lists using `flatMap`.

### 🔥 Method Reference

21. Sort a list of strings using method reference.
22. Replace lambda with method reference where possible.
23. Use constructor reference to create objects in stream.
24. Use `System.out::println` in `forEach`.

### 🔥 Real-world Coding Problems (Asked in Interviews)

25. Find 2nd highest number from list.
26. Get names of top 3 highest-paid employees.
27. Partition numbers into even and odd.
28. Group students by grade.
29. Find frequency/count of each character in string.
30. Reverse each word in a string using streams.

---
