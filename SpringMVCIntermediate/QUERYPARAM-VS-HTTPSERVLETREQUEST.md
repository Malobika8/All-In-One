
### 1. **What is `@RequestParam`?**

`@RequestParam` is a Spring annotation used in controller methods to **extract query parameters (or form data)** from the HTTP request and bind them directly to method parameters.

#### Example:

```java
@GetMapping("/greet")
public String greetUser(@RequestParam String name) {
    return "Hello, " + name;
}
```

If you call:

```
http://localhost:8080/greet?name=John
```

* The `name` parameter (`John`) from the URL will be passed into the method automatically.

✔️ Clean and declarative way to get request parameters
✔️ Spring handles type conversion too (`int`, `double`, etc.)

---

### 2. **What is `HttpServletRequest`?**

`HttpServletRequest` is a **Servlet API object** that represents the entire HTTP request. It gives you low-level access to everything in the request: headers, parameters, session, cookies, body, etc.

#### Example:

```java
@GetMapping("/greet")
public String greetUser(HttpServletRequest request) {
    String name = request.getParameter("name");
    return "Hello, " + name;
}
```

✔️ More flexible and powerful (you can access headers, attributes, session, etc.)
❌ But more verbose and manual — you have to extract and convert parameters yourself.

---

### ✅ **Key Differences:**

| Aspect               | `@RequestParam`                        | `HttpServletRequest`                  |
| -------------------- | -------------------------------------- | ------------------------------------- |
| Level                | Spring-specific (high-level)           | Servlet API (low-level)               |
| Usage                | To bind query/form parameters directly | To manually extract any request data  |
| Type Conversion      | Automatic by Spring                    | Manual (you get everything as String) |
| Verbosity            | Short and clean                        | Verbose (more lines of code)          |
| Access to other data | Only parameters                        | Headers, session, cookies, body, etc. |

---

### ✅ **When to use which?**

* Use **`@RequestParam`** when you just need query/form parameters — it's simpler and more modern in Spring.
* Use **`HttpServletRequest`** when you need deep access (headers, session, cookies, etc.) or are working close to servlet-level APIs.

---

