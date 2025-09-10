## 1️⃣ What is a CTE?

* A **CTE** is a temporary named result set that you can reference **within a single SQL statement**.
* It makes complex queries **more readable** and **easier to maintain**.
* Syntax:

```sql
WITH cte_name (column1, column2, ...) AS (
    -- your query here
)
SELECT *
FROM cte_name
WHERE ...;
```

### Example Table: Employees

| emp\_id | name  | manager\_id |
| ------- | ----- | ----------- |
| 1       | Alice | NULL        |
| 2       | Bob   | 1           |
| 3       | Carol | 1           |
| 4       | David | 2           |
| 5       | Emma  | 2           |
| 6       | Frank | 3           |

### Simple CTE Example

**Goal:** List employees whose manager is Alice (emp\_id = 1).

```sql
WITH Alice_team AS (
    SELECT *
    FROM Employees
    WHERE manager_id = 1
)
SELECT *
FROM Alice_team;
```

**Output:**

| emp\_id | name  | manager\_id |
| ------- | ----- | ----------- |
| 2       | Bob   | 1           |
| 3       | Carol | 1           |

### Key Benefits:

1. Break down complex queries into **readable parts**.
2. Can be **referenced multiple times** within the same query.
3. Works well with **recursive queries** (e.g., hierarchical reporting).

---

### **Recursive CTE**

* Useful for **hierarchical data** (employees → managers → top-level).
* Syntax adds `UNION ALL` to iterate through levels.

### **Question:** Using the same `Employees` table, write a query to **find all subordinates under Alice** (direct and indirect).

#### Explanation:


