# What is the purpose of @SessionAttributes in Spring MVC? When would you use it instead of HttpSession? What are its limitations?

### Sol:

> `@SessionAttributes` is used to store **model attributes into the HTTP session**, so they are available across **multiple handler methods** within the same controller.

| Feature         | Details                                                         |
| --------------- | --------------------------------------------------------------- |
| **Scope**       | Controller-specific                                             |
| **Stored in**   | HTTP Session (but accessed via `Model`)                         |
| **Used with**   | `@ModelAttribute`                                               |
| **Common use**  | Multi-step forms, login/session caching in a flow               |
| **Alternative** | `HttpSession` when global access is needed (across controllers) |

#### Limitations:

* Only works with `ModelAttribute`
* Limited to the controller it's declared in
* Doesn’t auto-remove — must manually clear or use `SessionStatus`

> I use `@SessionAttributes` to persist specific model attributes across multiple methods in the same controller, without explicitly dealing with `HttpSession`. For example, in a multi-page form, I can store user info and continue to access it as a model attribute.

---

# Create a controller with:

1. `@SessionAttributes("user")`
2. A method `/step1` that adds a `UserDTO(name, email)` to model
3. A method `/step2` that retrieves the same `user` object from session via `@ModelAttribute`

### Sol:

```java
@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
public class UserDTO {
    private String name;
    private String email;
}
```

```java
@Controller
@SessionAttributes("user")
public class TestController {

    // Step 1: Store user into session via model
    @PostMapping("/step1")
    public String step1(@ModelAttribute("user") UserDTO userDto, Model model) {
        model.addAttribute("user", userDto);
        return "step1complete"; // return view name if using JSP/Thymeleaf
    }

    // Step 2: Retrieve user from session automatically
    @GetMapping("/step2")
    public String step2(@ModelAttribute("user") UserDTO userDto) {
        System.out.println("Name: " + userDto.getName());
        System.out.println("Email: " + userDto.getEmail());
        return "step2complete";
    }
}
```

* `@SessionAttributes("user")` stores `user` in session (via `Model`)
* On next request, Spring injects the `user` session data back into `@ModelAttribute("user")`
* You never deal with `HttpSession` or manually fetching from `Model`

#### If you want to **clear the session**, use:

```java
@GetMapping("/clear")
public String clear(SessionStatus status) {
    status.setComplete(); // removes 'user' from session
    return "sessionCleared";
}
```

> "`@SessionAttributes` stores model attributes in session and auto-injects them in future requests. It’s ideal for multi-step forms within the same controller. For global access, `HttpSession` is more appropriate."

---

# Try the same with HttpSession

### Sol:

```
@RestController
public class TestController {

    // Step 1: Add user to session
    @PostMapping("/step1")
    public String storeInSession(@RequestBody UserDTO userDto, HttpSession session) {
        session.setAttribute("user", userDto);
        return "User saved to session";
    }

    // Step 2: Retrieve user from session
    @GetMapping("/step2")
    public String getFromSession(HttpSession session) {
        UserDTO user = (UserDTO) session.getAttribute("user");
        if (user == null) {
            return "No user found in session";
        }
        return "User from session: " + user.getName() + ", " + user.getEmail();
    }

    // Optional: Clear session
    @GetMapping("/clear")
    public String clearSession(HttpSession session) {
        session.invalidate();
        return "Session cleared";
    }
}
```

---



