## JPA Entity Lifecycle + Dirty Checking

#### What is the Entity Lifecycle?

An entity in JPA goes through **4 main states** (you already learned this, now with deeper focus):

| State         | Description                                     |
| ------------- | ----------------------------------------------- |
| **Transient** | New object, not in DB, not managed              |
| **Managed**   | Attached to persistence context, tracked by JPA |
| **Detached**  | Was managed, now out of context                 |
| **Removed**   | Marked for deletion, deleted on commit          |

#### What is Dirty Checking?

> Dirty checking = automatic detection of changes made to managed entities.

When you update a managed entity (no need to call `merge` or write `UPDATE`), JPA will:

* Check if the entity’s state has changed
* If yes, it automatically generates an `UPDATE` query **on commit**

#### Example:

```java
em.getTransaction().begin();

Employee emp = em.find(Employee.class, 1); // managed
emp.setSalary(70000); // dirty checking will detect this

em.getTransaction().commit();
```

✅ You don’t need to call `em.merge()` — JPA tracks the change and flushes the update.

#### ❗Gotcha:

Dirty checking only works on:

* Managed entities (not detached or transient)
* During an open transaction

---

# What will happen here?

```java
Employee emp = em.find(Employee.class, 1);
emp.setName("Updated Name");
em.getTransaction().commit();
```

You did **not call `em.getTransaction().begin()`** — just commit.
Will the change be saved? What will happen?

### Sol:

We never started a transaction with em.getTransaction().begin();

In JPA, without a transaction, no DB operation (insert, update, delete) will be flushed — even for managed entities.

The change (emp.setName(...)) will not be saved, because there was no active transaction.
Calling em.getTransaction().commit() without begin() throws an IllegalStateException.

Dirty checking happens only for managed entities inside an active transaction.
If you don’t call begin(), even managed entity changes won’t be saved.

---

# Perfect — let's first do a **dirty checking coding challenge**, and then we’ll go into **first-level cache (persistence context)** right after.

---

# Dirty Checking Coding Challenge

You have an `Employee` entity with `id`, `name`, and `salary`.

Write JPA code to:

1. Load an employee with ID 10
2. Increase their salary by 5000
3. Commit the change using **only dirty checking**
4. Don’t use `merge()` or `update` manually

### Sol:

```java
em.getTransaction().begin();
Employee emp = em.find(Employee.class, 10);
emp.setSalary(emp.getSalary()+5000);
em.getTransaction().commit();
```
