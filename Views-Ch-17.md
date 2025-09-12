# What is a View?

* A **View** is a **virtual table** based on the result of a SQL query.
* It doesn’t store data physically (except in case of *materialized views* in some databases).
* Instead, it stores the **query definition**, and whenever you query the view, the underlying query runs.

### Why use Views?

1. **Security** – You can expose only specific columns/rows from a table (e.g., hide salary column from employees).
2. **Simplification** – Complex joins/subqueries can be saved as a view, so developers just query the view.
3. **Consistency** – Ensure everyone uses the same query logic.
4. **Reusability** – One view can be reused across multiple applications/reports.
   
### Creating a View

```sql
CREATE VIEW EmployeeDept AS
SELECT e.emp_id, e.name, d.dept_name
FROM Employees e
JOIN Departments d ON e.dept_id = d.dept_id;
```

Now you can query it like a table:

```sql
SELECT * FROM EmployeeDept WHERE dept_name = 'HR';
```

### Updating Through Views

* Some views are **updatable** – meaning you can `INSERT`, `UPDATE`, or `DELETE` through them.
* Rules for updatable views:

  * Must be based on a single table.
  * Should not use `DISTINCT`, `GROUP BY`, `HAVING`, `UNION`, `JOIN`, or aggregate functions.

Example:

```sql
CREATE VIEW EmpBasic AS
SELECT emp_id, name, salary
FROM Employees;
```

You can do:

```sql
UPDATE EmpBasic SET salary = 60000 WHERE emp_id = 101;
```
### Dropping a View

```sql
DROP VIEW EmployeeDept;
```

---

# Indexes vs Views – Storage Perspective

**Indexes**

* Yes ✅ indexes are stored **physically** in the database.
* They create extra data structures (usually B-Trees, sometimes Hashes, depending on DB).
* That’s why they consume **disk space** and need to be updated when data changes.

**Views**

* A **view does not store data** (unless it’s a **materialized view**).
* What’s stored is only the **SQL query definition** (metadata) inside the system catalog of the database.
* When you query a view:

  * The DB engine substitutes the view definition into your query.
  * It’s as if you copied and pasted the underlying SELECT query.
  * The actual data is always fetched from the base tables.

### Where do Views “stay”?

* Views live in the **system catalog / data dictionary** of the database.
* For example:

  * In **MySQL**, views are stored in the `information_schema.VIEWS` table.
  * In **PostgreSQL**, they’re in `pg_views`.
  * In **SQL Server**, they’re in `sys.views`.

👉 So, a view = just a **named query stored in metadata**, not a separate physical table.

### Materialized Views (Special Case)

* Some DBs (Oracle, PostgreSQL, etc.) allow **Materialized Views**.
* Unlike normal views, they **store data physically**, like a snapshot of the query result.
* They can be refreshed (`ON DEMAND` or `ON COMMIT`).
* Use case: heavy aggregations or joins that you don’t want to recompute every time.

✅ Summary:

* **Indexes** = physical structures on disk.
* **Views** = just query definitions stored in metadata, no physical storage.
* **Materialized Views** = views + physical storage of results.

---

# 🔹 Why use Views if data still comes from the main table?

* A **view never has its own independent data** (unless materialized).
* It always pulls from the base table(s).

👉 So the power of views is **not about storage**, but about **abstraction, security, and simplicity**.

### Main Benefits of Views

1. **Simplify Complex Queries**

   * Imagine you have a query with 5 joins, filters, and calculations.
   * Instead of rewriting that monster query in 10 places, you can wrap it in a view:

     ```sql
     CREATE VIEW SalesReport AS
     SELECT c.customer_name, SUM(o.amount) total_sales
     FROM Customers c
     JOIN Orders o ON c.id = o.customer_id
     GROUP BY c.customer_name;
     ```

     Now anyone can just do:

     ```sql
     SELECT * FROM SalesReport WHERE total_sales > 5000;
     ```

     👉 Less code duplication, easier maintenance.

2. **Security / Data Hiding**

   * Suppose your `Employees` table has sensitive columns like `salary` or `ssn`.
   * You don’t want every developer/app to see them.
   * You can expose only safe columns via a view:

     ```sql
     CREATE VIEW PublicEmployees AS
     SELECT emp_id, name, dept
     FROM Employees;
     ```

     👉 Applications can query this view safely, without ever touching sensitive columns.

3. **Consistency & Reuse**

   * Let’s say “high salary employee” is defined as `salary > 80000`.
   * If 10 different developers write queries, they may use `salary > 75000` or `> 80000` inconsistently.
   * A view standardizes the logic:

     ```sql
     CREATE VIEW HighSalaryEmployees AS
     SELECT emp_id, name, salary FROM Employees WHERE salary > 80000;
     ```

     👉 Everyone now refers to the same business rule.

4. **Logical Data Independence**

   * Suppose your schema changes — e.g., you split `full_name` into `first_name` + `last_name`.
   * If all apps directly query the table, you need to fix them all.
   * But if they query a view that still provides `full_name`, you only fix the view once.

### Analogy

Think of a **view as a shortcut / saved lens** into your database:

* Tables = the raw data.
* Views = a *predefined perspective* of that data.
* Just like in Java, you don’t always expose your raw data structures — you create **APIs** or **DTOs** that provide a safe, simplified, and consistent interface.

✅ So the point of views is:

* Not to store data,
* But to give you a **named, reusable, secure, simplified, consistent way** to look at the underlying data.

---

# Question: Suppose you have a view created as:

```sql
CREATE VIEW HighSalary AS
SELECT emp_id, name, salary
FROM Employees
WHERE salary > 50000;
```

Can you `INSERT` a new employee through this view? Why or why not?

### Explanation:

* The view `HighSalary` is defined with a **WHERE condition (`salary > 50000`)**.
* If you try to `INSERT` through this view:

  * The database will check if the row satisfies the condition.
  * If the salary is **≤ 50000**, the row won’t appear in the view (and in many DBs, the insert will fail).
  * Even if salary > 50000, some databases may still not allow insert/update if the view is not marked explicitly as **updatable**.

So practically, most databases **do not allow inserting** through such filtered views, unless you add special rules (`WITH CHECK OPTION` in SQL).

#### WITH CHECK OPTION

If you create the view as:

```sql
CREATE VIEW HighSalary AS
SELECT emp_id, name, salary
FROM Employees
WHERE salary > 50000
WITH CHECK OPTION;
```

Now:

* Any `INSERT` or `UPDATE` through this view must satisfy the condition (`salary > 50000`).
* Otherwise, the statement will fail.

---

# Real-world scenario

### 🏢 Example: Employee Database

#### Tables

**Employees**

| emp\_id | name    | dept\_id | salary | ssn         |
| ------- | ------- | -------- | ------ | ----------- |
| 101     | Alice   | 1        | 90000  | 123-45-6789 |
| 102     | Bob     | 2        | 50000  | 987-65-4321 |
| 103     | Charlie | 1        | 70000  | 456-78-1234 |

**Departments**

| dept\_id | dept\_name  |
| -------- | ----------- |
| 1        | HR          |
| 2        | Engineering |

### Problem Without Views

Suppose management asks:

> "Give us a report of employee name, department name, and salary for employees earning more than 60k."

Query each time:

```sql
SELECT e.name, d.dept_name, e.salary
FROM Employees e
JOIN Departments d ON e.dept_id = d.dept_id
WHERE e.salary > 60000;
```

Now imagine:

* This query is used in **10 reports**,
* Developers may forget the exact join condition,
* Someone might apply `salary >= 60000` instead of `> 60000`.

👉 Leads to **duplication** and **inconsistency**.

### Solution With a View

Create a view once:

```sql
CREATE VIEW HighEarners AS
SELECT e.name, d.dept_name, e.salary
FROM Employees e
JOIN Departments d ON e.dept_id = d.dept_id
WHERE e.salary > 60000;
```

Now the report query is dead simple:

```sql
SELECT * FROM HighEarners;
```

👉 Benefits:

* **Developers don’t need to know the join logic.**
* **Everyone uses the same salary > 60000 rule.**
* **Query is shorter, cleaner, and less error-prone.**
* **Sensitive info (`ssn`) never leaves the base table.**

### Real-World Use Case (Java App)

In a Java microservice, instead of writing a long query in code, you might just call:

```sql
SELECT * FROM HighEarners WHERE dept_name = 'HR';
```

and map the results to your DTO.

👉 The business rule (`salary > 60000`) is centralized in the DB, not scattered across the codebase.

✅ That’s the real power of views: **abstraction, simplification, security, and consistency**.

---

