## ✅ Quick Intro: Exception Handling in Spring Boot

Spring Boot provides multiple ways to handle exceptions globally or locally.

### 🔹 1. Local Exception Handling

Handled directly inside a controller method using `try-catch`.

### 🔹 2. Global Exception Handling

Using `@ControllerAdvice` + `@ExceptionHandler`.

### 🔹 3. ResponseEntityExceptionHandler

Extend this class to override default Spring exceptions (e.g., 404, 400, etc.).

---

# Questions
## 1. **What is `@ControllerAdvice` in Spring Boot? How is it different from `@ExceptionHandler`?**

### Sol:

#### `@ControllerAdvice` vs `@ExceptionHandler`

| Annotation          | Purpose                                                 | Scope                                                                |
| ------------------- | ------------------------------------------------------- | -------------------------------------------------------------------- |
| `@ControllerAdvice` | Declares a **global exception handler** (and more)      | Applies to all or selected controllers                               |
| `@ExceptionHandler` | Declares a method that **handles a specific exception** | Can be used inside controller or globally (with `@ControllerAdvice`) |

#### 🔹 Use Cases of `@ControllerAdvice`:

1. Global **exception handling**
2. Global **model attributes** via `@ModelAttribute`
3. Global **data binders** via `@InitBinder`

#### ✅ Example:

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> handleUserNotFound(UserNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}
```

This handles `UserNotFoundException` **from any controller**.

---

## 2. Create a `UserNotFoundException` class, and a global handler using `@ControllerAdvice` that returns:

* HTTP 404
* Response body: `"User not found with id: <id>"`

Assume a controller method like:

```java
@GetMapping("/users/{id}")
public User getUser(@PathVariable Long id) {
   // if not found, throw new UserNotFoundException(id)
}
```

Create:

1. The exception class
2. The global handler method inside a `@ControllerAdvice` class

### Sol:

#### 1️⃣ `UserNotFoundException` 

```java
public class UserNotFoundException extends RuntimeException {

    public UserNotFoundException(Long id) {
        super("User not found with id: " + id);
    }
}
```

#### 2️⃣ `GlobalException`

```java
@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<String> userNotFoundException(UserNotFoundException ex) {
        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(ex.getMessage());
    }
}
```

#### 3️⃣ `UserController`

```java
@RestController
public class UserController {

    private List<User> users = List.of(
        new User(1L, "Alice", "alice@example.com"),
        new User(2L, "Bob", "bob@example.com")
    );

    @GetMapping("/users/{id}")
    public User getUser(@PathVariable Long id) {
        return users.stream()
            .filter(user -> user.getId().equals(id))
            .findFirst()
            .orElseThrow(() -> new UserNotFoundException(id)); // ✅ Fixed
    }
}
```

---

## 3. **How would you return a structured JSON error response like this?**

```json
{
  "timestamp": "2025-07-09T10:15:30",
  "status": 404,
  "error": "Not Found",
  "message": "User not found with id: 10",
  "path": "/users/10"
}
```

Give your approach or write code (e.g., custom error response class + modified exception handler).

### Sol:

#### What `@RestController` Does

* Combines `@Controller + @ResponseBody`
* Any method inside it that returns an object will be automatically converted to JSON using **Jackson**

```java
@RestController
public class UserController {
    @GetMapping("/hello")
    public Map<String, String> hello() {
        return Map.of("message", "Hi");
    }
}
```

✅ Output:

```json
{ "message": "Hi" }
```

####❗ What about exceptions?

If you return a plain `String` in your global exception handler:

```java
return ResponseEntity.status(404).body("User not found");
```

➡️ You'll get plain text:
`User not found`

#### If you want a structured JSON like:

```json
{
  "timestamp": "...",
  "status": 404,
  "message": "User not found with id: 10",
  "path": "/users/10"
}
```
You will need to:

1. Create a **custom error response DTO**
2. Return that from your `@ExceptionHandler`

---

## 4. Create `ErrorResponse` class with fields:

* `timestamp` (LocalDateTime)
* `status` (int)
* `message` (String)
* `path` (String)

Modify `@ExceptionHandler` to return this object as JSON.

### Sol:

```java
public class UserNotFoundException extends RuntimeException {

    public UserNotFoundException(Long id) {
        super("User not found with id: " + id);
    }
}
```

#### `ErrorResponse` – `LocalDateTime` or `String`

```java
import lombok.*;
import java.time.LocalDateTime;

@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class ErrorResponse {
    private LocalDateTime timestamp;
    private int status;
    private String error;
    private String message;
    private String path;
}
```

#### GlobalException Handler – `Time.getTimeStamp()` and real request path

```java
import org.springframework.web.context.request.WebRequest;
import java.time.LocalDateTime;

@ControllerAdvice
public class GlobalExceptionHandler {

    @ExceptionHandler(UserNotFoundException.class)
    public ResponseEntity<ErrorResponse> userNotFoundException(
            UserNotFoundException ex,
            HttpServletRequest request) {

        ErrorResponse error = new ErrorResponse(
            LocalDateTime.now(),
            HttpStatus.NOT_FOUND.value(),
            HttpStatus.NOT_FOUND.getReasonPhrase(),
            ex.getMessage(),
            request.getRequestURI()
        );

        return ResponseEntity.status(HttpStatus.NOT_FOUND).body(error);
    }
}
```

> ✅ `request.getRequestURI()` gives dynamic path like `/users/5`

```json
{
  "timestamp": "2025-07-09T12:30:00",
  "status": 404,
  "error": "Not Found",
  "message": "User not found with id: 5",
  "path": "/users/5"
}
```

```java
@RestController
public class UserController {

    private List<User> users = List.of(
        new User(1L, "Alice", "alice@example.com"),
        new User(2L, "Bob", "bob@example.com")
    );

    @GetMapping("/users/{id}")
    public User getUser(@PathVariable Long id) {
        return users.stream()
            .filter(user -> user.getId().equals(id))
            .findFirst()
            .orElseThrow(() -> new UserNotFoundException(id));
    }
}
```

---

## 4. `MethodArgumentNotValidException`

#### ❗Scenario:

You have this endpoint:

```java
@PostMapping("/users")
public User createUser(@RequestBody @Valid User user) { ... }
```

If the client sends invalid data (e.g., empty name), you’ll get `MethodArgumentNotValidException`.

---

#### 🔹 Coding Task:

1. Add validation to your `User` class using `@NotBlank` and `@Email`.
2. Handle `MethodArgumentNotValidException` in your `@ControllerAdvice` and return a structured JSON like:

```json
{
  "timestamp": "2025-07-09T14:30:00",
  "status": 400,
  "errors": [
    "name: must not be blank",
    "email: must be a valid email"
  ],
  "path": "/users"
}
```

### Sol:



