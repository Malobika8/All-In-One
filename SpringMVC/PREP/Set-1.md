# What is the DispatcherServlet in Spring MVC?
- What is its role?
- How does request flow work through it?
- What components does it coordinate with?

### Sol:

> It’s the **Front Controller** in the **Spring MVC architecture** — a single entry point for all incoming HTTP requests.

#### Request Flow in Spring MVC:

```
Browser --> DispatcherServlet --> HandlerMapping --> Controller --> ViewResolver --> Response
```

#### Detailed Step-by-Step Flow:

1. **Client sends HTTP request** → `/user/123`
2. **`DispatcherServlet`** receives the request
3. Uses a **HandlerMapping** to find the correct controller/method
4. Calls the matched **Controller method**
5. Controller returns:
   * A **View name** (for MVC)
   * Or **ResponseBody** (for REST)
6. If it's a view:
   * **ViewResolver** resolves the view (e.g. JSP, Thymeleaf)
   * Dispatcher renders view with data
7. If it's REST:
   * Response is sent as JSON/XML using **MessageConverters**

#### DispatcherServlet Coordinates With:

| Component             | Role                                      |
| --------------------- | ----------------------------------------- |
| **HandlerMapping**    | Finds correct controller/method           |
| **HandlerAdapter**    | Invokes handler method                    |
| **ViewResolver**      | Resolves logical view name to actual view |
| **MessageConverter**  | Converts objects to JSON/XML for REST     |
| **ExceptionResolver** | Handles exceptions globally               |
| **LocaleResolver**    | Handles i18n (optional)                   |

> “DispatcherServlet is the core of Spring MVC — it acts as the front controller, routing requests to appropriate handler methods, coordinating view resolution or REST responses using various pluggable components.”

---

# Write a simple `@Controller` class that:
* Handles GET `/home`
* Returns a JSP view named `"homepage"`
* Adds an attribute `"message": "Welcome!"` to the model

### 

```
@Controller
public class TestController{
    
    @GetMapping("/home")
    public String homePage(Model model){
        model.addAttribute("message", "Welcome!");
        
        return "homepage";
    }
}
```

---

# What’s the difference between @Controller and @RestController?

## Sol:

`@Controller` vs `@RestController`

| Aspect       | `@Controller`                               | `@RestController`                   |
| ------------ | ------------------------------------------- | ----------------------------------- |
| Role         | Handles **web views** (like JSP, Thymeleaf) | Handles **REST APIs**               |
| Return Value | View name (e.g., `"homepage"`)              | Data (e.g., `User`, `String`, etc.) |
| Uses         | `ViewResolver`                              | `HttpMessageConverters`             |
| Sends HTML?  | ✅ Yes (via JSP, etc.)                       | ❌ No (sends JSON/XML/text)          |
| Built from   | Just `@Controller`                          | `@Controller + @ResponseBody`       |

#### `@RestController = @Controller + @ResponseBody`

This means:

* Every method in `@RestController` automatically behaves like it's annotated with `@ResponseBody`
* No need to use `@ResponseBody` on each method

#### Example:

```java
@RestController
public class UserRestController {

    @GetMapping("/user")
    public User getUser() {
        return new User("malobika", "Kolkata");
    }
}
```

→ Spring uses **MessageConverter** (e.g., Jackson) to serialize the `User` object to JSON.

---

# Write a `@RestController` class that:
* Handles `GET /api/greet`
* Returns the plain text: `"Hello from REST!"`
* Uses no model or view

### Sol:

```
@RestController
public class TestController{
    
    @GetMapping("/api/greet")
    public String homePage(){
        
        return "Hello from REST!";
    }
}
```

---

# What’s the difference between: @RequestParam, @PathVariable, @ModelAttribute

## Sol:

### 1. `@RequestParam`

> Used to extract **query parameters** from the URL, or **form fields (key-value pairs)**.

🧪 Example URL:

```
GET /search?query=spring
```

```java
@GetMapping("/search")
public String search(@RequestParam String query) {
    return "You searched for: " + query;
}
```

### 2. `@PathVariable`

> Used to extract values **embedded in the URI path itself** — often used for IDs or dynamic path segments.

🧪 Example URL:

```
GET /user/101
```

```java
@GetMapping("/user/{id}")
public String getUser(@PathVariable int id) {
    return "User ID: " + id;
}
```

### 3. `@ModelAttribute`

> Used to **bind form data to a Java object** automatically, and also add it to the model for view rendering.

#### When Receiving Form Data:

```java
@PostMapping("/register")
public String register(@ModelAttribute User user) {
    // User fields are populated from form input
    return "success";
}
```

🧠 Spring automatically:

* Creates the `User` object
* Sets its fields using matching form input names
* Adds it to the model (for JSP access)

#### Summary:

| Annotation        | Source of Data           | Used In                               |
| ----------------- | ------------------------ | ------------------------------------- |
| `@RequestParam`   | Query param / form field | Simple values (e.g., `?page=1`)       |
| `@PathVariable`   | URI path                 | RESTful URIs (e.g., `/user/{id}`)     |
| `@ModelAttribute` | Form fields → POJO       | Full form data binding (e.g., `User`) |

---

# Write a controller that:
* Handles `GET /user?id=100`
* Uses `@RequestParam` to get the ID
* Returns `"User ID is: 100"`

Then, modify it to use `@PathVariable` with a URI like `/user/100` instead.

### Sol:

```

@RestController
public class TestController{
    
    @GetMapping("/user")
    public String getUser(@RequestParam("id") int id){
        
        return "User id is " + id;
    }
}

@RestController
public class TestController{
    
    @GetMapping("/user/{id}")
    public String getUser(@PathVariable("id") int id){
        
        return "User id is " + id;
    }
}
```

---

# What are @RequestBody and @ResponseBody used for? How are they different from @ModelAttribute? In what case do we use @RequestBody instead of @RequestParam?

### Sol:

#### `@ResponseBody`

* Applied on methods (or implicitly via `@RestController`)
* Tells Spring to **write the return value directly into the HTTP response body**
* Uses **MessageConverters** (like Jackson) to serialize objects to **JSON**, **XML**, or **plain text**

```java
@GetMapping("/hello")
@ResponseBody
public String hello() {
    return "Hello";  // → Sent directly as plain text
}
```

#### `@RequestBody`

* Applied on method parameters
* Tells Spring to **read the entire HTTP request body** and convert it to a Java object (usually JSON → POJO)
* Common in REST APIs (POST, PUT)

```java
@PostMapping("/register")
public String register(@RequestBody User user) {
    return "User: " + user.getName();
}
```

> 💡 Spring uses `MappingJackson2HttpMessageConverter` to convert the JSON request body into the `User` object.

#### `@ModelAttribute`

* Also used for mapping request data → POJO
* BUT: it uses **form fields (key-value pairs or query params)** — not raw JSON
* Adds the object to **Model**, useful in MVC apps (JSP/Thymeleaf)

```java
@PostMapping("/register")
public String register(@ModelAttribute User user) {
    return "User: " + user.getName(); // plus it’s available in the JSP
}
```

| Annotation        | Data Source       | Format Expected | Common Use Case             |
| ----------------- | ----------------- | --------------- | --------------------------- |
| `@RequestBody`    | HTTP Request Body | JSON/XML        | REST APIs (POST/PUT)        |
| `@ModelAttribute` | Form fields / URL | key-value pairs | Web forms (JSP, HTML forms) |
| `@ResponseBody`   | Java object       | → Response body | REST API output             |

* `@RequestBody` works **only** for **JSON/XML payloads**
* For form submissions, if `Content-Type` is `application/x-www-form-urlencoded`, you should use `@ModelAttribute`

#### Rule of Thumb:

| Use This          | When Data Comes As                           |
| ----------------- | -------------------------------------------- |
| `@RequestParam`   | Query param or single value (`?id=5`)        |
| `@ModelAttribute` | Form field (submitted via HTML form)         |
| `@RequestBody`    | JSON/XML body (from API client/Postman/etc.) |

---

# Create a `@RestController` that:

* Accepts a `POST /user`
* Takes a JSON body with `name` and `email`
* Maps it to a `User` object using `@RequestBody`
* Returns: `"User <name> with email <email> created"`

### Sol:

```java
@RestController
class TestController{
    
    @PostMapping("/user")
    public String test(@RequestBody InfoDTO infoDto){
        return "User "+infoDto.getName()+" with email "+infoDto.getEmail()+" created";
    }
}

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
class InfoDTO{
    private String name;
    private String email;
}
```

---

# What will happen if two controller methods have **exact same URI and HTTP method**, but their parameter lists are different? Will Spring allow this or throw an error? Why?

#### Example:

```java
@GetMapping("/test")
public String method1(@RequestParam String name) { ... }

@GetMapping("/test")
public String method2(@RequestParam int age) { ... }
```

### Sol:

Suppose the request looks like, `/test?name=lila` or `/test?age=9`, **Spring MVC will not be able to resolve the method just based on the type of the query parameter**.

Spring’s `HandlerMapping` doesn’t look at query param **types** when deciding which method to call. It looks at:

* The URL path (e.g., `/test`)
* The HTTP method (`GET`, `POST`, etc.)
* Any explicit parameter mapping annotations (`@RequestParam`, `@PathVariable`, etc.)

If both methods map to the same path and HTTP verb without distinct `@RequestParam` constraints (like `params="name"` vs `params="age"`), **Spring will throw an `IllegalStateException: Ambiguous mapping`** during application startup — **not at runtime** — because the mappings are indistinguishable.

If you want them to be different, you’d do something like:

```java
@GetMapping(value = "/test", params = "name")
public String testWithName(@RequestParam String name) { ... }

@GetMapping(value = "/test", params = "age")
public String testWithAge(@RequestParam int age) { ... }
```

Now `HandlerMapping` can unambiguously decide which method to pick.

---







