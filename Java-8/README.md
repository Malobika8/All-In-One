# Imperative VS Declarative VS Functional

> **Find all names starting with “J” and ending with “a”, convert them to uppercase, and print them.**

We’ll write it in **three styles** —
1️⃣ Imperative (traditional Java)
2️⃣ Declarative (SQL-like logic)
3️⃣ Functional (Java Streams)

### Imperative Style — *“How to do it”*

```java
List<String> names = Arrays.asList("Java", "Jaya", "Jenna", "Jira", "Julia");

List<String> result = new ArrayList<>();

for (String name : names) {
    if (name.startsWith("J") && name.endsWith("a")) {
        result.add(name.toUpperCase());
    }
}

for (String r : result) {
    System.out.println(r);
}
```

### Characteristics:

* Focuses on **how** to do each step.
* You manage **iteration**, **conditions**, and **mutable state** (`result` list).
* Verbose but explicit — classic procedural Java.

### Declarative Style — *“What to do” (SQL mindset)*

Imagine if your data were in a database table named `names`.

You’d simply write:

```sql
SELECT UPPER(name)
FROM names
WHERE name LIKE 'J%a';
```

### Characteristics:

* Describes **what you want** (“names starting with J and ending with a”)
* Doesn’t tell how iteration or filtering happens.
* SQL engine handles the “how.”

### Functional Style — *Declarative in Java (using functions)*

```java
import java.util.*;
import java.util.stream.*;

public class Main {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Java", "Jaya", "Jenna", "Jira", "Julia");

        names.stream()
             .filter(n -> n.startsWith("J") && n.endsWith("a"))
             .map(String::toUpperCase)
             .forEach(System.out::println);
    }
}
```

### Characteristics:

* Also **describes what**, not **how**.
* Uses **higher-order functions** (`filter`, `map`, `forEach`).
* No mutable state, no explicit loops.
* Can be parallelized easily with `.parallelStream()`.

### Summary Comparison

| Feature         | Imperative | Declarative (SQL)    | Functional (Streams)        |
| --------------- | ---------- | -------------------- | --------------------------- |
| Style           | Procedural | Declarative          | Declarative + Functional    |
| “How” or “What” | **How**    | **What**             | **What**                    |
| Code length     | Long       | Short                | Compact                     |
| Mutability      | Mutable    | Immutable            | Immutable                   |
| Example         | For-loops  | SQL Query            | Stream operations           |
| Parallelization | Manual     | Built-in (DB engine) | Built-in (`parallelStream`) |

### So in short:

* **Declarative style** = say what you want.
* **Functional style** = declarative style + use of functions (lambdas, pure functions, composition).


# Methods

- Stream.generate()
- Stream.of()
- iterate()
- forEach()
- peek()
- sorted()
- limit()
- filter()
- takeWhile()
- skip()
- distinct()

Stream functionality in Collections
- List.stream()
- Arrays.stream()

## Intermediate Operations
- Return a Stream → allow further chaining
- Lazy → executed only when a terminal operation is called

#### Examples:
- map()
- filter()
- flatMap()
- distinct()
- sorted()
- peek()

## Terminal Operations

- Consume the stream → produce a result or side-effect
- Trigger the execution of intermediate operations

#### Examples:
- collect()
- reduce()
- count()
- forEach()
- findFirst() / findAny()
- anyMatch() / allMatch() / noneMatch()
  
# In-built Functional Interfaces available:

<img width="381" alt="Screenshot 2024-08-05 at 10 58 09 AM" src="https://github.com/user-attachments/assets/511be3b5-7eed-44bd-b8b4-b51bb4f77435">
<img width="384" alt="Screenshot 2024-08-05 at 10 58 17 AM" src="https://github.com/user-attachments/assets/75c6e756-929f-4348-822e-984d96cd9d1b">

## Some examples

### BiConsumer:

```
@FunctionalInterface
public interface BiConsumer<T, U> {

    /**
     * Performs this operation on the given arguments.
     *
     * @param t the first input argument
     * @param u the second input argument
     */
    void accept(T t, U u);
```

### BiFunction:

```
@FunctionalInterface
public interface BiFunction<T, U, R> {

    /**
     * Applies this function to the given arguments.
     *
     * @param t the first function argument
     * @param u the second function argument
     * @return the function result
     */
    R apply(T t, U u);
```

### BinaryOperator:

```
@FunctionalInterface
public interface BinaryOperator<T> extends BiFunction<T,T,T> {
    /**
     * Returns a {@link BinaryOperator} which returns the lesser of two elements
     * according to the specified {@code Comparator}.
     *
     * @param <T> the type of the input arguments of the comparator
     * @param comparator a {@code Comparator} for comparing the two values
     * @return a {@code BinaryOperator} which returns the lesser of its operands,
     *         according to the supplied {@code Comparator}
     * @throws NullPointerException if the argument is null
     */
    public static <T> BinaryOperator<T> minBy(Comparator<? super T> comparator) {
        Objects.requireNonNull(comparator);
        return (a, b) -> comparator.compare(a, b) <= 0 ? a : b;
    }

    /**
     * Returns a {@link BinaryOperator} which returns the greater of two elements
     * according to the specified {@code Comparator}.
     *
     * @param <T> the type of the input arguments of the comparator
     * @param comparator a {@code Comparator} for comparing the two values
     * @return a {@code BinaryOperator} which returns the greater of its operands,
     *         according to the supplied {@code Comparator}
     * @throws NullPointerException if the argument is null
     */
    public static <T> BinaryOperator<T> maxBy(Comparator<? super T> comparator) {
        Objects.requireNonNull(comparator);
        return (a, b) -> comparator.compare(a, b) >= 0 ? a : b;
    }
}
```

### BiPredicate:

```
@FunctionalInterface
public interface BiPredicate<T, U> {

    /**
     * Evaluates this predicate on the given arguments.
     *
     * @param t the first input argument
     * @param u the second input argument
     * @return {@code true} if the input arguments match the predicate,
     * otherwise {@code false}
     */
    boolean test(T t, U u);
```

### BooleanSupplier:

```
@FunctionalInterface
public interface BooleanSupplier {

    /**
     * Gets a result.
     *
     * @return a result
     */
    boolean getAsBoolean();
}
```

### Consumer:

```
@FunctionalInterface
public interface Consumer<T> {

    /**
     * Performs this operation on the given argument.
     *
     * @param t the input argument
     */
    void accept(T t);
```

### DoubleBinaryOperator:

```
@FunctionalInterface
public interface DoubleBinaryOperator {
    /**
     * Applies this operator to the given operands.
     *
     * @param left the first operand
     * @param right the second operand
     * @return the operator result
     */
    double applyAsDouble(double left, double right);
}
```

### DoubleConsumer

```
@FunctionalInterface
public interface DoubleConsumer {

    /**
     * Performs this operation on the given argument.
     *
     * @param value the input argument
     */
    void accept(double value);
```

### DoubleFunction

```
@FunctionalInterface
public interface DoubleFunction<R> {

    /**
     * Applies this function to the given argument.
     *
     * @param value the function argument
     * @return the function result
     */
    R apply(double value);
}
```

### Function

```
@FunctionalInterface
public interface Function<T, R> {

    /**
     * Applies this function to the given argument.
     *
     * @param t the function argument
     * @return the function result
     */
    R apply(T t);
```

### Predicate:

```
@FunctionalInterface
public interface Predicate<T> {

    /**
     * Evaluates this predicate on the given argument.
     *
     * @param t the input argument
     * @return {@code true} if the input argument matches the predicate,
     * otherwise {@code false}
     */
    boolean test(T t);
```

### Supplier:

```
@FunctionalInterface
public interface Supplier<T> {

    /**
     * Gets a result.
     *
     * @return a result
     */
    T get();
}
```

### ToLongFunction:

```
@FunctionalInterface
public interface ToLongFunction<T> {

    /**
     * Applies this function to the given argument.
     *
     * @param value the function argument
     * @return the function result
     */
    long applyAsLong(T value);
}
```

---
# Stream methods

## Map:
- Collectors.toMap()
- Collectors.groupingBy(): returns a Map<K, List<V>>
  - Collectors.mapping(): It is a downstream collector used within another collector like groupingBy() or partitioningBy() to transform elements before collecting them. If we want the list to contain specific data rather than the entire object, we can use this.

## List:
- Collectors.toList();

## Split elements into 2 groups:
- partitioningBy() — Split elements into two groups (true/false)

## Summarizing or aggregating manually
- Collectors.reducing()

---

# Please check: https://docs.oracle.com/javase/8/docs/api/java/util/stream/Collectors.html





















