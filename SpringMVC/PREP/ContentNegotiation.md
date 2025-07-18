## ✅ What Is Content Negotiation?

> **Content negotiation** is the process of determining **what format** (JSON, XML, etc.) to return in the HTTP response — based on what the **client asks for**.

---

### 🔹 How Spring Determines the Response Type:

Spring looks at the request’s **`Accept` header**:

```http
Accept: application/json
```

or

```http
Accept: application/xml
```

Then Spring:

* Picks the right **HttpMessageConverter**
* Converts your Java object accordingly (JSON, XML, or String)

---

### ✅ Rules of Thumb:

| Scenario                                                             | What Happens                              |
| -------------------------------------------------------------------- | ----------------------------------------- |
| Return type is `String`                                              | `StringHttpMessageConverter` → plain text |
| Return type is object (e.g., `User`) and Accept = `application/json` | Uses Jackson → returns JSON               |
| Return type is object and Accept = `application/xml`                 | Uses JAXB (if available) → returns XML    |

---

### 🔧 You can also control content negotiation using:

* `Accept` header (client side)
* `produces` attribute in `@RequestMapping` or `@GetMapping`

```java
@GetMapping(value = "/user", produces = "application/json")
```

---

### ✅ Example:

```java
@GetMapping("/user")
public User getUser() {
    return new User("malobika", "malobika@example.com");
}
```

Client sends:

```
Accept: application/json → returns JSON
Accept: application/xml → returns XML (if JAXB is present)
```

## Summary:

> “Spring uses **HttpMessageConverters** to convert the response based on the `Accept` header. This mechanism is called **Content Negotiation**, and it allows the same endpoint to return JSON, XML, or other formats depending on client preference.”

---

# Write a @RestController that:
- Handles GET /product
- Returns a Product object (with fields: id, name)
- Produces only XML (produces = "application/xml")
- Annotate the Product class properly to enable XML conversion

🧠 Hint:
- You’ll need to use @XmlRootElement from JAXB
- Return an object, not a string

### Sol:

```java
@RestController
class TestController{
    
    @GetMapping(value="/product", produces="application/xml")
    public String test(){
        return new Product(101, "Laptop");
    }
}

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@XmlRootElement
class Product{
    private int id;
    private String name;
}
```

---

# Create a controller that:
- Accepts XML as input (Content-Type: application/xml)
- Uses @RequestBody to map it to a Product object
- Returns confirmation string: "Received product <name>"

### Sol:

```java
@RestController
class TestController{
    
    @PostMapping(value="/product", consumes="application/xml")
    public String test(@RequestBody Product product){
        return "Received product "+product.getName();
    }
}

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
@XmlRootElement
class Product{
    private int id;
    private String name;
}
```

---

# Recap

| Attribute  | Purpose                      |
| ---------- | ---------------------------- |
| `produces` | What type the method returns |
| `consumes` | What type the method accepts |

