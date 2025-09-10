## Consider the tables:

**Employees**

| emp\_id | name  | dept\_id | salary |
| ------- | ----- | -------- | ------ |
| 1       | Alice | 10       | 60000  |
| 2       | Bob   | 20       | 50000  |
| 3       | Carol | 10       | 75000  |
| 4       | Dave  | 30       | 40000  |
| 5       | Eve   | 20       | 65000  |

**Departments**

| dept\_id | dept\_name |
| -------- | ---------- |
| 10       | HR         |
| 20       | IT         |
| 30       | Marketing  |

--- 

### **Question:** Find **departments** that have at least one employee with a salary above 70000, using `EXISTS`.

💡 Hint:

* `EXISTS` checks if a subquery returns at least one row.
* Outer query: from **Departments**.
* Inner query: checks if that department has any employee with salary > 70000.


#### Explanation:

```sql
select d.dept_name from Department d where exists (select 1 from Employees e where e.dept_id=d.dept_id and e.salary>70000);
```

Let’s validate with our sample data:

**Employees**

* Alice (60000, HR)
* Bob (50000, IT)
* Carol (75000, HR)
* Dave (40000, Marketing)
* Eve (65000, IT)

**Departments**

* HR
* IT
* Marketing

✅ `HR` → Carol has 75000 → condition true → included
❌ `IT` → highest salary 65000 (not > 70000) → excluded
❌ `Marketing` → highest salary 40000 → excluded

**Final Result:**

| dept\_name |
| ---------- |
| HR         |

---

### **Question:** Find employees whose salary is **greater than the salary of ANY employee in the IT department**.

💡 Key points:

* `> ANY` means **greater than at least one value** from the subquery.
* So if IT salaries are `{50000, 65000}`, then:

  * `> ANY` means salary > 50000 **OR** salary > 65000 (i.e., greater than the minimum).
  * Effectively, `> ANY` = salary > **MIN(salary in IT)**.

---

#### Explanation:

```sql
SELECT name, salary
FROM Employees
WHERE salary > ANY (
    SELECT salary
    FROM Employees e
    JOIN Departments d ON e.dept_id = d.dept_id
    WHERE d.dept_name = 'IT'
);
```

Let’s test with our sample data:

**IT dept salaries** = {50000 (Bob), 65000 (Eve)}

* `> ANY` → salary > **at least one of them** → salary > 50000.

So effectively this query finds everyone earning more than 50k.

**Check each employee:**

* Alice → 60000 ✅
* Bob → 50000 ❌ (not greater)
* Carol → 75000 ✅
* Dave → 40000 ❌
* Eve → 65000 ✅

**Result:**

| name  |
| ----- |
| Alice |
| Carol |
| Eve   |

---

### **Question:** Can you try writing the same query but with `> ALL` instead of `> ANY`?

#### Explanation:

```sql
SELECT name, salary
FROM Employees
WHERE salary > ALL (
    SELECT salary
    FROM Employees e
    JOIN Departments d ON e.dept_id = d.dept_id
    WHERE d.dept_name = 'IT'
);
```

