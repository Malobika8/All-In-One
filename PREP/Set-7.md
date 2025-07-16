### Cascade Types in JPA

#### What is Cascading?

Cascading lets **one entity operation affect related entities** automatically.

> For example:
> If you `persist()` a `Department`, it can automatically `persist()` all its employees — if you enable cascade.

#### When does it apply?

On relationships:

* `@OneToMany`
* `@ManyToOne`
* `@OneToOne`
* `@ManyToMany`

#### Common Cascade Types:

| Type      | What It Means                                  |
| --------- | ---------------------------------------------- |
| `PERSIST` | Saving the parent also saves the child         |
| `MERGE`   | Merging parent also merges the child           |
| `REMOVE`  | Removing parent also removes the child         |
| `REFRESH` | Refreshing parent also refreshes child from DB |
| `DETACH`  | Detaching parent also detaches child           |
| `ALL`     | Applies all the above (except orphan removal)  |

#### Example:

```java
@OneToMany(mappedBy = "department", cascade = CascadeType.PERSIST)
private List<Employee> employees;
```

Now if you:

```java
em.persist(department);
```

✅ JPA will also **persist all employees** in the list.

---

# Question:

You have a `Department` entity with a `List<Employee>` and:

```java
@OneToMany(mappedBy = "department", cascade = CascadeType.PERSIST)
private List<Employee> employees;
```

If you **persist the Department** without explicitly persisting each Employee — what will happen?

### Sol:

* Because of `cascade = CascadeType.PERSIST`, when you do:

  ```java
  em.persist(department);
  ```

  — JPA will **automatically persist** all the `Employee` objects in `department.getEmployees()`.

#### Insight:

* Without `cascade = PERSIST`, you would need to explicitly call `em.persist(emp1)`, `em.persist(emp2)`, etc.
* With cascade, it’s **automatic** — cleaner and less error-prone

#### Example:

```java
Department d = new Department(1, "HR");
Employee e1 = new Employee(101, "Malo", 60000, d);
Employee e2 = new Employee(102, "Bika", 55000, d);

d.setEmployees(List.of(e1, e2));

em.persist(d); // ✅ will also persist e1 and e2 because of cascade
```

---
