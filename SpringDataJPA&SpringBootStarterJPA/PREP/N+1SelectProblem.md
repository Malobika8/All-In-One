### **Case 1: N+1 Problem (many small queries)**

Example: Fetching all departments and then accessing employees lazily in a loop.

Generated SQL:

```sql
SELECT * FROM department; -- 1 query

-- Then one query for each department when you access employees
SELECT * FROM employee WHERE dept_id = 1;  -- Query #2
SELECT * FROM employee WHERE dept_id = 2;  -- Query #3
SELECT * FROM employee WHERE dept_id = 3;  -- Query #4
...
SELECT * FROM employee WHERE dept_id = N;  -- Query #(N+1)
```

If you have **100 departments**, that’s **1 + 100 = 101 queries**.

---

### **Case 2: Single JOIN query (optimized)**

If we use `JOIN FETCH`:

```sql
SELECT d.*, e.*
FROM department d
LEFT JOIN employee e ON d.id = e.dept_id;
```

**Only 1 query** returns everything you need.

---

### **Why N+1 is bad**

1. **Round trips to the database increase**

   * Each query is a separate network call from your app to the DB.
   * With high N, latency adds up — especially over remote DB connections.

2. **Overhead on the DB**

   * Many queries cause more parsing, execution planning, and locking overhead.

3. **Transaction time grows**

   * More queries = more DB time = slower request handling.

---

💡 **Key point:**
N+1 is primarily bad because **of the many separate DB round trips**, which are slower than sending one well-optimized query.

---

## Let’s walk through a **realistic Spring Data JPA example** where the N+1 problem happens, and then fix it.

## **Step 1 – Entity Setup**

```java
@Entity
public class Department {
    @Id
    @GeneratedValue
    private Long id;
    private String name;

    @OneToMany(mappedBy = "department", fetch = FetchType.LAZY)
    private List<Employee> employees = new ArrayList<>();
}

@Entity
public class Employee {
    @Id
    @GeneratedValue
    private Long id;
    private String name;

    @ManyToOne
    @JoinColumn(name = "dept_id")
    private Department department;
}
```

---

## **Step 2 – Repository**

```java
public interface DepartmentRepository extends JpaRepository<Department, Long> {
}
```

---

## **Step 3 – Service Method (Causes N+1)**

```java
@Service
public class DepartmentService {
    @Autowired
    private DepartmentRepository deptRepo;

    public void printDepartmentsAndEmployees() {
        List<Department> depts = deptRepo.findAll(); // Query #1

        for (Department dept : depts) {
            // Accessing employees triggers a SELECT for each department
            System.out.println(dept.getEmployees().size());
        }
    }
}
```

---

### **SQL Generated**

```
SELECT * FROM department;  
SELECT * FROM employee WHERE dept_id = 1;  
SELECT * FROM employee WHERE dept_id = 2;  
SELECT * FROM employee WHERE dept_id = 3;  
...
```

If there are 100 departments → **101 queries** (1 + N).

---

## **Step 4 – Fix with `JOIN FETCH`**

```java
public interface DepartmentRepository extends JpaRepository<Department, Long> {

    @Query("SELECT d FROM Department d JOIN FETCH d.employees")
    List<Department> findAllWithEmployees();
}
```

Service now:

```java
public void printDepartmentsAndEmployees() {
    List<Department> depts = deptRepo.findAllWithEmployees(); // Only 1 query
    for (Department dept : depts) {
        System.out.println(dept.getEmployees().size()); // Already loaded
    }
}
```

---

### **SQL Generated**

```
SELECT d.*, e.*
FROM department d
JOIN employee e ON d.id = e.dept_id;
```

✅ **Only 1 round trip** to DB.

---

💡 **Alternative fix:**
If you don’t want to hardcode `JOIN FETCH` in JPQL, you can use:

```java
@EntityGraph(attributePaths = "employees")
List<Department> findAll();
```

This tells JPA to eagerly fetch `employees` only for that query.

---

