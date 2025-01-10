### Checked Exceptions
Checked exceptions are exceptions that are checked at **compile time**. This means that the compiler requires you to handle these exceptions, either by using a `try-catch` block or by declaring them in the method signature with the `throws` keyword.

#### Examples of Checked Exceptions:
1. `IOException`
2. `SQLException`
3. `FileNotFoundException`

#### Characteristics:
- You **must handle** or declare them in your code.
- Typically used for recoverable conditions, like file not found or network issues.

```java
import java.io.*;

public class CheckedExceptionExample {
    public static void main(String[] args) {
        try {
            FileReader file = new FileReader("nonexistentfile.txt");
        } catch (FileNotFoundException e) {
            System.out.println("File not found!");
        }
    }
}
```

---

### Unchecked Exceptions
Unchecked exceptions are exceptions that are checked at **runtime**, meaning the compiler does not force you to handle or declare them. They typically result from programming errors, such as logic or improper use of APIs.

#### Examples of Unchecked Exceptions:
1. `NullPointerException`
2. `ArrayIndexOutOfBoundsException`
3. `ArithmeticException`

#### Characteristics:
- **Not required** to handle or declare them.
- Usually caused by bugs or improper program logic.

```java
public class UncheckedExceptionExample {
    public static void main(String[] args) {
        int[] numbers = {1, 2, 3};
        System.out.println(numbers[3]);  // Throws ArrayIndexOutOfBoundsException
    }
}
```

---

### Key Differences:

| Feature                | Checked Exceptions            | Unchecked Exceptions            |
|------------------------|-------------------------------|----------------------------------|
| Checked at             | Compile time                 | Runtime                         |
| Declaration required   | Yes                          | No                              |
| Examples               | `IOException`, `SQLException` | `NullPointerException`, `ArithmeticException` |
| Use case              | Recoverable conditions        | Programming errors              | 

