# Let’s Recreate the Problem Mentally

Suppose:

* You don’t use `@Version`
* Two users update different fields

User A:

```
salary = 6000
```

User B:

```
department = "HR"
```

But your code does:

```java
emp.setDepartment(...)
emp.setSalary(...)
```

And both are using stale data. What subtle bug might happen here?

# What Actually Happens Without `@Version`

Let’s simulate properly.

### Step 1 — Both load same snapshot

Both users read:

```
salary = 5000
department = IT
```

### Step 2 — User 1 updates salary

User 1 sends full PUT body:

```json
{
  "salary": 6000,
  "department": "IT"
}
```

DB becomes:

```
salary = 6000
department = IT
```

### Step 3 — User 2 updates department

But User 2 still has OLD snapshot:

```
salary = 5000
department = IT
```

User 2 sends:

```json
{
  "salary": 5000,
  "department": "HR"
}
```

⚠️ Notice salary = 5000 (stale value)

Now your service does:

```java
emp.setSalary(employee.getSalary());      // 5000 (stale)
emp.setDepartment(employee.getDepartment()); // HR
```

DB becomes:

```
salary = 5000
department = HR
```
User 1’s update (6000) is LOST.

# This Is the Subtle Bug

It is NOT just about different fields.

Because you are replacing the entire object state.

This is called:

> Lost Update due to stale snapshot overwrite

Very common in REST APIs using PUT.

# 🎯 Why @Version Fixes This

With:

```java
@Version
private Long version;
```

User 2’s update will try:

```sql
WHERE id = 1 AND version = 1
```

But version is already 2.

So:

👉 0 rows updated
👉 OptimisticLockException
👉 No silent overwrite

# The Real Production Lesson

Without optimistic locking:

* You won’t even know data was overwritten.
* No error.
* No log.
* Silent corruption.

With optimistic locking:

* Conflict detected.
* Safe failure.

# Why is optimistic locking important in REST APIs?

> Because REST APIs typically send full resource representations. If two users update the same entity concurrently without version control, the later update can overwrite the earlier one using stale data, leading to silent lost updates.



