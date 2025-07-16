## Please read the documentation

https://docs.oracle.com/javaee/6/tutorial/doc/bnbpz.html

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/2c73ac66-86f0-4eec-bf63-4b886a5e4f0e" />

## ✅ JPA & Hibernate Revision Sheet

---

### 🔹 1. **JPA vs Hibernate**

* **JPA**: Specification (annotations + interfaces)
* **Hibernate**: Implementation (does actual DB work)
* You need an implementation (Hibernate, EclipseLink, etc.) to use JPA

---

### 🔹 2. **Entity Basics**

* Must be annotated with `@Entity`
* Must have `@Id`, no-arg constructor
* Mapped to a DB table

---

### 🔹 3. **Entity Lifecycle States**

| State     | Description                              |
| --------- | ---------------------------------------- |
| Transient | New object, not yet saved                |
| Managed   | Tracked by `EntityManager`               |
| Detached  | Was managed, now EM is closed or cleared |
| Removed   | Marked for deletion                      |

---

### 🔹 4. **EntityManager & Persistence Context**

* `EntityManager` handles all persistence operations (`persist`, `find`, `merge`, `remove`)
* First-level cache = **persistence context** (per EntityManager)
* Dirty checking = auto-detect changes to managed entities and auto-update on commit

---

### 🔹 5. **JPQL (Java Persistence Query Language)**

* Queries entities, not tables
* Use `SELECT e FROM Employee e WHERE e.salary > 50000`
* Supports joins, grouping, aggregation, subqueries

✅ Use `TypedQuery<T>`
✅ Use constructor expressions to return DTOs

---

### 🔹 6. **Relationships**

| Annotation   | Default Fetch | Notes                  |
| ------------ | ------------- | ---------------------- |
| `@ManyToOne` | EAGER         | Employee → Department  |
| `@OneToMany` | LAZY          | Department → Employees |

* Use `mappedBy` on inverse side
* Use `@JoinColumn` on owning side

---

### 🔹 7. **Cascading**

* `CascadeType.PERSIST` → Parent persist saves children
* `CascadeType.REMOVE` → Parent delete deletes children
* `orphanRemoval = true` → Removing child from collection deletes it from DB

---

### 🔹 8. **Lazy vs Eager Fetching**

* LAZY: Data is loaded when accessed (proxy)
* EAGER: Data is loaded immediately
* Lazy loading requires open `EntityManager`

---

### 🔹 9. **First-Level vs Second-Level Cache**

| Feature            | 1st Level     | 2nd Level             |
| ------------------ | ------------- | --------------------- |
| Scope              | EntityManager | EntityManagerFactory  |
| Enabled by default | ✅ Yes         | ❌ No — must configure |
| Shared?            | ❌ No          | ✅ Yes                 |

* 2nd-level cache uses providers like Ehcache, Infinispan

---


