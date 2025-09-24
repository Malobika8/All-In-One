# What is the difference between JPA and Hibernate? Can you use JPA without Hibernate?

### Sol:

JPA is a **specification** that defines how object-relational mapping (ORM) should be done in Java. It provides a standard set of annotations and APIs to interact with relational databases.
Hibernate is the most widely used **implementation** of the JPA specification — it actually performs the ORM and SQL execution behind the scenes.
While Hibernate is the most common JPA provider, others like **EclipseLink**, **OpenJPA**, and **DataNucleus** can also be used. You **can’t use JPA alone** — it needs a provider like Hibernate to function.

---

# What are the rules to make a class a valid JPA entity?

### Sol:

To make a class a valid JPA entity:

1. It must be annotated with `@Entity`
2. It must have a no-arg constructor (can be `public` or `protected`)
3. It must have a field annotated with `@Id` (the primary key)
4. It should not be `final`
5. Its fields should be either public or accessible via getters/setters
6. It should be a top-level class (not static or inner class)

---

# What is `EntityManager`? What is the role of the **persistence context**?

### Sol:

* `EntityManager` is the main interface provided by JPA to perform CRUD operations.
* It manages a **persistence context**, which is a **first-level cache** where all managed entity instances are stored.
* Any entity retrieved or persisted by the `EntityManager` becomes **managed** — changes to it are automatically tracked.
* This is how JPA knows what to flush to the database during commit — via **dirty checking** on the persistence context.

#### Common operations:

```
EntityManager em = emf.createEntityManager();

em.getTransaction().begin();

em.persist(employee);     // INSERT
em.find(Employee.class, 1);  // SELECT
em.merge(employee);       // UPDATE
em.remove(employee);      // DELETE

em.getTransaction().commit();
```

---

# Code Challenge

Suppose you have this `Employee` entity:

```java
@Entity
public class Employee {
    @Id
    private int id;
    private String name;
    private int salary;

    // Constructors, getters, setters
}
```

Write JPA code (not Spring) to:

* Create an employee with id `1`, name `"Malobika"`, and salary `60000`
* Persist it using `EntityManager`

### Sol:

```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("pu"); // "pu" = persistence-unit name
EntityManager em = emf.createEntityManager();

em.getTransaction().begin();

Employee employee = new Employee(1, "Malobika", 60000);
em.persist(employee);  // Use persist for new entity

em.getTransaction().commit();

em.close();
emf.close();
```

✅ `persist()` marks the entity as "managed" and inserts it into the DB.

---

# What is the difference between `persist()` and `merge()` in JPA?

### Sol:

* `persist()` is used to **make a new transient entity persistent**:

  * It **adds** the entity to the persistence context
  * The entity becomes **managed**
  * Changes are automatically tracked

* `merge()` is used to:

  * **Copy** the state of a **detached** (or even new) entity into a **managed instance**
  * It **returns** the managed copy
  * The passed object itself remains detached

#### Subtle Difference:

```java
Employee detachedEmp = new Employee(1, "Malobika", 60000);

Employee managedCopy = em.merge(detachedEmp);
```

* `detachedEmp` is NOT tracked
* `managedCopy` IS tracked — you must use this after the merge

> If you use `merge()` for a new entity (not yet in DB), JPA will still insert it!
> But it’s **less efficient** and **doesn’t make the original object managed**.

So always prefer:

* `persist()` for new
* `merge()` for updates/detached

---

# What are the four JPA entity states?

### Sol:

#### **Transient** – Not known to JPA yet

* You just created the object with `new`
* It has no connection to the database
* Example:

  ```java
  Employee e = new Employee(1, "Malobika", 60000);
  ```

#### **Managed** – Inside JPA's control

* You called `em.persist(e)`
* JPA is now watching it — if you change anything, JPA will auto-update the DB
* Example:

  ```java
  em.persist(e);  // now "e" is managed
  ```

#### **Detached** – Was managed, but now out of JPA’s hands

* You closed `EntityManager`, or the transaction ended
* The object still has data but JPA won’t track changes
* You need `merge()` to bring it back

#### **Removed** – Marked for deletion

* You called `em.remove(e)`
* It's managed, but JPA will delete it from DB when you commit

#### Summary Table

| State     | Means                   | Example                          |
| --------- | ----------------------- | -------------------------------- |
| Transient | Not in DB, not in JPA   | `new Employee(...)`              |
| Managed   | Being tracked by JPA    | `em.persist(e)`                  |
| Detached  | Was tracked, now not    | `em.close();` or transaction end |
| Removed   | Will be deleted from DB | `em.remove(e)`                   |

---

# If I call `new Employee(1, "Malo", 60000)` and then do nothing — what state is this entity in?

### Sol: 

`new Employee(...)` — and doing nothing else — means:

* It's **not in the database**
* It's **not being tracked by JPA**
* So, it's in the **transient** state.

---

# Question

```java
Employee e = new Employee(1, "Malo", 60000);
EntityManager em = emf.createEntityManager();
em.getTransaction().begin();
em.persist(e);
em.getTransaction().commit();
em.close();
```

After `em.close()`, what state is `e` in?

### Sol:

After you call `em.persist(e)`, the entity is:

* ✅ **Managed** (while EntityManager is open)

But once you:

```java
em.getTransaction().commit();
em.close();
```

👉 The EntityManager is closed
👉 So the entity `e` is no longer managed

🟰 Now it’s in the **detached** state

---

# Questions

1. Can you call `persist()` on a detached entity?
2. Can you call `merge()` on a transient entity?
3. Does `persist()` return anything?
4. Does `merge()` return a managed object?

### SOL:

#### 1. **Can you call `persist()` on a detached entity?**

> **Yes, technically — but it throws `EntityExistsException` if an entity with the same ID already exists**

Explanation:

* `persist()` is meant for **new (transient)** entities
* If you pass a **detached entity** (i.e. already in DB), JPA will try to insert and may fail
* So we **don’t** use `persist()` on detached — we use `merge()`

#### 2. **Can you call `merge()` on a transient entity?**

> **Yes**

✅ Hibernate will treat the new (transient) object as data to be inserted — it will copy the state into a **new managed object** and persist it.

#### 3. **Does `persist()` return anything?**

> **No**

* `persist()` has return type `void`
* It doesn’t return anything
* It just marks the entity as managed — changes are tracked automatically

#### 4. **Does `merge()` return a managed object?**

> **Yes**

```java
Employee detached = new Employee(...);
Employee managed = em.merge(detached);
```

* `merge()` returns the new **managed instance**
* The original `detached` object remains detached

So yes, `merge()` returns a **managed** object

#### 💡 Summary Table:

| Method  | Use Case            | Returns?             | Adds to Persistence Context? |
| ------- | ------------------- | -------------------- | ---------------------------- |
| persist | For new entity      | ❌ No                 | ✅ Yes (makes it managed)     |
| merge   | For detached OR new | ✅ Yes (managed copy) | ✅ Yes                        |


