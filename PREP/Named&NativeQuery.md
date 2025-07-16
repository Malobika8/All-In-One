# Named Queries & Native Queries in JPA

## ✅ 1. `@NamedQuery` (JPQL — predefined queries)

#### What is it?

* A way to define JPQL queries **at the entity class level**, not inline
* Useful when you want to reuse queries across the app
* Declared with `@NamedQuery` or `@NamedQueries`

#### Syntax:

```java
@Entity
@NamedQuery(
    name = "Employee.findByDept",
    query = "SELECT e FROM Employee e WHERE e.department = :dept"
)
public class Employee { }
```

#### Usage in code:

```java
TypedQuery<Employee> query = em.createNamedQuery("Employee.findByDept", Employee.class);
query.setParameter("dept", "HR");

List<Employee> list = query.getResultList();
```

#### When to use it?

* For **common queries** that don’t change often
* Keeps code cleaner

## ✅ 2. `@NamedNativeQuery` (SQL — native queries)

#### What is it?

* Used to write **real SQL queries**, not JPQL
* Can return entities or use `resultSetMapping`

#### Syntax:

```java
@Entity
@NamedNativeQuery(
    name = "Employee.findTopPaid",
    query = "SELECT * FROM employee WHERE salary > 90000",
    resultClass = Employee.class
)
public class Employee { }
```

#### Usage:

```java
Query query = em.createNamedQuery("Employee.findTopPaid");
List<Employee> result = query.getResultList();
```

---

# You want to fetch all employees whose salary > 80,000 using a **named JPQL query**. Write the annotation and how to call it from code.

### Sol:

```java
@Entity
@NamedQuery(
    name = "Employee.findBySalary",
    query = "SELECT e FROM Employee e WHERE e.salary > 80000"
)
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class Employee {
    @Id
    private int id;
    private String name;
    private int salary;
}
```
```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("pu");
EntityManager em = emf.createEntityManager();

TypedQuery<Employee> tq = em.createNamedQuery("Employee.findBySalary", Employee.class);
List<Employee> list = tq.getResultList();
```

---

# You have the following native query:

```sql
SELECT id, name FROM employee WHERE salary > 90000
```

You want to write a `@NamedNativeQuery` for it that maps to a DTO called `EmployeeNameDTO` with `int id`, `String name`.

How would you do it?

### Sol:

```
EntityManagerFactory emf = Persistence.createEntityManagerFactory("pu");
EntityManager em = emf.createEntityManager();
TypedQuery<Employee> tq = em.createNamedQuery("Employee.findBySalary", Employee.class);
List<Employee> list = tq.getResultList();

@Entity
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@NamedNativeQuery(
    name = "Employee.findBySalary",
    query = "SELECT id, name FROM employee WHERE salary > 90000"
    )
public class Employee{
    @Id
    int id;
    String name;
    int salary;
}
```

