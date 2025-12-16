## LazyInitializationException

* When a **LAZY association** is accessed **outside the persistence context** (e.g., after the `EntityManager` is closed or the transaction ends), JPA **cannot fetch the data** from the database.
* Example:

```java
Department dept = entityManager.find(Department.class, 1L);
entityManager.close(); // persistence context closed

int size = dept.getEmployees().size(); // LazyInitializationException
```

* Key point: **The proxy needs an active persistence context** to load the data.

* If the child collection is **empty**, no exception is thrown — the exception occurs only when JPA tries to fetch data and **cannot access the database**.

---

> *LAZY fetch requires an active persistence context. Accessing the association outside it triggers `LazyInitializationException`.*

---

## **Scenario Setup**

```java
@Entity
class Department {
    @Id @GeneratedValue
    Long id;
    String name;

    @OneToMany(mappedBy = "department", fetch = FetchType.LAZY)
    private List<Employee> employees = new ArrayList<>();
}

@Entity
class Employee {
    @Id @GeneratedValue
    Long id;
    String name;

    @ManyToOne(fetch = FetchType.EAGER)
    Department department;
}
```

### **Task 1**

You want to fetch a `Department` along with all its employees **in one query**, so that accessing `dept.getEmployees()` later **does not throw `LazyInitializationException`**.

**Question:**

* Write the **JPQL query** using `JOIN FETCH` to achieve this.

### Sol:

```jpql
SELECT d
FROM Department d
JOIN FETCH d.employees
```

This query:

* Loads `Department` **and** its `employees` in **one SQL**
* Initializes the LAZY collection
* Prevents `LazyInitializationException` when accessed later

Because this is a **`@OneToMany`**, the result may contain **duplicate departments** (one per employee row).

So the **safer version** is:

```jpql
SELECT DISTINCT d
FROM Department d
JOIN FETCH d.employees
```

### One-Liners

* *JOIN FETCH eagerly loads associations regardless of fetch type.*
* *DISTINCT is needed with JOIN FETCH on collections to avoid duplicate parent entities.*
* *JOIN FETCH is the primary solution to both N+1 and LazyInitializationException.*

---



