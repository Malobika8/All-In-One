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

# Q2 (Trigger – Update Auditing)

Suppose you have these tables:

**employees**
\| emp\_id | name | salary |

**salary\_audit**
\| emp\_id | old\_salary | new\_salary | change\_time |

Create a trigger `after_salary_update` that:

* Fires **AFTER UPDATE** on `employees`
* Inserts a row into `salary_audit` with:

  * `emp_id`
  * `old_salary` (before change)
  * `new_salary` (after change)
  * `change_time` as the current timestamp

### Explanation:

```sql
DELIMITER $$

CREATE TRIGGER after_salary_update
AFTER UPDATE ON employees
FOR EACH ROW
BEGIN
    INSERT INTO salary_audit(emp_id, old_salary, new_salary, change_time)
    VALUES (OLD.emp_id, OLD.salary, NEW.salary, NOW());
END$$

DELIMITER ;
```

---

# Q3 (Trigger – BEFORE DELETE)

Suppose you have these tables:

**employees**
\| emp\_id | name | salary |

**deleted\_employees**
\| emp\_id | name | salary | deleted\_at |

Create a trigger `before_employee_delete` that:

* Fires **BEFORE DELETE** on `employees`
* Inserts the row being deleted into `deleted_employees`

  * Include `deleted_at` as the current timestamp

### Explanation:

```sql
DELIMITER $$

CREATE TRIGGER before_employee_delete
BEFORE DELETE ON employees
FOR EACH ROW
BEGIN
    INSERT INTO deleted_employees(emp_id, name, salary, deleted_at)
    VALUES (OLD.emp_id, OLD.name, OLD.salary, NOW());
END$$

DELIMITER ;
```
---

# Q4 (Trigger – BEFORE UPDATE Rule Enforcement)

You have the table **employees**:

\| emp\_id | name | salary |

Create a trigger `before_salary_update` that:

* Fires **BEFORE UPDATE** on `employees`
* Prevents the salary from being updated to **less than 30,000**
* If someone tries to set it below 30,000, force it to stay at 30,000

### Explanation:

```sql
DELIMITER $$

CREATE TRIGGER before_salary_update
BEFORE UPDATE ON employees
FOR EACH ROW
BEGIN
    IF NEW.salary < 30000 THEN
        SET NEW.salary = 30000;
    END IF;
END$$

DELIMITER ;
```

---

# Q5: `AFTER INSERT` trigger

Requirement: Whenever a new employee is added to the `employees` table, insert a record into a log table `employee_audit` with details like `emp_id`, `name`, and `created_at`.

### Explanation:

First, let’s create the log table:

```sql
CREATE TABLE employee_audit (
    audit_id INT AUTO_INCREMENT PRIMARY KEY,
    emp_id INT,
    emp_name VARCHAR(100),
    action_time TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

Now, write the trigger:

```sql
DELIMITER $$

CREATE TRIGGER after_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_audit (emp_id, emp_name)
    VALUES (NEW.emp_id, NEW.name);
END$$

DELIMITER ;
```

Now, if you run:

```sql
INSERT INTO employees (emp_id, name, salary) VALUES (105, 'Ravi', 50000);
```

You’ll automatically get a row in `employee_audit` saying that Ravi was added.

---

# Quick Summary

## 🔹 What is a Trigger?

A **trigger** is a block of SQL code that executes automatically in response to an **INSERT, UPDATE, or DELETE** event on a table.

## Types of Triggers

1. **BEFORE Triggers**

   * Run before the row is inserted/updated/deleted.
   * Useful for **validation or modification**.

   ```sql
   DELIMITER $$  
   CREATE TRIGGER before_salary_update
   BEFORE UPDATE ON employees
   FOR EACH ROW
   BEGIN
     IF NEW.salary < 30000 THEN
       SET NEW.salary = 30000;
     END IF;
   END$$  
   DELIMITER ;
   ```

2. **AFTER Triggers**

   * Run after the row has been inserted/updated/deleted.
   * Useful for **logging, auditing, history tracking**.

   ```sql
   DELIMITER $$  
   CREATE TRIGGER after_salary_update
   AFTER UPDATE ON employees
   FOR EACH ROW
   BEGIN
     INSERT INTO salary_audit(emp_id, old_salary, new_salary, changed_at)
     VALUES(OLD.emp_id, OLD.salary, NEW.salary, NOW());
   END$$  
   DELIMITER ;
   ```

### Accessing Values

* **NEW\.column\_name** → new value being inserted/updated.
* **OLD.column\_name** → existing value before update/delete.

### Example: BEFORE INSERT

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

### Example: BEFORE DELETE

```sql
DELIMITER $$
CREATE TRIGGER before_employee_delete
BEFORE DELETE ON employees
FOR EACH ROW
BEGIN
  INSERT INTO deleted_employees(emp_id, name, salary, deleted_at)
  VALUES(OLD.emp_id, OLD.name, OLD.salary, NOW());
END$$
DELIMITER ;
```

### Key Points

* **Purpose**: automation, validation, auditing, history.
* **BEFORE vs AFTER**:

  * BEFORE → validation/change values.
  * AFTER → logging/history.
* **FOR EACH ROW** → applies to every row affected.
* **Limitations**: cannot commit/rollback inside trigger, careful with recursion.

---



