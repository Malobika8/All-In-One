### 🧠 **Topic 1: Lambda Expressions (Java 8 Core Feature)**

#### ✅ **Intro:**

Lambda expressions were introduced in Java 8 to enable **functional programming**. They allow you to treat **functions as first-class citizens**, making your code more concise and readable. Instead of using anonymous inner classes, you can write functional interfaces with simple syntax like `(args) -> expression`.

**Syntax:**

```java
(parameter1, parameter2) -> { // body }
```

Used commonly with **functional interfaces** (interfaces with only one abstract method), like `Runnable`, `Comparator`, or custom ones.

---

### 💻 **Question 1: Basic Lambda Usage**

Write a lambda expression that:

1. Takes two integers.
2. Returns their sum.

**Instructions:**

* Define a functional interface `Adder`.
* Use a lambda to implement the interface.
* Print the result of adding two numbers using the lambda.

**Code**
```
public class Test {
    public static void main(String[] args){
        Adder<Integer, Integer, Integer> func = (n1, n2) -> n1+n2;
        System.out.println(func.add(2, 3));
    }
}

@FunctionalInterface
interface Adder<T,U,R>{

    public R add(T t, U u);
}
```

---

### 🧠 **Topic 2: Functional Interface + `java.util.function` Package**

#### ✅ **Intro:**

Java 8 introduced many built-in functional interfaces in the `java.util.function` package, like:

* `Function<T, R>` – takes one input, returns one output.
* `BiFunction<T, U, R>` – takes two inputs, returns one output.
* `Consumer<T>` – takes one input, returns nothing.
* `Supplier<T>` – takes no input, returns one output.
* `Predicate<T>` – takes one input, returns boolean.

### 🧠 **Topic 3: Function Interface – One Input, One Output**

#### ✅ **Intro:**

The `Function<T, R>` interface is used when:

* You have **one input**.
* You want to **return a result**.

**Common use cases:** Converting types, extracting fields, transforming values.

---

### 🧠 **Topic 4: Predicate Interface – Used for Testing Conditions**

#### ✅ **Intro:**

The `Predicate<T>` interface is used to:

* **Test a condition** on an input.
* Returns a **boolean** result.

**Method:**

```java
boolean test(T t);
```

Commonly used for **filtering** in streams or conditional checks.

---

### 🧠 **Topic 5: Consumer Interface – Takes Input, Returns Nothing**

#### ✅ **Intro:**

`Consumer<T>` is used when:

* You want to **consume** a value (e.g., print, store, send).
* It returns **nothing** (i.e., `void` return type).

**Method:**

```java
void accept(T t);
```

---

### 🔍 **How to Use Other Default Methods in Functional Interfaces**

Most functional interfaces in `java.util.function` come with **default** or **static methods** to support **composition**, like chaining or combining logic.

Let’s look at some examples:

---

#### ✅ `Predicate` Default Methods

```java
Predicate<Integer> isEven = x -> x % 2 == 0;
Predicate<Integer> isPositive = x -> x > 0;

// Combine them
Predicate<Integer> isEvenAndPositive = isEven.and(isPositive);

System.out.println(isEvenAndPositive.test(4));  // true
System.out.println(isEvenAndPositive.test(-2)); // false
```

📌 Other useful methods:

* `and()`
* `or()`
* `negate()`

---

#### ✅ `Function` Default Methods

```java
Function<String, String> trim = str -> str.trim();
Function<String, String> toUpper = str -> str.toUpperCase();

// Compose functions
Function<String, String> trimThenUpper = trim.andThen(toUpper);
System.out.println(trimThenUpper.apply("   java 8   ")); // JAVA 8

Function<String, String> upperThenTrim = toUpper.compose(trim);
System.out.println(upperThenTrim.apply("   java 8   ")); // JAVA 8
```

📌 Key methods:

* `andThen()`: f.andThen(g) means g(f(x))
* `compose()`: f.compose(g) means f(g(x))

---

#### ✅ `Consumer` Default Method

```java
Consumer<String> print = str -> System.out.println("First: " + str);
Consumer<String> shout = str -> System.out.println("Second: " + str.toUpperCase());

Consumer<String> combined = print.andThen(shout);
combined.accept("hello");
```

🧠 Output:

```
First: hello
Second: HELLO
```
---

## ✍️ Mini Challenge Using Predicate, Function, Consumer Together**

**Goal:** Filter → Transform → Act

* `Predicate<String>` → to check if name starts with `"A"`.
* `Function<String, String>` → to convert to uppercase.
* `Consumer<String>` → to print the result.

```java
Predicate<String> predicate = name -> name.startsWith("A");
Function<String, String> function = name -> name.toUpperCase();
Consumer<String> consumer = name -> System.out.println(name);

List<String> names = Arrays.asList("Alice", "Bob", "Andrew", "David", "Ankit");

names.stream()
     .filter(predicate)   // Step 1: Filter names starting with A
     .map(function)       // Step 2: Convert to uppercase
     .forEach(consumer);  // Step 3: Print each
```

✅ Output:

```
ALICE
ANDREW
ANKIT
```

This is a common real-world stream processing pattern!

---
