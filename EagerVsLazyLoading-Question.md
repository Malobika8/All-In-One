# Scenario

### Note that *get()* is eager by default & *load()* lazy.

Consider a class.

```
@Entity
public class Student {
    @Id
    private int studentId;
    private String name;

    @OneToMany
    private List<Address> addressList;
}
```

When we fetch name and id, it doesn't get list of addresses in the select query while using get(). 
However, when we try to fetch addresses explicitly, the same is selected in the select query. 

### How is get() eager loading in that case? It should ideally fetch everything.

## Explanation

The behavior you're observing is related to **how Hibernate handles collections** (like `List<Address>`) and associated entities in relationships (like `@OneToMany` or `@OneToOne`) when using **eager** or **lazy** fetching. Let's break it down:

---

### **Key Points**
1. **`get()` Method Fetching Behavior**:
   - `get()` fetches the primary entity (`Student` in this case) **eagerly**, but it doesn't necessarily fetch related collections or associations unless they are explicitly configured to be eagerly loaded.
   - By default, collections like `List<Address>` in a `@OneToMany` relationship are **lazy-loaded**. This means Hibernate only fetches the collection when you explicitly access it.

2. **Eager vs Lazy Loading in Relationships**:
   - **Eager Loading**:
     - When configured, associated entities or collections are fetched immediately along with the primary entity.
     - Use `fetch = FetchType.EAGER` to enforce this behavior.
   - **Lazy Loading**:
     - Associated entities or collections are not fetched immediately. A proxy is returned, and the actual data is retrieved only when you access the collection or entity.

3. **Default Fetch Type**:
   - For **`@OneToMany`**: The default fetch type is `LAZY`.
   - For **`@OneToOne` and `@ManyToOne`**: The default fetch type is `EAGER`.

---

### **Why Your Collection (addressList) Isn't Fetched Immediately**
The `get()` method is eager-loading the `Student` entity itself but respects the default fetch type for the `@OneToMany` relationship, which is `LAZY`. This is why you see:
- The `name` and `id` of the `Student` fetched in the initial query.
- A separate query executed when you explicitly access the `addressList`.

---

### **Solution: Eagerly Loading the Collection**
If you want the `addressList` to be fetched along with the `Student` entity when using `get()`, you need to configure the relationship as eager:

```java
@OneToMany(fetch = FetchType.EAGER)
private List<Address> addressList;
```

### **Implications of Eager Fetching**
1. Hibernate will join the `Student` and `Address` tables in the initial query, which may impact performance if the collection is large.
2. Use eager loading cautiously for collections to avoid unnecessary data loading and performance bottlenecks.

---

### **Example Queries**
Assume:
- **Lazy Loading (Default)**:
  ```sql
  SELECT * FROM Student WHERE studentId = 1; -- Initial query
  SELECT * FROM Address WHERE studentId = 1; -- Triggered when addressList is accessed
  ```

- **Eager Loading**:
  ```sql
  SELECT s.*, a.* FROM Student s
  LEFT JOIN Address a ON a.studentId = s.studentId WHERE s.studentId = 1; -- Single query
  ```

---

### **Conclusion**
The **eager loading behavior of `get()` applies to the primary entity**, not necessarily to its collections or relationships, unless explicitly configured. For collections like `@OneToMany`, you need to use `fetch = FetchType.EAGER` if you want them loaded immediately. Otherwise, lazy loading ensures efficient fetching but requires explicit access to trigger queries.
