# QUESTION

1. What are the main differences between HTTP methods: **GET**, **POST**, **PUT**, and **DELETE** in REST APIs?
2. Which ones are **idempotent** and what does that mean?
3. When would you use:

   * `POST` vs `PUT`?
   * `PUT` vs `PATCH`?

### Sol:

#### `GET`

* Used to **retrieve** data
* Must be **safe** (does not modify server state)
* ✅ **Idempotent**

#### `POST`

* Used to **create** new resources
* Can also be used to **trigger server-side logic**
* ❌ Not idempotent (posting the same data twice = 2 records)

#### `PUT`

* Used to **create or update** a resource at a specific URI
* Replaces the entire resource
* ✅ **Idempotent**
  (sending the same `PUT` request multiple times → same result)

#### `DELETE`

* Used to **delete** a resource
* ✅ **Idempotent**
  (deleting the same thing twice doesn’t change the result)

#### `PATCH` (Bonus)

* Used to **partially update** a resource
* ❓ Idempotency is **not guaranteed** — depends on implementation

#### What is Idempotency?

> An operation is **idempotent** if making the same request **multiple times has the same effect as once**.

| Method   | Idempotent? | Why                                           |
| -------- | ----------- | --------------------------------------------- |
| `GET`    | ✅ Yes       | Always returns same resource (doesn’t modify) |
| `POST`   | ❌ No        | Creates new entries each time                 |
| `PUT`    | ✅ Yes       | Overwrites the same resource                  |
| `DELETE` | ✅ Yes       | Deletes once → further deletes do nothing     |

#### Summary:

> “In REST, `POST` is used to create, `PUT` to update or replace, `GET` to fetch, and `DELETE` to remove. Only `POST` is non-idempotent. Idempotent methods help make APIs safe and retryable.”

---

# Write a REST controller with these endpoints:

1. `GET /product/{id}` – returns `"Fetching product with ID: X"`
2. `POST /product` – accepts `Product` in JSON, returns `"Created product X"`
3. `PUT /product/{id}` – accepts updated `Product` and returns `"Updated product X"`
4. `DELETE /product/{id}` – returns `"Deleted product X"`

### Sol:

```
@RestController
class TestController{
    
    @GetMapping("/product/{id}")
    public String get(@PathVariable("id") int id){
        return "Fetching product with ID: "+id;
    }
    @PostMapping(value="/product", consumes="application/json")
    public String post(@RequestBody Product product){
        return "Created product "+product;
    }
    @PutMapping("/product/{id}")
    public String put(@PathVariable("id") int id, @RequestBody Product product){
        //code to update product based on product id
        return "Updated product "+product;
    }
    @DeleteMapping("/product/{id}")
    public String delete(@PathVariable("id") int id){
        //code to delete product based on product id
        return "Deleted product "+product;
    }
}

@Getter
@Setter
@AllArgsConstructor
@NoArgsConstructor
class Product{
    int id;
    String name;
}
```

---




