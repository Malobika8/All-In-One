# What is the purpose of @ExceptionHandler in Spring MVC or REST? How is it different from @ControllerAdvice? When would you use each?

### Sol:

#### `@ExceptionHandler`

> Used inside a **specific controller** to handle exceptions thrown by **that controller’s** methods.

```java
@ExceptionHandler(IllegalArgumentException.class)
public ResponseEntity<String> handleInvalidArg(IllegalArgumentException ex) {
    return ResponseEntity.badRequest().body("Invalid input: " + ex.getMessage());
}
```

#### `@ControllerAdvice`

> Makes exception handling **global across all controllers** — acts like an **aspect** that intercepts exceptions app-wide.

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(Exception.class)
    public ResponseEntity<String> handleAll(Exception ex) {
        return ResponseEntity.status(500).body("Internal Error: " + ex.getMessage());
    }
}
```

| Use Case                                              | Annotation                                |
| ----------------------------------------------------- | ----------------------------------------- |
| Handle exceptions **only in one controller**          | `@ExceptionHandler` inside the controller |
| Handle exceptions **across all controllers** (global) | `@ExceptionHandler` + `@ControllerAdvice` |

> “Spring lets us separate exception handling logic using `@ExceptionHandler`. By combining it with `@ControllerAdvice`, we decouple and centralize error handling for cleaner architecture.”

---

# Create a Spring REST controller that:

1. Has a `GET /divide?a=10&b=0` endpoint
2. Performs division of `a / b`
3. Throws `ArithmeticException` if `b = 0`
4. Handle the exception using a `@ControllerAdvice`-based global handler
5. Return: `400 Bad Request` with message `"Division by zero is not allowed"`

### Sol:

```
@RestController
public class TestController {

    @GetMapping("/divide")
    public String divide(@RequestParam int a, @RequestParam int b) {
        int result = a / b;  // Will throw ArithmeticException if b = 0
        return "Result: " + result;
    }
}
```
```
@ControllerAdvice
public class GlobalException {

    @ExceptionHandler(ArithmeticException.class)
    public ResponseEntity<String> handleArithmetic(ArithmeticException ex) {
        return ResponseEntity
                .badRequest()
                .body("Division by zero is not allowed");
    }
}
```












