# You want a repository that supports:

* Basic CRUD
* Sorting results by salary descending
* Pagination

👉 Which Spring Data JPA interface should you extend?

### Sol:

Would extend JpaRepository because it inherits from both CrudRepository and PagingAndSortingRepository, and it also adds useful JPA-specific methods like findAllById, flush, and saveAll.
It’s the most complete and commonly used interface in Spring Data JPA.

---

## Derived Query Methods in Spring Data JPA

*(a.k.a. method-name-based queries)*

#### What are these?

Spring Data JPA lets you define queries **just by naming methods properly** in your repository interface.
No SQL, no JPQL — Spring parses the method name and builds the query!

#### Example:

```java
public interface EmployeeRepository extends JpaRepository<Employee, Integer> {
    List<Employee> findBySalaryGreaterThan(int salary);
}
```

✅ Spring auto-generates this:

```sql
SELECT * FROM employee WHERE salary > ?
```

#### 🔤 Common Keywords You Can Use

| Keyword                                            | Meaning                 |
| -------------------------------------------------- | ----------------------- |
| `findBy...`                                        | Start of a query method |
| `And`, `Or`                                        | Combine conditions      |
| `GreaterThan`, `LessThan`, `Between`               | Range conditions        |
| `Like`, `StartingWith`, `EndingWith`, `Containing` | Pattern matching        |
| `In`, `NotIn`                                      | For collections         |
| `IsNull`, `IsNotNull`                              | Null checks             |
| `OrderBy`                                          | Sorting                 |
| `Top`, `First`                                     | Limit result            |

#### Sample Queries:

```java
List<Employee> findByDepartment_DepartmentName(String name);
List<Employee> findByNameStartingWith(String prefix);
List<Employee> findBySalaryBetween(int min, int max);
List<Employee> findByNameIn(List<String> names);
List<Employee> findTop3ByOrderBySalaryDesc();
```

---

# Write a method in your `EmployeeRepository` that:

* Returns all employees in the **"IT"** department
* Whose salary is **greater than 70000**

### Sol:

```
List<Employee> findByDepartment_DepartmentNameAndSalaryGreaterThan(String departmentName, int salary);
```

---

# Write a repository method to:

✅ Find all employees whose name starts with "M"
✅ And salary is less than 80000

### Sol:

```
List<Employee> findByNameStartingWithAndSalaryLessThan(String str, int salary);
```

---

# Write a repository method to:

✅ Find top 5 highest-paid employees
✅ From the "HR" department
✅ Ordered by salary in descending order

### Sol:

In Spring Data JPA, Top5 should appear at the start, like findTop5By...

```
List<Employee> findTop5ByDepartment_DepartmentNameOrderBySalaryDesc(String departmentName);
```

---

# Write a repository method to:

> ✅ Find all employees whose name **contains `"a"`** (case-insensitive)
> ✅ And whose salary is **between 50000 and 100000**
> ✅ Order the results by name ascending

### Sol:

- Parameter order must match the method signature
- Contains is case-sensitive → we’ll use ContainingIgnoreCase for case-insensitive search

```
List<Employee> findByNameContainingIgnoreCaseAndSalaryBetweenOrderByNameAsc(String str, int min, int max);
```

---

# Write a repository method to:

✅ Find all employees who belong to any one of several departments (passed as a list of names)
✅ And whose salary is not null

### Sol:

```
List<Employee> findByDepartment_DepartmentNameInAndSalaryIsNotNull(List<String> departmentNames);
```

---

# In Spring Data JPA, what is the difference between findById() and getOne() (or getReferenceById() in newer versions)?

### Sol:

1. **`findById(id)`**

   * **Eagerly fetches** the entity from the database immediately.
   * Returns `Optional<T>` (in Spring Data JPA), so **never returns `null`** — you check with `.isPresent()` or `.orElse(...)`.
   * If the entity is not found, it returns an **empty `Optional`**.

2. **`getOne(id)`** *(deprecated since Spring Data JPA 2.5, replaced by `getReferenceById(id)`)*

   * **Does not hit the DB immediately** — returns a **lazy proxy**.
   * Actual SQL query happens **only when you access a field**.
   * If the entity doesn’t exist and you try to access it, JPA throws **`EntityNotFoundException`**.
   * Requires an **active transaction** when you access the fields (lazy loading).

#### **Note:**

   * `getOne()` / `getReferenceById()` **does not return the first row in the table**. It always returns a proxy for the **given ID**, not arbitrary data.

---

💡 **When to use:**

* **`findById()`** → When you actually need the entity data immediately, and want to handle absence safely.
* **`getReferenceById()`** → When you just need a reference (e.g., to set a foreign key in another entity) without triggering a full fetch.

---

# In Spring Data JPA, what is the difference between save() and saveAndFlush()? When would you use saveAndFlush() instead of save()?

### Sol:

#### **`save(entity)`**

* Persists a **new** entity or merges an **existing** one into the **persistence context**.
* Changes are **not immediately written to the database**.
* The actual SQL is executed when:

  * The **transaction commits**, or
  * The persistence context is **flushed** automatically (e.g., before a JPQL query).

#### **`saveAndFlush(entity)`**

* Calls `save(entity)` **and** immediately calls `EntityManager.flush()`.
* This forces Hibernate to:

  * Synchronize the persistence context with the database **right now**.
  * Execute any pending SQL statements immediately.
* **Use cases:**

  * When you need the database to reflect changes **before the transaction commits** (e.g., when subsequent code relies on updated DB state).
  * Example: saving an entity and then running a native query that depends on it.

💡 **Note:**
You can also manually flush anytime via:

```java
@PersistenceContext
private EntityManager em;

em.flush();
```

…but `saveAndFlush()` is the Spring Data JPA convenience method.

---

# What is the N+1 select problem in JPA, and how can you solve it in Spring Data JPA?

### Sol:

---

# Suppose you have an entity `Book` with fields `id`, `title`, `price`. You want to update the `price` of a book with id = 1 to `500` **without fetching the whole entity first**. How would you write this in **Spring Data JPA** (method or annotation-based approach)?

### Sol:

- **Update queries in JPA**
   * You must add `@Modifying` above `@Query` to tell Spring this is an update/delete query.
   * The return type should usually be `int` (rows updated), not `void`.

**JPQL:**

```java
@Repository
public interface BookRepository extends JpaRepository<Book, Integer> {

    @Modifying
    @Query("update Book b set b.price = :price where b.id = :id")
    int updateBookPrice(@Param("id") int id, @Param("price") double price);
}
```

**Native SQL:**

```java
@Repository
public interface BookRepository extends JpaRepository<Book, Integer> {

    @Modifying
    @Query(value = "update book set price = :price where id = :id", nativeQuery = true)
    int updateBookPrice(@Param("id") int id, @Param("price") double price);
}
```

⚠️ **Important:**

* You also need to run this method inside a `@Transactional` context (either on service method or repository method). Otherwise, the update won’t execute.

---




