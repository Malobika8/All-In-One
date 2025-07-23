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

### ✅ Task:

1. Create a `Calculator` class with an `add` method.
2. Write a test class `CalculatorTest` with `@Test` method.
3. Use `assertEquals` to verify output.


