Here's a **clear and simple example** of how `merge()` works in Hibernate, including how it differs from `update()`.

---

## 🏗️ Setup:

Assume we have this entity:

```java
@Entity
@Table(name = "table1")
public class Table1 {
    @Id
    private int tId;
    private String tName;
    private String tCity;

    public Table1() {} // Required default constructor

    public Table1(int tId, String tName, String tCity) {
        this.tId = tId;
        this.tName = tName;
        this.tCity = tCity;
    }

    // Getters and setters
}
```

---

## ✅ Example: Using `merge()` safely

```java
Session session1 = sessionFactory.openSession();
Transaction tx1 = session1.beginTransaction();

// 1. Load the entity
Table1 t1 = session1.get(Table1.class, 1); // Managed
tx1.commit();
session1.close(); // Now it's detached

// 2. Modify the detached entity
t1.settCity("NewCity");

// 3. Open new session
Session session2 = sessionFactory.openSession();
Transaction tx2 = session2.beginTransaction();

// 4. Merge the changes (safe even if another instance is already managed)
Table1 merged = (Table1) session2.merge(t1); // returns managed instance
System.out.println(merged == t1); // false - this is a different (managed) instance

tx2.commit();
session2.close();
```

---

## ⚠️ Why `update()` would fail here:

If you did:

```java
session2.update(t1);
```

It would throw a `NonUniqueObjectException` **if** `session2` had already loaded another instance with the same ID (`tId = 1`).

---

## 🔁 Recap:

* `merge()` copies changes from the detached entity into the **managed instance inside session**.
* It returns that managed instance.
* You should prefer using `merge()` when:

  * You’re working with **detached objects**.
  * You’re not sure whether the session already contains that entity.
  * You want to avoid exceptions due to duplicate managed objects.

---
