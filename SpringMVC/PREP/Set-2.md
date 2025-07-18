# How does Spring MVC handle form submissions?
- What annotations or objects do you use to bind form data?
- How do you perform validation on form input?
- What is the role of BindingResult?

### Sol:

#### How to Bind Form Data?

> Use `@ModelAttribute` to bind form fields to a POJO (DTO).

Example:

```java
@PostMapping("/register")
public String registerUser(@ModelAttribute User user) {
    // fields auto-populated from form input names
}
```

#### How to Validate Form Data?

1. Annotate fields in the DTO with **validation constraints**:
   * `@NotEmpty`, `@Email`, `@Min`, `@Max`, etc.
2. Use `@Valid` or `@Validated` on the controller method parameter
3. Accept a `BindingResult` immediately **after** the validated object to capture validation errors

#### Example:

```java
@PostMapping("/register")
public String registerUser(@Valid @ModelAttribute User user, BindingResult result) {
    if (result.hasErrors()) {
        return "registrationForm"; // back to form with errors
    }

    return "success";
}
```

* `@Valid` triggers validation
* `BindingResult` captures field errors, form errors, etc.

#### What is `BindingResult`?

* Spring auto-populates it after validation
* You can check: `result.hasErrors()`
* You can loop through errors:

```java
for (FieldError error : result.getFieldErrors()) {
    System.out.println(error.getField() + ": " + error.getDefaultMessage());
}
```

> “Spring integrates with JSR-303/380 validation APIs (Hibernate Validator, Jakarta Validation). We annotate our model with constraints and validate automatically during form binding using `@Valid` and `BindingResult`.”

---

# Create a Spring MVC controller that:

1. Displays a registration form using `@GetMapping("/register")`
2. Accepts form POST using `@PostMapping("/register")`
3. Binds to a `UserDTO` class with:
   * `@NotEmpty String name`
   * `@Email String email`
4. If validation fails → redisplay form
   If validation succeeds → redirect to `"success"`

### Sol:

```java
@Controller
public class TestController {

    @GetMapping("/register")
    public String showForm(Model model) {
        model.addAttribute("userDTO", new UserDTO());
        return "showForm";
    }

    @PostMapping("/register")
    public String submitForm(@Valid @ModelAttribute("userDTO") UserDTO userDto, BindingResult bindingResult) {
        if (bindingResult.hasErrors()) {
            return "showForm"; // Back to form with error messages
        }
        return "success";
    }
}
```
```java
import lombok.*;
import jakarta.validation.constraints.*;

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
public class UserDTO {

    @NotEmpty(message = "Name cannot be empty")
    private String name;

    @Email(message = "Invalid email format")
    private String email;
}
```

In Spring MVC, we handle form binding using @ModelAttribute and validate it using @Valid. BindingResult lets us capture and react to validation errors without throwing exceptions.

---



