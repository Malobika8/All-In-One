# QUESTION

Which of the following is the **best practice** in REST URI design? Why?

A. `/getUserById?id=1`
B. `/user?id=1`
C. `/users/1`
D. `/users?id=1`

### Ans

/users/1
REST favors resource-oriented URIs over action-oriented ones.

---

# Match each use case to the correct HTTP status code:

- A resource was created successfully
- Resource updated, nothing to return
- Request data was invalid
- Requested ID doesn’t exist
- Server crashed during processing
- Request processed successfully, data returned

#### Options:

- 200
- 201
- 204
- 400
- 404
- 500

### Ans

| Use Case                                         | Status Code                       | Explanation                       |
| ------------------------------------------------ | --------------------------------- | --------------------------------- |
| 1. A resource was created successfully           | ✅ **201 (Created)**               | Indicates new resource created    |
| 2. Resource updated, nothing to return           | ❌ Should be **204 (No Content)**  | PUT succeeded but no body         |
| 3. Request data was invalid                      | ❌ Should be **400 (Bad Request)** | Invalid input from client         |
| 4. Requested ID doesn’t exist                    | ✅ **404 (Not Found)**             | Resource doesn’t exist            |
| 5. Server crashed during processing              | ✅ **500 (Internal Server Error)** | Something went wrong on server    |
| 6. Request processed successfully, data returned | ✅ **200 (OK)**                    | Normal success with response body |

---

# Why do we need versioning in REST APIs? And what are the pros/cons of URI-based versioning vs Header-based versioning?

### Sol:

> When APIs evolve over time (new fields, logic, format), we don’t want to break existing clients. Versioning lets us **serve both old and new clients** simultaneously.

Examples:

* v1 returns basic fields
* v2 returns additional fields or new format

| Strategy                | Example                                   | Pros                     | Cons                            |
| ----------------------- | ----------------------------------------- | ------------------------ | ------------------------------- |
| **URI**                 | `/v1/products`                            | Easy, visible, cacheable | Breaks URI structure purity     |
| **Request Param**       | `/products?version=1`                     | Easy to implement        | Clutters query params           |
| **Header**              | `X-API-VERSION: 1`                        | Clean URI                | Hard to test/debug from browser |
| **Content Negotiation** | `Accept: application/vnd.company.v1+json` | Flexible, standard       | Complex to implement/test       |

> “Versioning helps avoid breaking clients when APIs evolve. URI versioning is simple and widely used, but header/content-based strategies are more flexible and REST-pure.”

---

# Create a Spring REST controller that:

1. Exposes `/v1/product` → returns `"Product v1"`
2. Exposes `/v2/product` → returns `"Product v2 with extra fields"`

### Sol:

```
@RestController
public class TestController {

    @GetMapping("/v1/product")
    public ProductV1 getV1() {
        return new ProductV1(1, "max");
    }

    @GetMapping("/v2/product")
    public ProductV2 getV2() {
        return new ProductV2(1, "max", "lanka");
    }
}
```
```
@Getter @Setter @AllArgsConstructor
class ProductV1 {
    private int id;
    private String name;
}

@Getter @Setter @AllArgsConstructor
class ProductV2 {
    private int id;
    private String name;
    private String address;
}
```

---

# ✅ Header-Based Versioning in Spring

> We use **custom headers** like `X-API-VERSION` to distinguish API versions.

#### How it works:

You define the same URI (e.g. `/product`) but check the header to decide which version to return.

---

# Coding – Header-based versioning

Create a controller that exposes a single URI `/product`, but:

* If header `X-API-VERSION = 1`, return:
  `ProductV1(id, name)`

* If header `X-API-VERSION = 2`, return:
  `ProductV2(id, name, address)`

### Sol:

```
@RestController
public class TestController {

    @GetMapping("/product")
    public Object getProduct(@RequestHeader("X-API-VERSION") String version) {
        if ("1".equals(version)) {
            return new ProductV1(1, "max");
        } else if ("2".equals(version)) {
            return new ProductV2(1, "max", "lanka");
        } else {
            return new ErrorResponse("Unsupported API version: " + version);
        }
    }
}
```
```
@Getter @Setter @AllArgsConstructor
class ProductV1 {
    private int id;
    private String name;
}

@Getter @Setter @AllArgsConstructor
class ProductV2 {
    private int id;
    private String name;
    private String address;
}

@Getter @Setter @AllArgsConstructor
class ErrorResponse {
    private String error;
}
```

---




