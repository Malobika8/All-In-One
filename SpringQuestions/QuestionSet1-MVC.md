## 1. DispatcherServlet – Spring MVC Request Flow

### Sol:

1. **Client sends a request**
2. **`DispatcherServlet` intercepts it** (registered in `web.xml` or auto-configured via Spring Boot)
3. It consults the **HandlerMapping** to find the appropriate **Controller/Handler method**
4. The matched method is executed via a **HandlerAdapter**
5. The controller returns a `ModelAndView` (in classic MVC) or just the object (in REST)
6. The result is sent to a **ViewResolver** (for JSP, Thymeleaf) or **HttpMessageConverter** (for JSON/XML)
7. The **response** is sent back to the client

#### 🔸 Bonus Concepts

* `@RestController` skips ViewResolvers; it directly returns body using `HttpMessageConverter`
* Handler mappings are based on `@RequestMapping`, `@GetMapping`, etc.

---

## 2. Spring MVC – **What is the difference between `@Controller` and `@RestController`?**
Give one real-world example where you'd prefer each.

### Sol:
#### ✅ `@Controller` vs `@RestController`

| Feature                  | `@Controller`                          | `@RestController`                    |
| ------------------------ | -------------------------------------- | ------------------------------------ |
| Response Type            | Returns **View** (e.g., JSP/Thymeleaf) | Returns **Response Body** (JSON/XML) |
| Use with `@ResponseBody` | Needed to return raw data              | Already implied                      |
| Suitable for             | Traditional web apps (UI rendering)    | REST APIs (data services)            |
| View Resolution          | Goes through **ViewResolver**          | Uses **HttpMessageConverter**        |

✅ `@RestController = @Controller + @ResponseBody`

---

#### 🔸 Real-World Use Cases

* **`@Controller`**: A JSP-based web app where users interact via HTML pages.

  * Example: Login page that returns `login.jsp`.
* **`@RestController`**: A microservice returning JSON to a frontend (e.g., React, Angular).

  * Example: `/api/users` returns JSON list of users.

---

## 3. Spring MVC – Coding Challenge 1: Create a REST controller class `UserController` with:

* Endpoint: `GET /users`
* It should return a list of dummy users like: `["Alice", "Bob", "Charlie"]`

### Sol:

```java
@RestController
public class UserController {

    @GetMapping("/users")
    public List<String> users() {
        return Arrays.asList("Alice", "Bob", "Charlie");
    }
}
```

No extra annotations needed since:

* `@RestController` handles both component scanning (`@Controller`) and response serialization (`@ResponseBody`)
* `@GetMapping("/users")` maps GET requests directly

---


## 4. Spring MVC – Coding Challenge: Modify `UserController` to:

* Add a new endpoint `GET /users/{id}`
* Return the name based on ID:

  * 0 → Alice
  * 1 → Bob
  * 2 → Charlie
* Return `"User not found"` if index is invalid.

### Sol:

```java
@RestController
public class UserController {

    private final List<String> list = Arrays.asList("Alice", "Bob", "Charlie");

    @GetMapping("/users")
    public List<String> users() {
        return list;
    }

    @GetMapping("/users/{id}")
    public String user(@PathVariable("id") int id) {
        if (id < 0 || id >= list.size()) {
            return "User not found";
        }
        return list.get(id);
    }
}
```

---

### 🔎 Tip:

> “What if I try `/users/-1` or `/users/abc`?”

* **Negative numbers** are handled in your `if` condition ✅
* **Non-integer path variables** will cause `400 Bad Request`, as Spring tries to convert `abc` to `int`. You can handle it globally using `@ControllerAdvice`.

---




