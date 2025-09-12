# 🔹 What is a Trigger?

* A **trigger** is a special stored program that **automatically runs** when a specific event happens on a table.
* Events: `INSERT`, `UPDATE`, or `DELETE`.
* Timing: `BEFORE` or `AFTER` the event.

So, a trigger is basically **“if something happens on this table, do this automatically.”**

### 🔹 Example Scenario

Suppose we want to **log all salary updates** into another table `salary_audit`.

1. Create an audit table:

   ```sql
   CREATE TABLE salary_audit (
       emp_id INT,
       old_salary DECIMAL(10,2),
       new_salary DECIMAL(10,2),
       change_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP
   );
   ```

2. Create a trigger:

   ```sql
   DELIMITER $$

   CREATE TRIGGER after_salary_update
   AFTER UPDATE ON employees
   FOR EACH ROW
   BEGIN
       INSERT INTO salary_audit(emp_id, old_salary, new_salary)
       VALUES (OLD.emp_id, OLD.salary, NEW.salary);
   END$$

   DELIMITER ;
   ```

👉 Now whenever `employees.salary` is updated, MySQL **automatically inserts a row** into `salary_audit`.

### 🔹 Key Points to Remember

1. `OLD` → holds the row values before change.
2. `NEW` → holds the row values after change (only for `INSERT`/`UPDATE`).
3. `BEFORE` triggers can modify `NEW` values before they are written.
4. `AFTER` triggers can only **log or validate**; they can’t change data.
5. Triggers are **per row** (fires for each row affected).

---

# Q1 (Trigger – Insert Logging)
Suppose you have a table `users(id INT, username VARCHAR(50), created_at TIMESTAMP)`. Create a trigger `before_user_insert` that:
* Automatically sets `created_at = NOW()` before a new user is inserted (so you don’t have to supply it manually).

### Explanation:

```sql
DELIMITER $$

CREATE TRIGGER before_user_insert
BEFORE INSERT ON users
FOR EACH ROW
BEGIN
    SET NEW.created_at = NOW();
END$$

DELIMITER ;
```

---



