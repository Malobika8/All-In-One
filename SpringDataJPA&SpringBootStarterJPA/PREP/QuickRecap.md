## ✅ Spring Data JPA

---

### 🔹 What Is Spring Data JPA?

> Spring Data JPA is a part of the Spring ecosystem that:

* Simplifies JPA-based database access
* Eliminates boilerplate code like `EntityManager`, `createQuery()`, etc.
* Uses **interface-based repositories** with built-in CRUD methods

---

### 🔧 Prerequisites:

* You're already familiar with **JPA/Hibernate** (✅ you are!)
* You have Spring Boot in your project (we’ll assume this for simplicity)

---

## ✅ Step 1: Setup

**In `pom.xml`:**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>
```

You can replace `H2` with MySQL, PostgreSQL, etc.

---

## ✅ Step 2: Entity Example

```java
@Entity
public class Employee {
    @Id
    private int id;
    private String name;
    private int salary;

    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;

    // Getters, setters, constructors
}
```

---

## ✅ Step 3: Repository Interface

```java
public interface EmployeeRepository extends JpaRepository<Employee, Integer> {
    List<Employee> findByDepartment_DepartmentName(String deptName);
    List<Employee> findBySalaryGreaterThan(int salary);
}
```

📌 No need to implement this — Spring creates the implementation automatically.

---

## ✅ Step 4: Use It in a Service or Controller

```java
@Service
public class EmployeeService {
    @Autowired
    private EmployeeRepository repo;

    public List<Employee> getHighEarners() {
        return repo.findBySalaryGreaterThan(50000);
    }
}
```

---

## 🔍 Behind the scenes:

* `JpaRepository` gives methods like `findAll()`, `save()`, `deleteById()`, etc.
* Spring Data JPA uses **method name conventions** to generate SQL/JPQL

---

## ✅ Step 5: Spring Data JPA Repository Hierarchy

---

Spring Data JPA gives you interfaces with **increasing capabilities**:

```
Repository (marker)
   └── CrudRepository
         └── PagingAndSortingRepository
               └── JpaRepository
```

---

### ✅ 1. `Repository<T, ID>`

> The **base interface** — no methods. Just a **marker** so Spring knows this is a repository.

```java
public interface MyRepo extends Repository<Employee, Integer> {
    // nothing here
}
```

---

### ✅ 2. `CrudRepository<T, ID>`

> Adds basic **CRUD** operations:

```java
Optional<T> findById(ID id);
List<T> findAll();
T save(T entity);
void deleteById(ID id);
```

You can use it if you want only **basic CRUD**.

---

### ✅ 3. `PagingAndSortingRepository<T, ID>`

> Adds pagination and sorting support:

```java
Iterable<T> findAll(Sort sort);
Page<T> findAll(Pageable pageable);
```

---

### ✅ 4. `JpaRepository<T, ID>`

> Most powerful — includes everything from above + more:

```java
List<T> findAll();
List<T> findAllById(Iterable<ID> ids);
void deleteInBatch(Iterable<T> entities);
<T> List<T> findAll(Specification<T> spec);
```

**💡 Best practice: Just extend `JpaRepository` — it includes all others.**

---

### ✅ Summary Table:

| Interface                    | Use When You Need...                                    |
| ---------------------------- | ------------------------------------------------------- |
| `Repository`                 | Just a marker interface (rarely used)                   |
| `CrudRepository`             | Basic CRUD only                                         |
| `PagingAndSortingRepository` | Pagination and sorting                                  |
| `JpaRepository`              | Everything (CRUD + pagination + JPA-specific helpers) ✅ |

---

