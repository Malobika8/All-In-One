### JPQL Basics (Java Persistence Query Language)

#### What is JPQL?

* JPQL is like SQL — but it queries **entities**, not tables
* It uses **entity names and field names**, not table/column names
* It is **type-safe**, portable across databases

#### Example Entity:

```java
@Entity
public class Employee {
    @Id
    private int id;
    private String name;
    private int salary;
}
```

#### Example JPQL:

```java
TypedQuery<Employee> query =
    em.createQuery("SELECT e FROM Employee e WHERE e.salary > 50000", Employee.class);
```

---

# Write a JPQL query to: Fetch all employee names (only name) where salary is greater than 60000.

### Sol:

```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("pu");
EntityManager em = emf.createEntityManager();

TypedQuery<String> tq = em.createQuery(
    "SELECT e.name FROM Employee e WHERE e.salary > 60000",
    String.class
);

List<String> list = tq.getResultList();
```

---

# Write a JPQL query to: Fetch all employees whose name starts with 'M'

### Sol:

```
EntityManagerFactory emf = Persistence.createEntityManagerFactory("pu");
EntityManager em = emf.createEntityManager();

TypedQuery<Employee> tq = em.createQuery(
    "SELECT e FROM Employee e WHERE e.name LIKE 'M%'",
    Employee.class
);

List<Employee> list = tq.getResultList();
```

---

# Write a JPQL query to fetch: Names of all employees who earn the maximum salary

### Sol:

```
TypedQuery<String> tq = em.createQuery(
    "SELECT e.name FROM Employee e WHERE e.salary = (SELECT MAX(e.salary) FROM Employee e)",
    String.class
);
List<String> list = tq.getResultList();
```

---

# Write a JPQL query to fetch department names and average salary of each department — only if average is more than 50000.

### Sol:

- **JPQL doesn’t return a DTO automatically** — you must use a **constructor expression**:
   `SELECT new DepartmentAvgSalaryDTO(...)`
- **`group by e.department` is valid**, but to avoid confusion, better to group by a scalar field like `e.department.departmentName`
- **DTO class must have a constructor matching selected fields**

### Step-by-Step

#### 1. Assume this DTO:

```java
public class DepartmentAvgSalaryDTO {
    private String departmentName;
    private Double averageSalary;

    public DepartmentAvgSalaryDTO(String departmentName, Double averageSalary) {
        this.departmentName = departmentName;
        this.averageSalary = averageSalary;
    }

    // Getters and setters
}
```

#### JPQL with Constructor Expression:

```java
TypedQuery<DepartmentAvgSalaryDTO> tq = em.createQuery(
    "SELECT new com.example.dto.DepartmentAvgSalaryDTO(e.department.departmentName, AVG(e.salary)) " +
    "FROM Employee e " +
    "GROUP BY e.department.departmentName " +
    "HAVING AVG(e.salary) > 50000",
    DepartmentAvgSalaryDTO.class
);
```






