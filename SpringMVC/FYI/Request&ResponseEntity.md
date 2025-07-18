## ✅ What is `ResponseEntity<T>`?

`ResponseEntity<T>` is a class in Spring used to **represent the entire HTTP response**:

* **Status code** (like 200 OK, 404 NOT FOUND, etc.)
* **Headers**
* **Body** (actual response content)

---

### 📦 Why and when to use `ResponseEntity`?

You use it when:

* You want to control the **status code** or **headers** of the response
* You want to customize what gets sent back to the client

---

### 🧪 Example

#### Without ResponseEntity:

```java
@GetMapping("/hello")
public String hello() {
    return "Hello!";
}
```

This returns just the body `"Hello!"` with status `200 OK`.

---

#### With ResponseEntity:

```java
@GetMapping("/hello")
public ResponseEntity<String> hello() {
    return ResponseEntity
           .status(HttpStatus.OK)
           .header("Custom-Header", "MyValue")
           .body("Hello with headers!");
}
```

This returns:

* Body: `"Hello with headers!"`
* Status: `200 OK`
* Header: `Custom-Header: MyValue`

---

## ✅ What is `RequestEntity<T>`?

`RequestEntity<T>` is used to **access the entire HTTP request**:

* **Headers**
* **Body**
* **HTTP Method**
* **URI**

It's rarely used unless you **need full control over the incoming request**, not just the body.

---

### 🧪 Example with RequestEntity:

```java
@PostMapping("/data")
public ResponseEntity<String> handleData(RequestEntity<String> request) {
    HttpHeaders headers = request.getHeaders();
    String body = request.getBody();

    System.out.println("Headers: " + headers);
    System.out.println("Body: " + body);

    return ResponseEntity.ok("Received your request");
}
```

This lets you examine the request headers, body, method, etc.

---

## ✅ Summary

| Class               | Purpose                                    | Common Use Case                        |
| ------------------- | ------------------------------------------ | -------------------------------------- |
| `ResponseEntity<T>` | Full control over HTTP **response**        | Set status codes, headers, return data |
| `RequestEntity<T>`  | Full access to HTTP **request** (advanced) | Inspect headers, body, method, URI     |

---

# ✅ 1. `HttpServletRequest` & `HttpServletResponse`

These come from the **Servlet API**, and Spring allows you to use them when needed.

### 📦 Use when:

* You need **low-level control**
* You're dealing with **legacy code**, **filters**, or **servlets**
* You want to do things like session handling, manually reading query params, or writing to response output stream

### 🧪 Example:

```java
@GetMapping("/test")
public void test(HttpServletRequest request, HttpServletResponse response) throws IOException {
    String userAgent = request.getHeader("User-Agent");
    response.getWriter().write("User-Agent: " + userAgent);
}
```

---

## ✅ 2. `RequestEntity` & `ResponseEntity`

These are **higher-level, Spring-style abstractions** built on top of the Servlet API.

### 📦 Use when:

* You want **object-oriented, declarative access** to the request/response
* You want to **leverage Spring's features** like message converters, clean REST APIs
* You want to **return JSON/XML/body + status code + headers** in a neat way

### 🧪 Cleaner alternative:

```java
@GetMapping("/test")
public ResponseEntity<String> test(RequestEntity<String> request) {
    String userAgent = request.getHeaders().getFirst("User-Agent");
    return ResponseEntity.ok("User-Agent: " + userAgent);
}
```

---

## ✅ Summary Table

| Feature                           | `HttpServletRequest` / `HttpServletResponse` | `RequestEntity` / `ResponseEntity` |
| --------------------------------- | -------------------------------------------- | ---------------------------------- |
| Origin                            | Servlet API (javax.servlet)                  | Spring Framework                   |
| Level                             | Low-level                                    | High-level                         |
| Headers, URI, Method, Body        | Manual access                                | Available via simple APIs          |
| Spring-friendly & testable        | ❌ Not as clean                               | ✅ Very clean & testable            |
| Status code / headers in response | Manual (`response.setStatus`)                | Easy via builder methods           |

---

### 👉 When to use what?

* Use `HttpServletRequest/Response` when doing **custom servlet logic or filters**
* Prefer `RequestEntity/ResponseEntity` when building **REST APIs or Spring MVC controllers**
