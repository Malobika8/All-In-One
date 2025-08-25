### 1. The Employee Table

Let’s say we have this table:

**employees**

| emp\_id | name    | manager\_id |
| ------- | ------- | ----------- |
| 1       | Alice   | NULL        |
| 2       | Bob     | 1           |
| 3       | Charlie | 1           |
| 4       | David   | 2           |
| 5       | Emma    | 2           |
| 6       | Frank   | 3           |

* `emp_id` → Unique for each employee
* `manager_id` → Points to another employee’s `emp_id` (the manager).
* If `manager_id` is `NULL`, that person (Alice) has **no manager** (top boss).

---

### 2. The Need for SELF JOIN

👉 The manager is also an employee, so both employees and managers live in the **same table**.
👉 To display *employee name* along with *manager name*, we join the **employees table with itself**.

---

### 3. SELF JOIN Query

```sql
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id;
```

---

### 4. Result

| employee | manager |
| -------- | ------- |
| Alice    | NULL    |
| Bob      | Alice   |
| Charlie  | Alice   |
| David    | Bob     |
| Emma     | Bob     |
| Frank    | Charlie |

---

✅ Notes:

* We alias the table as `e` (employee) and `m` (manager).
* `e.manager_id = m.emp_id` → links employee’s manager to manager’s record.
* `LEFT JOIN` ensures even employees without a manager (Alice) show up.

---

### Table Reminder (employees)

| emp\_id | name    | manager\_id |
| ------- | ------- | ----------- |
| 1       | Alice   | NULL        |
| 2       | Bob     | 1           |
| 3       | Charlie | 1           |
| 4       | David   | 2           |
| 5       | Emma    | 2           |
| 6       | Frank   | 3           |

### 📝 Practice Problems

1. **List all employees with their managers (we did this one already).**

```sql
SELECT e.name AS employee, m.name AS manager
FROM employees e
LEFT JOIN employees m
ON e.manager_id = m.emp_id;
```

2. **Find all employees who are also managers (i.e., at least one person reports to them).**
   👉 (Hint: If someone’s emp\_id appears as another’s manager\_id)

3. **Find all employees who do NOT have a manager.**
   👉 (Hint: manager\_id IS NULL)

4. **Find the number of employees reporting to each manager.**
   👉 (Hint: GROUP BY manager)

5. **Find the hierarchy: employee → manager → manager’s manager.**
   👉 (Hint: SELF JOIN twice)


2. ```sql
   select e.name 
   from employees e 
   inner join employees m 
   on e.emp_id = m.manager_id;
   ```

3. ```sql
   select name 
   from employees 
   where manager_id is null;
   ```

4. ```sql
   select m.name as manager, count(e.emp_id) as num_reports
   from employees e
   inner join employees m
   on e.manager_id = m.emp_id
   group by m.name;
   ```

5. ```sql
   select e.name as employee, 
       m.name as manager, 
       mm.name as managers_manager
   from employees e
   left join employees m 
       on e.manager_id = m.emp_id
   left join employees mm
       on m.manager_id = mm.emp_id;
   ```

---

# Understanding the diff. 

Consider the employee table

| emp\_id | name    | manager\_id |
| ------- | ------- | ----------- |
| 1       | Alice   | NULL        |
| 2       | Bob     | 1           |
| 3       | Charlie | 1           |
| 4       | David   | 2           |
| 5       | Emma    | 2           |
| 6       | Frank   | 3           |

### Case A: ❌ Wrong join

```sql
... on e.emp_id = m.manager_id
```

👉 Means: "match employees whose **id = some other’s manager\_id**."
So it pairs **employee = manager-of-someone**.

Result of the join:

| e.emp\_id | e.name  | e.manager\_id | m.emp\_id | m.name  | m.manager\_id |
| --------- | ------- | ------------- | --------- | ------- | ------------- |
| 1         | Alice   | NULL          | 2         | Bob     | 1             |
| 1         | Alice   | NULL          | 3         | Charlie | 1             |
| 2         | Bob     | 1             | 4         | David   | 2             |
| 2         | Bob     | 1             | 5         | Emma    | 2             |
| 3         | Charlie | 1             | 6         | Frank   | 3             |

🛑 Problem: Here **e is manager** and **m is employee**, but you meant the opposite!
So when you `count(e.emp_id)`, you’re not really counting employees per manager correctly.

### Case B: ✅ Correct join

```sql
... on e.manager_id = m.emp_id
```

👉 Means: "match an employee’s **manager\_id** to the manager’s **emp\_id**."

Result of the join:

| e.emp\_id | e.name  | e.manager\_id | m.emp\_id | m.name  | m.manager\_id |
| --------- | ------- | ------------- | --------- | ------- | ------------- |
| 2         | Bob     | 1             | 1         | Alice   | NULL          |
| 3         | Charlie | 1             | 1         | Alice   | NULL          |
| 4         | David   | 2             | 2         | Bob     | 1             |
| 5         | Emma    | 2             | 2         | Bob     | 1             |
| 6         | Frank   | 3             | 3         | Charlie | 1             |

✔ This is the **employee → manager mapping** we want.
Now grouping by `m.name` gives correct counts:

* Alice → 2 (Bob, Charlie)
* Bob → 2 (David, Emma)
* Charlie → 1 (Frank)

So the difference:

* `e.emp_id = m.manager_id` → treats **employee as manager**, flipping roles.
* `e.manager_id = m.emp_id` → correctly matches **employee → their manager**.



