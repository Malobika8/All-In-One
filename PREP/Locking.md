# 🔐 Optimistic Locking (JPA / Hibernate)

### 🧠 Problem it solves

👉 **Lost updates in concurrent transactions**

Example:

* User A and User B load the **same Employee row**
* Both modify salary
* Whoever commits last **overwrites the other**

## ✅ Optimistic Locking — Core Idea

> “Assume conflicts are rare.
> Check before update if data was modified by someone else.”

## 🛠 How it is implemented (MOST IMPORTANT)

### ✔ Using `@Version`

```java
@Entity
class Employee {

    @Id
    Long id;

    String name;

    double salary;

    @Version
    int version;
}
```

## 🔄 What happens internally

1️⃣ Transaction A reads employee (version = 1)
2️⃣ Transaction B reads employee (version = 1)

3️⃣ Transaction A updates:

```sql
UPDATE employee 
SET salary = 60000, version = 2 
WHERE id = 1 AND version = 1;
```

✔ succeeds

4️⃣ Transaction B updates:

```sql
UPDATE employee 
SET salary = 65000, version = 2 
WHERE id = 1 AND version = 1;
```

❌ affects **0 rows**

➡️ Hibernate throws:

```text
OptimisticLockException
```

## 🟢 Why this is GOOD

* No database locks
* High performance
* Best for **read-heavy systems**

## ❌ When it fails

* High write contention
* Many concurrent updates

## One-Liner (Memorize This)

> *Optimistic locking uses a version column to detect concurrent modifications and prevents lost updates without database locks.*

---

# 🔒 Pessimistic Locking (JPA)

## 🧠 Core Idea

> **“Assume conflicts WILL happen, so block others immediately.”**

Unlike optimistic locking, **pessimistic locking uses database locks**.

## 🛠 How it is applied (VERY IMPORTANT)

Using `LockModeType`:

```java
Employee emp = entityManager.find(
    Employee.class,
    1L,
    LockModeType.PESSIMISTIC_WRITE
);
```

OR in JPQL:

```java
SELECT e FROM Employee e WHERE e.id = :id
```

```java
query.setLockMode(LockModeType.PESSIMISTIC_WRITE);
```

## 🔄 What happens internally

Database executes something like:

```sql
SELECT * FROM employee WHERE id = 1 FOR UPDATE;
```

👉 Row is **locked**
👉 Other transactions:

* Must **wait**, or
* Get **timeout / deadlock**

## 🔑 Types of Pessimistic Locks

| Lock Mode                     | Meaning                           |
| ----------------------------- | --------------------------------- |
| `PESSIMISTIC_READ`            | Others can read, not write        |
| `PESSIMISTIC_WRITE`           | Others can neither read nor write |
| `PESSIMISTIC_FORCE_INCREMENT` | Increments version                |

## ⚖ Optimistic vs Pessimistic

| Aspect            | Optimistic | Pessimistic |
| ----------------- | ---------- | ----------- |
| Locking           | No DB lock | DB lock     |
| Performance       | High       | Lower       |
| Conflict handling | On commit  | Immediately |
| Use case          | Read-heavy | Write-heavy |

## 🎯 When to use which

* **Optimistic** → Most web apps
* **Pessimistic** → Banking, inventory, seat booking

---


