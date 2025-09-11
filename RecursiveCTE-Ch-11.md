## 🔹 What is a Recursive CTE?

It has **two parts**:

1. **Anchor member** → the starting point (base query).
2. **Recursive member** → repeatedly runs and references the CTE itself, until no more rows are returned.

**Syntax:**

```sql
WITH RECURSIVE cte_name AS (
    -- Anchor member
    SELECT ...
    UNION ALL
    -- Recursive member
    SELECT ...
    FROM cte_name
    JOIN ...
)
SELECT * FROM cte_name;
```

---

## 🔹 Example: Employee Hierarchy

### **Employees Table**

| emp\_id | emp\_name | manager\_id |
| ------- | --------- | ----------- |
| 1       | Alice     | NULL        |
| 2       | Bob       | 1           |
| 3       | Carol     | 1           |
| 4       | David     | 2           |
| 5       | Eva       | 2           |
| 6       | Frank     | 3           |

Alice is the CEO (no manager). Bob & Carol report to Alice. David & Eva report to Bob. Frank reports to Carol.

### Recursive CTE to find hierarchy under Alice

```sql
WITH RECURSIVE EmployeeHierarchy AS (
    -- Anchor: start with Alice
    SELECT emp_id, emp_name, manager_id, 1 AS level
    FROM Employees
    WHERE emp_name = 'Alice'
    
    UNION ALL
    
    -- Recursive: find direct reports of previous level
    SELECT e.emp_id, e.emp_name, e.manager_id, eh.level + 1
    FROM Employees e
    INNER JOIN EmployeeHierarchy eh
      ON e.manager_id = eh.emp_id
)
SELECT * FROM EmployeeHierarchy;
```

### 🔹 Output

| emp\_id | emp\_name | manager\_id | level |
| ------- | --------- | ----------- | ----- |
| 1       | Alice     | NULL        | 1     |
| 2       | Bob       | 1           | 2     |
| 3       | Carol     | 1           | 2     |
| 4       | David     | 2           | 3     |
| 5       | Eva       | 2           | 3     |
| 6       | Frank     | 3           | 3     |

So we got the **entire hierarchy tree starting from Alice** 🎉.

It works like this:

#### **Anchor query runs once**

* Fetches Alice (level = 1).
* That’s the *starting dataset*.
* Think of it as “seed rows.”

Result after step 1:

```
Alice (level 1)
```

#### **Recursive query runs**

* It looks at the result from the *previous step* (`EmployeeHierarchy`) and finds rows in `Employees` where `manager_id = emp_id of those results`.
* For Alice → finds Bob, Carol (level 2).

Now the result set contains:

```
Alice (level 1)
Bob (level 2)
Carol (level 2)
```

#### **Recursive query runs again**

* Now `EmployeeHierarchy` has Alice, Bob, Carol.
* The recursive part checks:

  * Who reports to Bob? → David, Eva.
  * Who reports to Carol? → Frank.

New rows added:

```
David (level 3)
Eva   (level 3)
Frank (level 3)
```

#### **Runs again**

* Now recursion checks David, Eva, Frank.
* None of them have further subordinates.
* Recursive query returns **no new rows**.

#### **Stops automatically**

* Since the recursive query produced **0 rows**, recursion ends.
* Final result = everything collected so far.

So **Alice is fetched only once** (from the anchor).
After that, each level is discovered step by step, until no more children are found.

