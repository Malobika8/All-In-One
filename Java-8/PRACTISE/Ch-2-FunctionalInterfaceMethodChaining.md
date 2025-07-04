## 🧠 Functional Interface Method Chaining

---

### ✅ 1. **Predicate Chaining**

#### 📌 Methods:

* `.and(Predicate other)` → returns true if both are true
* `.or(Predicate other)` → returns true if any is true
* `.negate()` → inverts the condition

#### 🔧 Example:

```java
Predicate<String> startsWithA = name -> name.startsWith("A");
Predicate<String> endsWithT = name -> name.endsWith("t");

Predicate<String> combined = startsWithA.and(endsWithT);

System.out.println(combined.test("Ankit"));   // true
System.out.println(combined.test("Amit"));    // false
System.out.println(combined.test("Anil"));    // false
```

---

### ✅ 2. **Function Chaining**

#### 📌 Methods:

* `.andThen(Function after)` → apply first, then apply second
* `.compose(Function before)` → apply second, then apply first

#### 🔧 Example:

```java
Function<String, String> trim = str -> str.trim();
Function<String, String> toUpper = str -> str.toUpperCase();

Function<String, String> trimThenUpper = trim.andThen(toUpper);
Function<String, String> upperThenTrim = toUpper.compose(trim);

System.out.println(trimThenUpper.apply("  hello  ")); // HELLO
System.out.println(upperThenTrim.apply("  hello  ")); // HELLO
```

💡 Use `compose` when the second function should be executed **first**.

---

### ✅ 3. **Consumer Chaining**

#### 📌 Method:

* `.andThen(Consumer other)` → performs both consumers in order

#### 🔧 Example:

```java
Consumer<String> print = str -> System.out.println("Value: " + str);
Consumer<String> shout = str -> System.out.println("Shout: " + str.toUpperCase());

Consumer<String> combined = print.andThen(shout);
combined.accept("hello");
```

🧠 Output:

```
Value: hello
Shout: HELLO
```

---

### ❗ `Supplier` does **not** support chaining — it only has `.get()` and is meant to supply values independently.

---

## 🧪 Mini Exercise: Practice Chaining

Here's your task:

### 💻 **Chain Predicate + Function + Consumer**

1. Filter strings that:

   * Start with `"J"` **AND** end with `"a"` (use `.and()`)
2. Convert them to lowercase (chain `Function`)
3. Print them with a prefix `"Result: "` (chain `Consumer`)

**Input:**

```java
List<String> names = Arrays.asList("Java", "Jaya", "Jenna", "Jira", "Julia");
```

**Code:**

```
public static void main(String[] args){
        Predicate<String> predicate1 = (str) -> str.startsWith("J");
        Predicate<String> predicate2 = (str) -> str.endsWith("a");
        Function<String, String> function = (str) -> str.toLowerCase();
        Consumer<String> consumer = (str) -> System.out.println("Result: " + str);

        List<String> names = Arrays.asList("Java", "Jaya", "Jenna", "Jira", "Julia");

        names.stream()
                .filter(predicate1.and(predicate2))
                .map(function)
                .forEach(consumer);
    }
```

