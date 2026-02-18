# The Original Problem

We had:

* 3 Departments
* 3000+ Employees
* Bidirectional mapping:

```java
Employee  →  Department  (ManyToOne)
Department →  List<Employee> (OneToMany)
```

We implemented pagination:

```java
Page<Employee> findAll(Pageable pageable);
```

And exposed:

```
GET /employees?page=0&size=50
```

---

## ❗ Unexpected Behavior

We observed:

1. Infinite JSON recursion
2. Extra SQL queries firing
3. N+1 behavior during serialization

---

# 2️⃣ Why Infinite Recursion Happened

Because of **bidirectional mapping**.

Object graph in memory:

```
Employee
  └── Department
        └── List<Employee>
              └── Department
                    └── List<Employee>
                          ...
```

When returning `List<Employee>`, Jackson tries to serialize everything:

```
Employee → Department → Employees → Department → Employees ...
```

This results in:

* Deeply nested JSON
* Huge response
* Possible StackOverflowError

---

# 3️⃣ Why Lazy Loading Triggered Queries

Even though we set:

```java
@ManyToOne(fetch = FetchType.LAZY)
```

Lazy does NOT mean “never load”.

It means:

> Load when accessed.

Jackson accesses:

```java
employee.getDepartment()
department.getName()
department.getEmployeeList()
```

This initializes Hibernate proxies.

So Hibernate executes:

```sql
select department where id=?
select employee where department_id=?
```

This caused N+1 behavior.

---

# 4️⃣ Important Concept: Hibernate Proxy

When loading Employee:

```sql
select e.id, e.department_id, e.name, e.salary
```

Hibernate stores:

```
employee.department = Proxy
```

No DB hit yet.

But when any non-ID field is accessed:

```java
department.getName()
```

Hibernate initializes proxy → fires SQL.

Serialization counts as field access.

---

# 5️⃣ Why N+1 Happened

For each employee in the page:

Jackson accessed department fields.

If page size = 50:

* 1 query for employees
* 50 queries for departments (worst case)

Classic N+1.

---

# 6️⃣ Temporary Fixes

### Option 1 — `@JsonIgnore`

```java
@JsonIgnore
private List<Employee> employeeList;
```

Prevents recursion.

Or:

```java
@JsonIgnore
private Department department;
```

Prevents lazy loading entirely.

Result:

* Only employee query runs
* No N+1
* But department info missing

---

# 7️⃣ Why Exposing Entities is Dangerous

Problems:

* Lazy loading triggers unexpectedly
* Infinite recursion
* Security risk
* Over-fetching
* Tight coupling between DB model & API

Best practice:

> Never expose entities directly in REST APIs.

---

# 8️⃣ Correct Production Solution — DTO

Instead of returning:

```java
List<Employee>
```

Return:

```java
List<EmployeeResponseDTO>
```

Example DTO:

```java
public class EmployeeResponseDTO {
    private Long id;
    private String name;
    private Long salary;
    private String departmentName;
}
```

Now:

* No recursion
* No lazy surprises
* Controlled JSON structure
* Clean API contract

---

# 9️⃣ Pagination — What It Actually Does

When you call:

```
GET /employees?page=0&size=50
```

Hibernate generates:

```sql
select e ... offset 0 rows fetch first 50 rows only
select count(e.id)
```

Pagination = LIMIT + OFFSET.

Important:

* Always fires a count query.
* Returns metadata:

  * totalElements
  * totalPages
  * currentPage
  * isLast

Client decides when to request next page.

Server does not loop automatically.

---

# 🔟 Pagination Pros & Cons

### ✅ Pros

* Controlled memory usage
* Fast responses
* Suitable for UI
* Easy to implement

### ❌ Cons

* Requires count query
* Offset becomes slow for very large datasets
* Not ideal for processing millions of rows

---

# 1️⃣1️⃣ Streaming — What Is It?

Streaming allows processing large datasets without loading everything into memory.

Instead of:

```java
Page<Employee>
```

We use:

```java
Stream<Employee>
```

Example:

```java
@Query("SELECT e FROM Employee e")
Stream<Employee> streamAll();
```

Service:

```java
@Transactional(readOnly = true)
public void processAll() {
    try (Stream<Employee> stream = repo.streamAll()) {
        stream.forEach(emp -> {
            // process one by one
        });
    }
}
```

---

# 1️⃣2️⃣ Streaming vs Pagination

| Feature         | Pagination       | Streaming        |
| --------------- | ---------------- | ---------------- |
| Use case        | REST APIs        | Batch processing |
| Memory usage    | Small (per page) | Very small       |
| Count query     | Yes              | No               |
| UI friendly     | Yes              | No               |
| Good for export | Not ideal        | Excellent        |
| Network calls   | Multiple         | Single           |

---

# 1️⃣3️⃣ When To Use What

### Use Pagination When:

* Building REST APIs
* Data shown in UI
* Client requests data in chunks

### Use Streaming When:

* Exporting CSV/Excel
* Processing millions of records
* Running background jobs
* Data migration

---

# 1️⃣4️⃣ Key Architectural Lessons

1. Lazy loading triggers on getter access.
2. Serialization can cause N+1.
3. Bidirectional mapping ≠ safe JSON.
4. DTOs are mandatory in production systems.
5. Pagination is client-driven.
6. Streaming is server-side batch processing.

---

