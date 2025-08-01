## Orphan Removal in JPA

#### What is Orphan Removal?

> Orphan removal means:
> If a child entity is **removed from the parent's collection**, it is also **deleted from the database** automatically.

#### When to use it:

In `@OneToMany` (or `@OneToOne`) relationships where:

* You manage child objects through the parent
* And you want **automatic deletion** when the child is no longer referenced

#### Syntax:

```java
@OneToMany(mappedBy = "department", cascade = CascadeType.ALL, orphanRemoval = true)
private List<Employee> employees;
```

#### Example:

```java
Department d = em.find(Department.class, 1);
d.getEmployees().remove(0); // remove one employee from the list

em.getTransaction().commit();
```

➡️ The removed employee is automatically deleted from the DB

#### ⚠️ Important:

* Orphan removal works **only if the entity was previously managed**
* It is **not the same** as `CascadeType.REMOVE`

---

# Question:

You have:

```java
@OneToMany(mappedBy = "department", cascade = CascadeType.ALL, orphanRemoval = true)
private List<Employee> employees;
```

If you remove an `Employee` from the list, but **do not call `em.remove(employee)`**, will it still be deleted from the DB?

### Sol:

Yes since orphanRemoval is set to true

---

# What if you remove the employee from the list but don’t set the department field of the employee to null — will it still be deleted?

```java
Department d = em.find(Department.class, 1);
Employee empToRemove = d.getEmployees().get(0);

d.getEmployees().remove(empToRemove);

em.getTransaction().commit();
```

### Sol:

> "Yes, the employee will be deleted **because it’s removed from the parent’s collection**, and `orphanRemoval = true`.
> Even if we don’t nullify the child’s `department` field manually, JPA handles it internally."

💡 In bi-directional mappings, JPA manages the inverse side (`mappedBy`) for orphan removal.

---

# Task:

Write code (not JPQL) to:

* Load a `Department` and its employees
* Remove one employee from the list
* Commit the transaction so that employee gets deleted via `orphanRemoval`

### Sol:

```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("pu");
EntityManager em = emf.createEntityManager();

em.getTransaction().begin();

Department department = em.find(Department.class, 1);
Employee employee = department.getEmployees().get(0);

department.getEmployees().remove(employee); // not removeEmployee

em.getTransaction().commit();
em.close();
```

---

# ✅ Difference Between `orphanRemoval = true` vs `CascadeType.REMOVE`

| Feature                 | `CascadeType.REMOVE`                    | `orphanRemoval = true`                                   |
| ----------------------- | --------------------------------------- | -------------------------------------------------------- |
| **When it applies**     | When **you remove the parent entity**   | When **you remove a child from the parent’s collection** |
| **Effect**              | Also removes the child entities         | Also removes the child entity from DB                    |
| **Use case**            | Delete entire object graph              | Delete a child that is no longer referenced              |
| **Typical use with**    | `em.remove(parent)`                     | `parent.getChildren().remove(child)`                     |
| **Manual call needed?** | Yes — you must call `em.remove(parent)` | No — just removing from collection is enough             |

---

### 🔍 Example:

#### 👉 `CascadeType.REMOVE`:

```java
@OneToMany(mappedBy = "department", cascade = CascadeType.REMOVE)
private List<Employee> employees;

...

em.remove(department);
```

✅ All employees will also be removed when the department is removed

---

#### 👉 `orphanRemoval = true`:

```java
@OneToMany(mappedBy = "department", orphanRemoval = true)
private List<Employee> employees;

...

department.getEmployees().remove(emp);
```

✅ Just removing `emp` from the list causes JPA to delete `emp` from the DB — no need to call `em.remove(emp)`

---

### 🔥 You can combine both:

```java
@OneToMany(mappedBy = "department", cascade = CascadeType.ALL, orphanRemoval = true)
```

* Deletes children when:

  * You delete the parent
  * Or you remove children from parent’s collection

---

### ✅ Summary:

> `CascadeType.REMOVE` is used to delete child entities **when the parent is deleted**.
> `orphanRemoval = true` is used to delete child entities **when they’re removed from the parent’s collection**.
> You can use both together if you want full cascading + orphan handling.

---



