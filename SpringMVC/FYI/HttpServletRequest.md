`HttpServletRequest` is an interface in the **Java Servlet API** that represents an **HTTP request** made by a client (usually a web browser) to a **web server**. It is used primarily in **Java web applications** (Servlets, JSP, Spring, etc.) to access request data.

---

### 📌 Key Points:
- Defined in the package: `javax.servlet.http.HttpServletRequest`
- It provides **methods** to access:
  - Request **headers**
  - Request **parameters**
  - Request **body**
  - **Cookies**
  - **Session** information
  - **HTTP method** (GET, POST, etc.)
  - **URL**, **URI**, **context path**, etc.

---

### ✅ Commonly Used Methods:
| Method | Description |
|--------|-------------|
| `getParameter(String name)` | Gets a single request parameter (like form input). |
| `getParameterMap()` | Returns all request parameters as a map. |
| `getHeader(String name)` | Returns the value of a specific header. |
| `getCookies()` | Returns all cookies from the request. |
| `getMethod()` | Returns HTTP method (GET, POST, etc.). |
| `getRequestURI()` | Gets the part of the URL from the domain onward. |
| `getContextPath()` | Returns the context path of the web application. |
| `getSession()` | Returns the current HTTP session. |
| `getInputStream()` / `getReader()` | Reads the raw request body. |

---

### 📘 Example Usage in a Servlet:
```java
protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
    String username = request.getParameter("username");
    String userAgent = request.getHeader("User-Agent");
    HttpSession session = request.getSession();

    System.out.println("Username: " + username);
    System.out.println("User Agent: " + userAgent);
}
```

---

# What can we use instead?

---

### ✅ 1. **Spring's `@RequestParam`, `@RequestHeader`, etc.** (Alternative Style, Not Replacement)

Instead of directly using `HttpServletRequest`, Spring MVC provides **annotations** to extract request data more conveniently:

```java
@GetMapping("/greet")
public String greet(@RequestParam String name, @RequestHeader("User-Agent") String userAgent) {
    return "Hello " + name + ", your browser is " + userAgent;
}
```

➡️ **Advantage:** Cleaner, declarative, less boilerplate than manually calling `request.getParameter()`

---
