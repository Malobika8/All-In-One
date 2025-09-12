## 🔹 Stored Procedures vs Functions

### 1. **Stored Procedure**

* A **named block of SQL code** stored in the database.
* Can accept **input/output parameters**.
* Can contain multiple SQL statements (`SELECT`, `INSERT`, `UPDATE`, `DELETE`).
* Can include logic (IF, WHILE, loops, error handling).
* Used for **business logic**, batch operations, or encapsulating workflows.
* **Does not necessarily return a value** (but can return output parameters or result sets).

Example (MySQL style):

```sql
DELIMITER $$
CREATE PROCEDURE GetHighSalaryEmployees(IN min_salary INT)
BEGIN
   SELECT emp_id, name, salary
   FROM Employees
   WHERE salary > min_salary;
END$$
DELIMITER ;
```

Call it:

```sql
CALL GetHighSalaryEmployees(60000);
```

### 2. **Function**

* Similar to procedures, but:

  * **Must return exactly one value** (scalar or table).
  * Can be used inside SQL statements (e.g., in `SELECT`, `WHERE`).
  * Generally used for **calculations** or **transformations**, not for big business logic.

Example:

```sql
CREATE FUNCTION BonusCalculator(salary INT)
RETURNS INT
DETERMINISTIC
BEGIN
   RETURN salary * 0.1;
END;
```

Use it like:

```sql
SELECT name, salary, BonusCalculator(salary) AS bonus
FROM Employees;
```

## 🔹 Key Differences

| Feature               | Stored Procedure                                      | Function                               |
| --------------------- | ----------------------------------------------------- | -------------------------------------- |
| Return value          | Optional (can return multiple result sets/OUT params) | Must return exactly one value          |
| Use in SQL statements | Cannot be used in `SELECT`                            | Can be used in `SELECT`, `WHERE`, etc. |
| Complexity            | For business logic/workflows                          | For calculations/transformations       |
| Transaction control   | Can use COMMIT/ROLLBACK                               | Not allowed in most DBs                |
| Parameters            | IN, OUT, INOUT                                        | Only IN parameters                     |

## 🔹 When to Use What?

* **Procedure** → If you want to **perform an action** (e.g., update salaries, insert logs).
* **Function** → If you want to **compute and return a value** (e.g., calculate tax, format strings).

---

## 🏢 Real-World Scenario

Suppose we’re building a simple HR system in MySQL.

### 1. **Function for calculation**

We want to calculate **annual bonus** for an employee (10% of salary).

```sql
DELIMITER $$

CREATE FUNCTION AnnualBonus(salary DECIMAL(10,2))
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
   RETURN salary * 0.10;
END$$

DELIMITER ;
```

Usage:

```sql
SELECT emp_id, name, salary, AnnualBonus(salary) AS bonus
FROM Employees;
```
### 2. **Procedure for action**

We want to give a **salary raise of 5% to all employees in a department**.

```sql
DELIMITER $$

CREATE PROCEDURE GiveRaise(IN dept VARCHAR(50))
BEGIN
   UPDATE Employees
   SET salary = salary * 1.05
   WHERE dept_name = dept;
END$$

DELIMITER ;
```

Usage:

```sql
CALL GiveRaise('Engineering');
```

---

## Questions

1. **Conceptual**:

   * What’s the difference between a stored procedure and a function in MySQL?
   * Can a stored procedure be used inside a `SELECT` query? Why or why not?
   * Can a function modify data in MySQL (e.g., `INSERT` or `UPDATE`)?

2. **Practical**:

   * Write a function that takes `salary` and `tax_rate` as input, and returns net salary.
   * Write a procedure that deletes all employees with salary < 30000.
   * How would you modify a procedure to return multiple values (e.g., OUT parameters)?

### Explanation:

#### Conceptual:

1. **Stored Procedure**

   * Correct ✅: It can return nothing, a result set, or OUT parameters.
   * Correct ✅: It can’t be used in a `SELECT`, because `SELECT` expects a scalar/table result and procedures don’t guarantee that.

2. **Function**

   * Always returns exactly **one value**.
   * In MySQL, a **function cannot modify data** (like `INSERT`, `UPDATE`, `DELETE`).
     * By design, functions should be *deterministic and side-effect free*.
     * If you try DML inside a function, MySQL will throw an error (`Not allowed to return a result set from a function`).

👉 So:

* Use **procedure** for data modifications.
* Use **function** for returning calculated values.

#### Practical

a) Function for net salary

```sql
DELIMITER $$

CREATE FUNCTION netSalaryCalculator(salary DECIMAL(10,2), tax_rate DECIMAL(5,2))
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
   RETURN salary - (salary * tax_rate / 100);
END$$

DELIMITER ;
```

Usage:

```sql
SELECT name, netSalaryCalculator(salary, 10) AS net_salary FROM Employees;
```

b) Procedure to delete employees with salary < 30000

```sql
DELIMITER $$

CREATE PROCEDURE deleteLowSalaryEmployees()
BEGIN
   DELETE FROM Employees WHERE salary < 30000;
END$$

DELIMITER ;
```

Call it:

```sql
CALL deleteLowSalaryEmployees();
```

c) Returning multiple values from a procedure

In MySQL, this is done using **OUT parameters**.

```sql
DELIMITER $$

CREATE PROCEDURE GetEmployeeStats(OUT total_emps INT, OUT avg_salary DECIMAL(10,2))
BEGIN
   SELECT COUNT(*) INTO total_emps FROM Employees;
   SELECT AVG(salary) INTO avg_salary FROM Employees;
END$$

DELIMITER ;
```

Call it:

```sql
CALL GetEmployeeStats(@total, @avg);
SELECT @total AS total_employees, @avg AS avg_salary;
```

✅ So:
* **Procedures** → for actions (can return OUT params, multiple values, or result sets).
* **Functions** → for calculations (must return 1 value, no side effects).

---

## Question: Suppose you want to **log every login attempt** (username + timestamp) into a table. Would you use a **stored procedure** or a **function** here, and why?

### Explanation:
* **Stored Procedure** is the right choice here because:

  * You want to **perform an action** (insert into a table).
  * There’s no single value to return.
  * Procedures in MySQL can handle inserts/updates/deletes easily.

👉 Example in MySQL:

```sql
DELIMITER $$

CREATE PROCEDURE LogLogin(IN uname VARCHAR(50))
BEGIN
   INSERT INTO LoginHistory(username, login_time)
   VALUES (uname, NOW());
END$$

DELIMITER ;
```

Call it when a user logs in:

```sql
CALL LogLogin('Alice');
```

This will store `"Alice"` + current timestamp in the `LoginHistory` table.
Whereas a **function** wouldn’t fit here, because it must **return a single value** and isn’t meant for actions like inserts/updates.

---

# DETERMINISTIC

### What does *DETERMINISTIC* mean?

When you create a function in MySQL, you can (optionally) tell MySQL whether the function will **always return the same output for the same input**.

* **DETERMINISTIC** → Output depends only on input values, not on anything else.
  Example:

  ```sql
  CREATE FUNCTION squareNum(n INT)
  RETURNS INT
  DETERMINISTIC
  RETURN n * n;
  ```

  * If you pass `5`, it will *always* return `25`.
  * No randomness, no dependence on external data.

* **NOT DETERMINISTIC** → Output may vary even for the same input.
  Example:

  ```sql
  CREATE FUNCTION randomValue(n INT)
  RETURNS INT
  NOT DETERMINISTIC
  RETURN RAND() * n;
  ```

  * For input `10`, result can be `3`, `7`, `9`… changes every call.

### Why does MySQL care?

MySQL cares because of **query optimization and replication**:

* If a function is **DETERMINISTIC**, MySQL can safely **cache results** or optimize queries better.
* In replication setups, knowing if a function is deterministic ensures **consistent results** across master and replica servers.

### Do we need to write it?

* **Yes, for functions** → You should declare `DETERMINISTIC` or `NOT DETERMINISTIC`.
  If you don’t, MySQL assumes **NOT DETERMINISTIC** by default.
* **For stored procedures** → Not required, only applies to functions.

👉 Best practice: If your function is a pure calculation (no randomness, no external state), declare it `DETERMINISTIC`.

---

