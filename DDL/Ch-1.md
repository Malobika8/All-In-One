# JDBC — DDL Operations

DDL = **Data Definition Language**
Examples → `CREATE`, `ALTER`, `DROP`, `TRUNCATE`, `RENAME`

In JDBC, DDL commands are executed using:

```java
Statement stmt = connection.createStatement();
stmt.executeUpdate(sql);   // returns 0 for DDL
```

---

## 1. Write a `CREATE TABLE` statement for a table named `employees` with these columns:

* `id` — integer primary key (auto-incrementing)
* `full_name` — string up to 100 characters, not null
* `salary` — decimal with two fractional digits
* `joined_on` — date, default to current date

Write the exact MySQL `CREATE TABLE` statement.

### ->

```
CREATE TABLE employees (
    id INT PRIMARY KEY AUTO_INCREMENT,
    full_name VARCHAR(100) NOT NULL,
    salary DECIMAL(10,2),
    joined_on DATE DEFAULT CURRENT_DATE
);
```

---

## 2. Add a new column to the existing `employees` table:

* Column name: `department`
* Type: `VARCHAR(30)`
* Should allow NULL values

### ->

```
alter table employees
add column department varchar(30);
```

---

## 3. Modify the `salary` column to:

* `DECIMAL(12,2)`
* `NOT NULL`

Write the **ALTER TABLE** statement to update the column definition.

### ->

```
alter table employees
modify salary decimal(12, 2) not null;
```

---

## 4. Rename the column `full_name` to `employee_name` in the `employees` table.

Write the **ALTER TABLE** statement.

### ->

```
alter table employees
rename column full_name to employee_name;
```

---

## 5. Drop the column `department` from the `employees` table.

Write the **ALTER TABLE** statement.

### ->

```
alter table employees
drop column department;
```

---

## 6. Truncate the `employees` table so that:

* All rows are deleted
* Auto-increment counter resets

Write the **TRUNCATE TABLE** statement.

### ->

```
truncate table employees;
```

🔹 AUTO_INCREMENT in MySQL

* Columns like `id INT AUTO_INCREMENT` automatically generate a **unique sequential number** for each new row.
* MySQL keeps track of the **next number** internally.
  Example:

```sql
id
1
2
3
```

Next insert will get `4`.

🔹 What happens when you **TRUNCATE TABLE**?

* All rows are deleted **immediately**.
* The **internal counter for AUTO_INCREMENT is reset to 1** (or the starting value you defined).

Example:

```sql
TRUNCATE TABLE employees;
```

* All data gone.
* Next insert will get `id = 1`, even if the previous rows had `id = 10` or higher.
* Faster than `DELETE` for large tables because it **deallocates storage pages**, not row-by-row deletion.

🔹 Key Difference from DELETE

| Operation                | Rows removed        | AUTO_INCREMENT    | Rollback                      |
| ------------------------ | ------------------- | ----------------- | ----------------------------- |
| DELETE FROM employees    | Can remove all rows | Counter continues | Can rollback                  |
| TRUNCATE TABLE employees | All rows removed    | Counter reset     | Cannot rollback (auto-commit) |

* **DELETE FROM employees**

  * Suppose the last `id` was 10.
  * You delete all rows.
  * Next insert will get **id = 11**.
  * Auto-increment **does not reset**.

* **TRUNCATE TABLE employees**

  * Deletes all rows **and resets the counter**.
  * Next insert will get **id = 1** (or whatever starting value you defined).
    
TRUNCATE is **faster than DELETE for large tables** because it doesn’t log each row deletion — it deallocates storage pages directly.

🔹 DELETE Logging

* **DELETE** removes rows **one by one**.
* For each deleted row, MySQL logs the operation in the **transaction log (binary log / InnoDB redo log)**.
* This allows:

  * **Rollback** (undo the deletion if transaction not committed)
  * **Replication** (sending changes to slave servers)

Example:

```sql
DELETE FROM employees WHERE id = 5;
```

* Logs “DELETE row with id=5” in the transaction log.
* Can be rolled back if inside a transaction.

🔹 TRUNCATE Logging

* **TRUNCATE TABLE** is **DDL**, not DML.
* MySQL treats it as **drop + recreate table internally**.
* Logs only the **table-level operation**, not individual rows.
* Because of this:

  * Cannot rollback in InnoDB (auto-commit happens immediately)
  * Replication sees it as “table truncated” event, not row-by-row deletions

🔹 Key Difference (Logging)

| Operation | Logs stored                 | Can rollback? | Notes                       |
| --------- | --------------------------- | ------------- | --------------------------- |
| DELETE    | Row-level (transaction log) | Yes           | Slower for large tables     |
| TRUNCATE  | Table-level only            | No            | Fast, resets AUTO_INCREMENT |

**“Why is TRUNCATE faster than DELETE?”**, the answer is:

> Because TRUNCATE does **not log each row deletion**, it only logs the **table deallocation**, making it much faster for large tables.

---

## 7. Drop the `employees` table completely.

Write the **DROP TABLE** statement.

### ->

```
drop table employees
```

---

## 8. You have this table and view:

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(50),
    salary DECIMAL(10,2)
);

CREATE VIEW emp_view AS
SELECT emp_id, emp_name, salary
FROM employees;
```

Now you need to:

1. Add a new column `department VARCHAR(30)` to **employees**
2. Update the **view** so that it also includes the new column `department`
3. Later delete/drop the **view** without affecting the table

Write the SQL statements for all 3 operations.

### ->

```
ALTER TABLE employees
ADD COLUMN department VARCHAR(30);

CREATE OR REPLACE VIEW emp_view AS
SELECT emp_id, emp_name, salary, department
FROM employees;

DROP VIEW emp_view;
```

---

## 9. You have this table:

```sql
CREATE TABLE departments (
    dept_id INT PRIMARY KEY,
    dept_name VARCHAR(50)
);
```

Now perform the following operations **on employees table**:

1. Add a foreign key constraint on `department_id` referencing `departments(dept_id)`
2. Try to delete a row from `departments` that is referenced in `employees`
3. Then modify the foreign key so that deleting a department automatically deletes employees in that department

Write SQL statements for steps **1, 2, and 3**.

### ->

```
ALTER TABLE employees
ADD CONSTRAINT fk_name
FOREIGN KEY (department_id) REFERENCES departments(dept_id);

delete from departments where dept_id=1;
delete from employees where department_id=1;


-- 3
ALTER TABLE employees DROP FOREIGN KEY fk_name;

ALTER TABLE employees
ADD CONSTRAINT fk_name
FOREIGN KEY (department_id)
REFERENCES departments(dept_id)
ON DELETE CASCADE;
```

---

## 10. You have the table:

```sql
CREATE TABLE customers (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(50),
    email VARCHAR(100) UNIQUE
);
```

Perform the following:

1. Rename the table `customers` to `clients`
2. Rename column `name` to `full_name`
3. Change the `email` column to allow `NULL` instead of `UNIQUE`

### ->

```
ALTER TABLE customers RENAME TO clients;

ALTER TABLE clients RENAME COLUMN name TO full_name;

ALTER TABLE clients MODIFY email VARCHAR(100) NULL;
```

---

## 11. You have this table:

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    amount DECIMAL(10,2),
    order_date DATE
);
```

Perform the following:

1. Add a **CHECK constraint** so `amount` must be greater than 0
2. Later remove the CHECK constraint

### ->

```
ALTER TABLE orders
ADD CONSTRAINT check_ck CHECK (amount > 0);

ALTER TABLE orders
DROP CONSTRAINT check_ck;
```

---

## 12. You have this table:

```sql
CREATE TABLE bank_accounts (
    acc_no INT PRIMARY KEY,
    holder VARCHAR(50),
    balance DECIMAL(10,2)
);
```

Perform the following:

1. Change the table name to `accounts`
2. Add a new column `branch VARCHAR(30)`
3. Rename column `holder` to `account_holder`

### ->

```
ALTER TABLE bank_accounts RENAME TO accounts;

alter table accounts add column branch varchar(30);

ALTER TABLE accounts RENAME COLUMN holder TO account_holder;
```

---

## 13. You have a table:

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    name VARCHAR(50),
    price DECIMAL(10,2)
);
```

Perform the following:

1. Create a copy of the table structure (no data)
2. Create a full copy of the table including data

### ->

```
create table duplicateproducts like products;

CREATE TABLE duplicatepro AS
SELECT * FROM products;
```

---

## 14. You have this table:

```sql
CREATE TABLE transactions (
    txn_id INT PRIMARY KEY,
    amount DECIMAL(10,2),
    status VARCHAR(20)
);
```

Perform the following:

1. Add a column `created_on` of type `DATETIME` with default current timestamp
2. Add a **UNIQUE** constraint on `status`
3. Remove the UNIQUE constraint later

### ->

```
ALTER TABLE transactions
ADD COLUMN created_on DATETIME DEFAULT CURRENT_TIMESTAMP;

```


