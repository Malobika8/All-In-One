## 15. Same table:

```sql
CREATE TABLE transactions (
    txn_id INT PRIMARY KEY,
    amount DECIMAL(10,2),
    status VARCHAR(20)
);
```

Now perform:

**Add a UNIQUE constraint on `status` column.**

### ->

```
ALTER TABLE transactions
ADD CONSTRAINT uk_status UNIQUE (status);
```

---

## 16. Same table:

```sql
CREATE TABLE transactions (
    txn_id INT PRIMARY KEY,
    amount DECIMAL(10,2),
    status VARCHAR(20),
    created_on DATETIME DEFAULT CURRENT_TIMESTAMP
);
```

Now remove the **UNIQUE** constraint on `status` that you created earlier (`uk_status`).

📌 Write only the SQL for dropping the constraint.

### ->

```
alter table transactions drop index uk_status;
```

---

## 17. You have this table:

```sql
CREATE TABLE employees (
    emp_id INT PRIMARY KEY AUTO_INCREMENT,
    emp_name VARCHAR(100),
    salary DECIMAL(10,2),
    dept_id INT
);
```

You need to perform the following schema changes **in order**:

1. Add a column `email VARCHAR(100) UNIQUE`
2. Modify `salary` to `DECIMAL(12,2) NOT NULL`
3. Add a foreign key on `dept_id` referencing `departments(dept_id)` with **ON DELETE SET NULL**
4. Rename the table `employees` to `company_employees`
5. Drop the **email** column later

### ->

```
alter table employees add column email varchar(100) unique;

alter table employees modify salary decimal(12,2) not null;

ALTER TABLE employees
ADD CONSTRAINT fk_key
FOREIGN KEY (dept_id)
REFERENCES departments(dept_id)
ON DELETE SET NULL;

alter table employees rename to company_employees;

alter table company_employees drop column email;
```

