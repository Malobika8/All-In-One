# Write a JPQL query to fetch all employees with salary greater than 50,000.

* Write this as a JPQL string.
* Then show how you’d execute it using `EntityManager`.

Assume the following JPA entity:

```java
@Entity
public class Employee {
    @Id
    private int id;

    private String name;
    private int salary;
    private String department;
}
```

### Sol:

```java
import jakarta.persistence.*;

import java.util.List;

public class Main {
    public static void main(String[] args) {

        EntityManagerFactory emf = Persistence.createEntityManagerFactory("my-pu");
        EntityManager em = emf.createEntityManager();

        String jpql = "SELECT e FROM Employee e WHERE e.salary > 50000";
        TypedQuery<Employee> query = em.createQuery(jpql, Employee.class);

        List<Employee> employees = query.getResultList();

        for (Employee e : employees) {
            System.out.println(e.getName() + " - " + e.getSalary());
        }

        em.close();
        emf.close();
    }
}
```

#### JPQL Summary:

| SQL                      | JPQL                         |
| ------------------------ | ---------------------------- |
| `SELECT * FROM employee` | `SELECT e FROM Employee e`   |
| `WHERE salary > 50000`   | `WHERE e.salary > 50000`     |
| Use table + column names | Use **Entity + field names** |

---

# Write a JPQL query to fetch employees from the “HR” department with salary > 30000, and order them by salary descending.

### Sol:

```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("pu");
EntityManager em = emf.createEntityManager();

TypedQuery<Employee> query = em.createQuery(
    "SELECT e FROM Employee e WHERE e.department = 'HR' AND e.salary > 30000 ORDER BY e.salary DESC",
    Employee.class
);

List<Employee> employees = query.getResultList();

for (Employee e : employees) {
    System.out.println(e.getName() + " - " + e.getSalary());
}

em.close();
emf.close();
```

---

# Write a JPQL query to fetch employees whose names start with “A”, and return only the **first 5 results.

**Requirements**:

* Use `LIKE 'A%'`
* Set `maxResults` to 5

### Sol:



