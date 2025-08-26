## 1️⃣ What is a Window Function?

A **window function** performs a calculation **across a set of table rows related to the current row**, without collapsing them like `GROUP BY` does.

* Unlike `GROUP BY`, **all rows are preserved**.
* The set of rows considered is called a **window**.

**Syntax (simplified):**

```sql
<window_function>() OVER (
    [PARTITION BY column1, column2, ...] 
    [ORDER BY column3, ...]
)
```

* `PARTITION BY` → splits rows into groups (like `GROUP BY`)
* `ORDER BY` → defines order within the window
* Common functions: `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `LEAD()`, `LAG()`, `SUM() OVER(...)`, etc.

---

## 2️⃣ Example Table

Let’s use a **sales table**:

| emp\_id | emp\_name | dept | salary |
| ------- | --------- | ---- | ------ |
| 1       | Alice     | HR   | 5000   |
| 2       | Bob       | IT   | 6000   |
| 3       | Carol     | HR   | 5500   |
| 4       | Dave      | IT   | 7000   |
| 5       | Eve       | IT   | 6000   |

---

## 3️⃣ Basic Example: ROW\_NUMBER()

Assign a unique number to each employee **within each department**, ordered by salary descending:

```sql
SELECT emp_id, emp_name, dept, salary,
       ROW_NUMBER() OVER (PARTITION BY dept ORDER BY salary DESC) AS rn
FROM employee;
```

**Output:**

| emp\_id | emp\_name | dept | salary | rn |
| ------- | --------- | ---- | ------ | -- |
| 3       | Carol     | HR   | 5500   | 1  |
| 1       | Alice     | HR   | 5000   | 2  |
| 4       | Dave      | IT   | 7000   | 1  |
| 2       | Bob       | IT   | 6000   | 2  |
| 5       | Eve       | IT   | 6000   | 3  |

---

### Key Points:

* `ROW_NUMBER()` → gives a unique number **per row in the partition**
* `RANK()` → gives the same rank to ties, but can skip numbers
* `DENSE_RANK()` → gives the same rank to ties, no skipping

---

# Questions:

We’ll use this **employee table** for examples:

| emp\_id | emp\_name | dept | salary |
| ------- | --------- | ---- | ------ |
| 1       | Alice     | HR   | 5000   |
| 2       | Bob       | IT   | 6000   |
| 3       | Carol     | HR   | 5500   |
| 4       | Dave      | IT   | 7000   |
| 5       | Eve       | IT   | 6000   |

## 🔹 Exercise 1: ROW\_NUMBER()

**Question:**
Assign a row number to each employee **within their department**, ordered by **salary descending**.

* Expected output (partial view for HR):

| emp\_name | dept | salary | rn |
| --------- | ---- | ------ | -- |
| Carol     | HR   | 5500   | 1  |
| Alice     | HR   | 5000   | 2  |

### Ans:

```sql
SELECT emp_name, dept, salary, 
       ROW_NUMBER() OVER(PARTITION BY dept ORDER BY salary DESC) AS num
FROM employee;
```

- ROW_NUMBER() always gives a unique number to each row within the partition.
- Ties are not given the same number — it still increments uniquely.
- PARTITION BY works like GROUP BY but doesn’t collapse rows.

## 🔹 Exercise 2: RANK()

**Question:**
Assign a rank to each employee **within their department**, ordered by **salary descending**, using `RANK()`.

* Expected output for IT department:

| emp\_name | dept | salary | rank |
| --------- | ---- | ------ | ---- |
| Dave      | IT   | 7000   | 1    |
| Bob       | IT   | 6000   | 2    |
| Eve       | IT   | 6000   | 2    |

Notice how **Bob and Eve have the same rank** because their salary is tied, but the next rank would skip to 4.

### Sol:

```sql
SELECT emp_name, dept, salary, 
       RANK() OVER (PARTITION BY dept ORDER BY salary DESC) AS rank
FROM employee;
```

### 🔹 Output

| emp\_name | dept | salary | rank |
| --------- | ---- | ------ | ---- |
| Carol     | HR   | 5500   | 1    |
| Alice     | HR   | 5000   | 2    |
| Dave      | IT   | 7000   | 1    |
| Bob       | IT   | 6000   | 2    |
| Eve       | IT   | 6000   | 2    |

* `RANK()` assigns **the same rank to ties**.
* It **skips numbers after ties** (e.g., rank 2 appears twice, next would be rank 4).
* Unlike `ROW_NUMBER()`, the numbering is **not unique** when there’s a tie.

## 🔹 Exercise 3: DENSE\_RANK()

**Question:**
Assign a dense rank to each employee **within their department**, ordered by **salary descending**, using `DENSE_RANK()`.

* Expected output for IT department:

| emp\_name | dept | salary | dense\_rank |
| --------- | ---- | ------ | ----------- |
| Dave      | IT   | 7000   | 1           |
| Bob       | IT   | 6000   | 2           |
| Eve       | IT   | 6000   | 2           |

Notice: **No numbers are skipped** after ties, unlike `RANK()`.

### Sol:

```sql
SELECT emp_name, dept, salary, 
       DENSE_RANK() OVER (PARTITION BY dept ORDER BY salary DESC) AS rank
FROM employee;
```

### 🔹 Output

| emp\_name | dept | salary | rank |
| --------- | ---- | ------ | ---- |
| Carol     | HR   | 5500   | 1    |
| Alice     | HR   | 5000   | 2    |
| Dave      | IT   | 7000   | 1    |
| Bob       | IT   | 6000   | 2    |
| Eve       | IT   | 6000   | 2    |

### 🔑 Key Points

* `DENSE_RANK()` gives **same rank to ties**, just like `RANK()`.
* **Unlike `RANK()`**, it **does not skip numbers** after ties.
* Useful when you want consecutive ranking numbers despite ties.

## 🔹 Exercise 4: LEAD()

**Question:**
For each employee, find the **salary of the next higher-paid employee within the same department**, ordered by salary descending.

Expected output for HR:

| emp\_name | dept | salary | next\_salary |
| --------- | ---- | ------ | ------------ |
| Carol     | HR   | 5500   | 5000         |
| Alice     | HR   | 5000   | NULL         |

### Sol:

`LEAD()` **needs the column you want to look at** inside the parentheses.

```sql
SELECT emp_name, dept, salary, 
       LEAD(salary) OVER(PARTITION BY dept ORDER BY salary DESC) AS next_salary
FROM employee;
```

### 🔹 Output

| emp\_name | dept | salary | next\_salary |
| --------- | ---- | ------ | ------------ |
| Carol     | HR   | 5500   | 5000         |
| Alice     | HR   | 5000   | NULL         |
| Dave      | IT   | 7000   | 6000         |
| Bob       | IT   | 6000   | 6000         |
| Eve       | IT   | 6000   | NULL         |

### 🔑 Key Points:

* `LEAD(column)` → looks **forward** to the next row in the window.
* `PARTITION BY dept` → ensures the function resets for each department.
* `ORDER BY salary DESC` → defines the order of the rows for LEAD.
* Returns **NULL** if there’s no “next” row.

## 🔹 Exercise 5: LAG()

**Question:**
For each employee, find the **salary of the previous higher-paid employee within the same department**, ordered by salary descending.

Expected output for HR:

| emp\_name | dept | salary | prev\_salary |
| --------- | ---- | ------ | ------------ |
| Carol     | HR   | 5500   | NULL         |
| Alice     | HR   | 5000   | 5500         |

### Sol:

```sql
SELECT emp_name, dept, salary, 
       LAG(salary) OVER(PARTITION BY dept ORDER BY salary DESC) AS prev_salary
FROM employee;
```

### 🔹 Output

| emp\_name | dept | salary | prev\_salary |
| --------- | ---- | ------ | ------------ |
| Carol     | HR   | 5500   | NULL         |
| Alice     | HR   | 5000   | 5500         |
| Dave      | IT   | 7000   | NULL         |
| Bob       | IT   | 6000   | 7000         |
| Eve       | IT   | 6000   | 7000         |

### 🔑 Key Points:

* `LAG(column)` → looks **backward** to the previous row in the window.
* `PARTITION BY dept` → resets the calculation for each department.
* `ORDER BY salary DESC` → defines the row order.
* Returns **NULL** if there’s no previous row.

## 🔹 Exercise 6 – Top earners per department

Write a query to show **the top 2 earners in each department**, along with:

* Their rank (`RANK()`),
* Their previous salary (`LAG(salary)`),
* Their next salary (`LEAD(salary)`),

**Expected output for IT:**

| emp\_name | salary | rank | prev\_salary | next\_salary |
| --------- | ------ | ---- | ------------ | ------------ |
| Dave      | 7000   | 1    | NULL         | 6000         |
| Bob       | 6000   | 2    | 7000         | 6000         |
| Eve       | 6000   | 2    | 7000         | NULL         |

### Sol:

```sql
SELECT emp_name, salary,
       RANK() OVER(PARTITION BY dept ORDER BY salary DESC) AS rank,
       LAG(salary) OVER(PARTITION BY dept ORDER BY salary DESC) AS prev_salary,
       LEAD(salary) OVER(PARTITION BY dept ORDER BY salary DESC) AS next_salary
FROM employee
WHERE RANK() OVER(PARTITION BY dept ORDER BY salary DESC) <= 2;
```

## 🔹 Exercise 7 – Consecutive salary differences

Write a query to show, for each employee:

* Salary,
* Previous salary (`LAG`),
* Difference with previous salary,
* Difference with next salary (`LEAD`),

### Sol:

```sql
SELECT emp_name, salary,
       LAG(salary) OVER(PARTITION BY dept ORDER BY salary DESC) AS prev_salary,
       salary - LAG(salary) OVER(PARTITION BY dept ORDER BY salary DESC) AS prev_salary_diff,
       LEAD(salary) OVER(PARTITION BY dept ORDER BY salary DESC) - salary AS next_salary_diff
FROM employee;
```




