## What is JUnit?

**JUnit** is the **default unit testing framework** in Java. Spring Boot uses it under the hood.

#### ➕ Why use it?

* To test individual methods and logic
* To prevent bugs when refactoring
* It integrates easily with Spring Boot

---

## Create a Simple Java Class to Test

Try writing a basic class:

```java
public class Calculator {
    public int add(int a, int b) {
        return a + b;
    }
}
```

Now write this test class (you can use plain Java or in a Spring Boot project):

```java
import org.junit.jupiter.api.Test;
import static org.junit.jupiter.api.Assertions.assertEquals;

public class CalculatorTest {

    @Test
    void testAdd() {
        Calculator calc = new Calculator();
        int result = calc.add(2, 3);
        assertEquals(5, result);
    }
}
```

---

# 🔄 `@BeforeEach` and `@AfterEach` in JUnit 5

These help you:

* **Set up** reusable objects before every test
* **Clean up** after every test if needed

---

## ✅ 1. `@BeforeEach` – Setup Code (Runs Before Every Test)

### Example:

```java
import org.junit.jupiter.api.*;

public class CalculatorTest {

    Calculator calculator;

    @BeforeEach
    void setUp() {
        calculator = new Calculator();
        System.out.println("Setting up Calculator instance...");
    }

    @Test
    void testAdd() {
        Assertions.assertEquals(5, calculator.add(2, 3));
    }

    @Test
    void testAddNegative() {
        Assertions.assertEquals(-1, calculator.add(2, -3));
    }
}
```

### 🧠 What happens here?

* `@BeforeEach` runs **before each `@Test`**
* You **avoid repeating** `Calculator calculator = new Calculator();` in every test

---

## ✅ 2. `@AfterEach` – Tear Down (Runs After Every Test)

You typically use this to **clean up resources** like closing DB connections, files, etc.

### Example:

```java
@AfterEach
void tearDown() {
    System.out.println("Test finished.");
}
```

You’ll see this message **after every test**.

---

## ✅ `@BeforeAll` and `@AfterAll` in JUnit 5

These are like `@BeforeEach` and `@AfterEach`, **but they run only once for the entire test class**, not before/after every test.

---

### 🔁 Comparison Table

| Annotation    | Runs Before/After | How Many Times? | Use Case                             |
| ------------- | ----------------- | --------------- | ------------------------------------ |
| `@BeforeEach` | Each test         | Multiple        | Create fresh object before each test |
| `@AfterEach`  | Each test         | Multiple        | Clean up after each test             |
| `@BeforeAll`  | All tests         | Once            | Expensive setup — e.g. DB connection |
| `@AfterAll`   | All tests         | Once            | Final cleanup, shutdown DB/server    |

---

### ✅ Example:

```java
import org.junit.jupiter.api.*;

@TestInstance(TestInstance.Lifecycle.PER_CLASS)
public class CalculatorTest {

    Calculator calculator;

    @BeforeAll
    public void initAll() {
        System.out.println("🔥 Runs once before all tests");
    }

    @BeforeEach
    public void init() {
        calculator = new Calculator();
        System.out.println("🔁 Runs before each test");
    }

    @Test
    public void testAdd() {
        Assertions.assertEquals(5, calculator.add(2, 3));
    }

    @AfterEach
    public void cleanup() {
        System.out.println("🧹 Runs after each test");
    }

    @AfterAll
    public void tearDownAll() {
        System.out.println("🏁 Runs once after all tests");
    }
}
```

---

## ⚠️ Important Note:

* `@BeforeAll` and `@AfterAll` **must be `static` methods** by default.
* But if you add this on top of the class:

  ```java
  @TestInstance(TestInstance.Lifecycle.PER_CLASS)
  ```

  You can use **non-static** methods (which is more natural in Java).

---

## 🔍 What is `@TestInstance(TestInstance.Lifecycle.PER_CLASS)`?

This annotation tells JUnit **how to manage the lifecycle of your test class instance** — whether it should create:

* **a new instance of the test class for each test method** (default), or
* **a single instance of the test class for all test methods**

---

## 🔁 Two Lifecycles in JUnit 5

| Lifecycle Type         | Description                                                                                                                            |
| ---------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| `PER_METHOD` (default) | A **new object** of the test class is created **for each test method**. All methods must be `static` for `@BeforeAll` and `@AfterAll`. |
| `PER_CLASS`            | A **single test object** is created and reused for **all tests**. You can use **non-static** `@BeforeAll`, `@AfterAll`, fields, etc.   |

---

### ✅ Why use `PER_CLASS`?

Without it, JUnit **requires** `@BeforeAll` and `@AfterAll` methods to be `static`, which feels clunky in object-oriented programming.

With `@TestInstance(PER_CLASS)`, you get:

* Cleaner code — you don’t need `static`
* Ability to reuse `@BeforeAll`/`@AfterAll` logic with instance variables

---

### ✅ Example Without `PER_CLASS` (Default Behavior):

```java
@BeforeAll
static void setupAll() {
    // has to be static!
}
```

---

### ✅ Example With `PER_CLASS`:

```java
@TestInstance(TestInstance.Lifecycle.PER_CLASS)
public class MyTest {

    @BeforeAll
    void setupAll() {
        // ✅ does NOT need to be static anymore
    }
}
```

---

### 🧠 Rule of Thumb:

* If you want to **use instance fields or non-static setup/cleanup logic**, use `PER_CLASS`.
* Otherwise, stick with the default (`PER_METHOD`) — it provides test isolation.

---



