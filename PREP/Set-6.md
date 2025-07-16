# If @ManyToOne(fetch = FetchType.LAZY) is used, what happens when you load an Employee entity using em.find() — will the department be loaded?

### Sol:

* By default, `@ManyToOne` is **EAGER** — but you overrode it to **LAZY**
* So `department` is **not** loaded when you call `em.find(Employee.class, ...)`
* It’s only fetched **when accessed** (e.g. `emp.getDepartment().getName()`)

If you do that access **after EM is closed**, you’ll get a `LazyInitializationException`

---

# What happens when this code runs?

Suppose you have:

```java
@ManyToOne(fetch = FetchType.LAZY)
private Department department;
```

And you run:

```java
EntityManager em = emf.createEntityManager();
Employee emp = em.find(Employee.class, 1);
em.close();

System.out.println(emp.getDepartment().getDepartmentName());
```

### Sol:

* Lazy loading happens **only while the EntityManager is open**
* After `em.close()`, the proxy can't fetch the `department` from DB
* Result: 💥 `LazyInitializationException`

#### onus:

To avoid this, you can:

* Access all needed fields **before** closing EM
* Or use **fetch join** in JPQL:

```java
SELECT e FROM Employee e JOIN FETCH e.department WHERE e.id = :id
```

This **eagerly loads** the department even if the mapping is `LAZY`.




