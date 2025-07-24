## ✅ 1. What is Content Negotiation?

**Content negotiation** is the mechanism by which a **client and server agree on the content format** (e.g., JSON, XML, HTML) for communication.

> The server looks at what the client can accept and responds in the most appropriate format.

---

## ✅ 2. Why is it needed?

Different clients might expect different formats:

* Web browsers want HTML
* REST clients like Postman want JSON
* Older systems may need XML

Spring Boot uses **Content Negotiation** to return the right response format based on the client's preferences.

---

## ✅ 3. How does it work?

Spring Boot uses **HttpMessageConverters** internally.

### Content negotiation can happen using:

| Method            | Description                                   |
| ----------------- | --------------------------------------------- |
| `Accept` Header   | Most common; `Accept: application/json`, etc. |
| URL extension     | E.g., `/user.json` or `/user.xml`             |
| Request parameter | E.g., `/user?format=json`                     |

---

## ✅ 4. Spring Boot – Default Behavior

By default, Spring Boot:

* Uses **`Accept` header** for negotiation.
* Uses **`MappingJackson2HttpMessageConverter`** to convert Java to JSON.
* Uses **`JAXB`** if XML is required.

You **don’t need to configure anything** to support JSON. For XML, you need dependencies.

---

## ✅ 5. Example Code – Basic Setup

### ✅ Step 1: Simple POJO

```java
public class User {
    private String name;
    private int age;

    // Getters and setters
}
```

---

### ✅ Step 2: Controller

```java
@RestController
@RequestMapping("/user")
public class UserController {

    @GetMapping(produces = {MediaType.APPLICATION_JSON_VALUE, MediaType.APPLICATION_XML_VALUE})
    public User getUser() {
        return new User("Malobika", 25);
    }
}
```

---

### ✅ Step 3: XML Support (optional)

To support XML, add this dependency:

```xml
<!-- Add in pom.xml -->
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
</dependency>
```

Or use JAXB:

```xml
<dependency>
    <groupId>javax.xml.bind</groupId>
    <artifactId>jaxb-api</artifactId>
</dependency>
```

Annotate the POJO:

```java
import jakarta.xml.bind.annotation.XmlRootElement;

@XmlRootElement
public class User {
    private String name;
    private int age;
    // Getters and setters
}
```

---

### ✅ Step 4: Test with Curl or Postman

#### JSON

```
GET /user
Accept: application/json
```

#### XML

```
GET /user
Accept: application/xml
```

---

## ✅ 6. Content Negotiation Strategy in Spring

Spring Boot uses `ContentNegotiationStrategy` internally. You can customize it.

### Optionally configure in `WebMvcConfigurer`:

```java
@Configuration
public class WebConfig implements WebMvcConfigurer {

    @Override
    public void configureContentNegotiation(ContentNegotiationConfigurer configurer) {
        configurer
            .favorParameter(true)                // Enable ?format=xml
            .parameterName("format")             // Default: format
            .favorPathExtension(false)           // Disable /user.xml
            .ignoreAcceptHeader(false)           // Enable Accept header
            .defaultContentType(MediaType.APPLICATION_JSON)
            .mediaType("json", MediaType.APPLICATION_JSON)
            .mediaType("xml", MediaType.APPLICATION_XML);
    }
}
```

---

## ✅ 7. Example Requests After Customization

1. `GET /user?format=json` → JSON
2. `GET /user?format=xml` → XML
3. `GET /user` with header `Accept: application/json` → JSON
4. `GET /user` with header `Accept: application/xml` → XML

---

## ✅ 8. HttpMessageConverters in Action

Spring uses these classes internally:

| Format     | Converter                                                                          |
| ---------- | ---------------------------------------------------------------------------------- |
| JSON       | `MappingJackson2HttpMessageConverter`                                              |
| XML        | `Jaxb2RootElementHttpMessageConverter` or `MappingJackson2XmlHttpMessageConverter` |
| Plain Text | `StringHttpMessageConverter`                                                       |

---

## ✅ 9. Disable or Force JSON/XML

You can force the response format by only using one `produces`:

```java
@GetMapping(produces = MediaType.APPLICATION_JSON_VALUE)
```
---

Spring Boot allows you to use **`produces`** and **`consumes`** attributes in `@RequestMapping` (or `@GetMapping`, `@PostMapping`, etc.) to **explicitly declare**:

* `produces`: what content types your method **returns**
* `consumes`: what content types your method **accepts**

## ✅ `produces` – What the method can **return**

### Example: JSON and XML response supported

```java
@GetMapping(
    value = "/user",
    produces = { MediaType.APPLICATION_JSON_VALUE, MediaType.APPLICATION_XML_VALUE }
)
public User getUser() {
    return new User("Malobika", 25);
}
```

### Use Case:

Client says:

```http
Accept: application/xml
```

Then Spring matches it and sends XML, **if possible**.

## ✅ `consumes` – What the method can **accept** as input

### Example: Accepting only JSON

```java
@PostMapping(
    value = "/user",
    consumes = MediaType.APPLICATION_JSON_VALUE
)
public ResponseEntity<String> saveUser(@RequestBody User user) {
    // Save logic
    return ResponseEntity.ok("User saved!");
}
```

### Use Case:

If client sends:

```http
Content-Type: application/json
```

✅ Accepted

If it sends:

```http
Content-Type: application/xml
```

❌ 415 Unsupported Media Type error is returned.

## ✅ Both Together Example

```java
@PostMapping(
    value = "/user",
    consumes = MediaType.APPLICATION_JSON_VALUE,
    produces = MediaType.APPLICATION_XML_VALUE
)
public User createUser(@RequestBody User user) {
    return user;
}
```

This means:

* Request must be JSON (`Content-Type: application/json`)
* Response will be XML (`Accept: application/xml`)

#### Tip:

💬 **Q:** What is the difference between `produces` and `consumes`?

**A:**

* `produces` defines the **response type(s)** the method can return.
* `consumes` defines the **request type(s)** the method can accept in the body.

---

# Common Questions

| Question                                       | Sample Answer                                                                                      |
| ---------------------------------------------- | -------------------------------------------------------------------------------------------------- |
| What is Content Negotiation in Spring Boot?    | It's how the server decides the response format (like JSON or XML) based on client preference.     |
| How does Spring Boot decide the response type? | By checking `Accept` header, request parameter (`?format=json`), or path extension (`/user.json`). |
| How to enable XML support in Spring Boot?      | Add Jackson XML or JAXB dependency, annotate the model with `@XmlRootElement`.                     |
| How to customize content negotiation?          | Implement `WebMvcConfigurer` and override `configureContentNegotiation()`.                         |

---

## Summary

| Feature                       | Support in Spring Boot             |
| ----------------------------- | ---------------------------------- |
| JSON support out of the box   | ✅ Yes                              |
| XML support                   | ❌ Need dependency                  |
| Accept Header                 | ✅ Supported                        |
| Path Extension (`/user.json`) | ❌ Disabled by default              |
| Request Parameter             | ❌ Disabled by default (can enable) |

---

