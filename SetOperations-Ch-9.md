## Set Operations - Set operations let you combine results from multiple `SELECT` queries.

The main ones are:

1. **UNION** – combines and removes duplicates.
2. **UNION ALL** – combines and keeps duplicates.
3. **INTERSECT** – returns only rows common to both queries.
4. **EXCEPT** (or **MINUS** in Oracle) – returns rows in the first query but not in the second.

⚠️ Rules:

* Both queries must have the **same number of columns**.
* Columns must have **compatible data types**.

---

### Example Tables

**Employees\_USA**

| name  | dept\_id |
| ----- | -------- |
| Alice | 10       |
| Bob   | 20       |
| Carol | 10       |

**Employees\_India**

| name  | dept\_id |
| ----- | -------- |
| Carol | 10       |
| Dave  | 30       |
| Eve   | 20       |

---

### Question 1 (UNION vs UNION ALL)

Write queries to get the list of all employee names from both tables:

1. Without duplicates
2. With duplicates

#### Explanation:

1. Without duplicates (`UNION`)

```sql
SELECT name FROM Employees_USA
UNION
SELECT name FROM Employees_India;
```

2. With duplicates (`UNION ALL`)

```sql
SELECT name FROM Employees_USA
UNION ALL
SELECT name FROM Employees_India;
```

#### Result with our sample data:

**Employees\_USA**: Alice, Bob, Carol
**Employees\_India**: Carol, Dave, Eve

* Using **UNION** → removes duplicates → {Alice, Bob, Carol, Dave, Eve}
* Using **UNION ALL** → keeps duplicates → {Alice, Bob, Carol, Carol, Dave, Eve}

---

### Question: Can you write a query using **INTERSECT** to find employees present in **both USA and India tables**?

#### Explanation:

```sql
SELECT name FROM Employees_USA
intersect
SELECT name FROM Employees_India;
```

#### Explanation with our sample data:

**Employees\_USA** → Alice, Bob, Carol
**Employees\_India** → Carol, Dave, Eve

* `INTERSECT` → only rows present in **both tables**
* Result → **Carol**

**Output:**

| name  |
| ----- |
| Carol |

---

### Question: Write a query to find employees who are in **USA** but **not in India**.

#### Explanation:

```sql
SELECT name FROM Employees_USA
Minus
SELECT name FROM Employees_India;
```

**Note**: Just a small note depending on SQL dialect:

* **Oracle / some DBs** → use `MINUS` ✅
* **SQL Server / PostgreSQL** → use `EXCEPT` instead

#### With our sample data:

**Employees\_USA** → Alice, Bob, Carol
**Employees\_India** → Carol, Dave, Eve

* `MINUS` → rows in USA but not in India → Alice, Bob

**Result:**

| name  |
| ----- |
| Alice |
| Bob   |

---




