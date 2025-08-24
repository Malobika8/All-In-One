# Spring Security — (User Registration & Login in Spring MVC)

---

## 1) Problem With Hardcoded Users

* Earlier: Users were hardcoded in `InMemoryUserDetailsManager` during bean setup.
* Limitation: Not scalable; every new user requires code changes & redeployment.
* Solution: Build **dynamic registration** so users can sign up themselves.

---

## 2) Setting Up Registration Page (JSP + Spring MVC)

* **View Resolver**: Traditional Spring MVC requires manual configuration.

  ```java
  @Configuration
  public class WebConfig {
      @Bean
      public InternalResourceViewResolver viewResolver() {
          InternalResourceViewResolver resolver = new InternalResourceViewResolver();
          resolver.setPrefix("/WEB-INF/views/");
          resolver.setSuffix(".jsp");
          return resolver;
      }
  }
  ```
* **Registration Form (JSP)**

  ```jsp
  <%@ taglib prefix="form" uri="http://www.springframework.org/tags/form" %>

  <h2>Register</h2>
  <form:form action="/register" modelAttribute="user" method="post">
      Username: <form:input path="username"/><br/>
      Password: <form:password path="password"/><br/>
      <input type="submit" value="Register"/>
  </form:form>
  ```
* **DTO for Data Binding**

  ```java
  public class RegistrationDTO {
      private String username;
      private String password;
      // getters & setters
  }
  ```

---

## 3) Spring MVC Controller

* Handles GET + POST for registration.

```java
@Controller
public class RegistrationController {

    private final InMemoryUserDetailsManager userDetailsManager;
    private final PasswordEncoder encoder;

    public RegistrationController(InMemoryUserDetailsManager userDetailsManager, PasswordEncoder encoder) {
        this.userDetailsManager = userDetailsManager;
        this.encoder = encoder;
    }

    @GetMapping("/register")
    public String showForm(Model model) {
        model.addAttribute("user", new RegistrationDTO());
        return "register";
    }

    @PostMapping("/register")
    public String register(@ModelAttribute("user") RegistrationDTO dto) {
        UserDetails user = User.withUsername(dto.getUsername())
                .password(encoder.encode(dto.getPassword()))
                .roles("USER")
                .build();
        userDetailsManager.createUser(user);
        return "redirect:/login";
    }
}
```

---

## 4) Security Configuration

* Permit registration + login pages to all.
* Require authentication elsewhere.

```java
@Bean
SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
    http
        .authorizeHttpRequests(auth -> auth
            .requestMatchers("/register", "/login").permitAll()
            .anyRequest().authenticated()
        )
        .formLogin(Customizer.withDefaults())
        .httpBasic(Customizer.withDefaults());
    return http.build();
}

@Bean
PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
}

@Bean
InMemoryUserDetailsManager userDetailsService() {
    return new InMemoryUserDetailsManager(); // starts empty, users added dynamically
}
```

---

## 5) Handling Challenges

* **CSRF**

  * Default enabled; blocks POST unless CSRF tokens provided.
  * Temporary fix: `http.csrf().disable()` during dev.
* **Circular Dependency**

  * Occurs if beans depend on each other incorrectly.
  * Fix: Use **constructor injection** & avoid mixing config + controller dependencies.
* **Form Submission**

  * Use `POST` for sensitive data (avoid GET exposing params in URL).

---

## 6) Data Binding with DTOs & Spring Form Tags

* Benefits:

  * Cleaner controllers (`@ModelAttribute` auto-binds form fields → DTO).
  * Can pre-populate default values (`model.addAttribute("user", new RegistrationDTO("defaultUser"))`).
  * Two-way binding simplifies both rendering and data collection.

---

## 7) How Users Are Stored & Authenticated

* `InMemoryUserDetailsManager` stores users in-memory (HashMap).
* `createUser()` adds new `UserDetails` at runtime.
* On login → Spring Security calls `loadUserByUsername()` to retrieve user.
* Password comparison uses the configured `PasswordEncoder`.
* Limitation: Non-persistent (lost on restart). Suitable only for demos & prototyping.

---

## 8) Summary of Flow

1. User opens `/register` page → sees JSP form.
2. Submits username/password → bound to `RegistrationDTO`.
3. Controller encodes password & adds new user via `InMemoryUserDetailsManager`.
4. User redirected to `/login` → authenticates with new account.
5. After login → gains access to protected endpoints.

---

