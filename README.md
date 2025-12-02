## **Order of SQL Keywords (Query Execution Order)**

### 1️⃣ **Logical Execution Order** (How DB *processes* the query — **interview important**)

### 2️⃣ **Syntax Order** (How *you write* it — useful for fluency & practice)

---

### 🔍 1. Logical Execution Order (How SQL Engine Executes It)

| Step | Clause         | What It Does                       |
| ---- | -------------- | ---------------------------------- |
| 1️⃣  | `FROM`         | Tables & joins                     |
| 2️⃣  | `WHERE`        | Row-level filtering (before group) |
| 3️⃣  | `GROUP BY`     | Group rows                         |
| 4️⃣  | `HAVING`       | Filter on grouped data             |
| 5️⃣  | `SELECT`       | Choose columns                     |
| 6️⃣  | `ORDER BY`     | Sort the result                    |
| 7️⃣  | `LIMIT/OFFSET` | Paginate or truncate results       |

---

### 🔧 2. Syntax Order (How You Write It)

```sql
SELECT column1, column2, ...
FROM table_name
[JOIN other_table ON condition]
WHERE condition
GROUP BY column
HAVING condition
ORDER BY column [ASC|DESC]
LIMIT number OFFSET number;
```

---

In SQL, commands are divided into categories based on what they do.
Two very important categories are **DDL** and **DML**.

## **DDL – Data Definition Language**

These commands are used to **define or modify the structure of the database and its objects** (tables, schemas, indexes, etc.).

### 🔹 What DDL does

* Creates database objects
* Modifies structure of objects
* Deletes objects

### 🔹 Common DDL Commands

| Command    | Purpose                                                  |
| ---------- | -------------------------------------------------------- |
| `CREATE`   | Creates new database objects (table, database, view…)    |
| `ALTER`    | Modifies existing objects (add column, modify datatype…) |
| `DROP`     | Deletes database objects                                 |
| `TRUNCATE` | Removes all rows from a table (faster than DELETE)       |
| `RENAME`   | Renames a table or other object                          |

> ⚠ DDL commands are **auto-committed** → changes cannot be rolled back.

## ✅ **DML – Data Manipulation Language**

These commands are used to **manipulate the data stored inside database tables**.

### 🔹 What DML does

* Insert data
* Update existing data
* Delete data
* Read data (in ANSI SQL, SELECT is considered DQL, but many consider it under DML in interviews)

### 🔹 Common DML Commands

| Command  | Purpose                                              |
| -------- | ---------------------------------------------------- |
| `INSERT` | Adds new rows/data                                   |
| `UPDATE` | Modifies existing data                               |
| `DELETE` | Removes data row-wise                                |
| `MERGE`  | Inserts or updates depending on condition (“upsert”) |

> 🔁 DML commands **are not auto-committed** → can be rolled back.

## 📝 Summary

| Category | Full Form                  | Works On           | Auto Commit | Examples                      |
| -------- | -------------------------- | ------------------ | ----------- | ----------------------------- |
| **DDL**  | Data Definition Language   | Structure / schema | Yes         | CREATE, ALTER, DROP, TRUNCATE |
| **DML**  | Data Manipulation Language | Data inside tables | No          | INSERT, UPDATE, DELETE, MERGE |

## Other SQL Categories

| Category | Full Form                    | Examples                    |
| -------- | ---------------------------- | --------------------------- |
| **DQL**  | Data Query Language          | SELECT                      |
| **TCL**  | Transaction Control Language | COMMIT, ROLLBACK, SAVEPOINT |
| **DCL**  | Data Control Language        | GRANT, REVOKE               |

**“Is SQL = DML?”**
→ No. SQL is a language that includes multiple categories (DDL, DML, DQL, TCL, DCL).
DML is only one part of SQL.

---

## **TRUNCATE vs DELETE**

| Feature              | **DELETE**                             | **TRUNCATE**                      |
| -------------------- | -------------------------------------- | --------------------------------- |
| Type                 | **DML** (Data manipulation)            | **DDL** (Schema modification)     |
| Removes              | Selected rows (with WHERE) or all rows | **All rows only**                 |
| WHERE allowed?       | ✔ Yes                                  | ❌ No                              |
| Speed                | Slower (row by row)                    | Very fast                         |
| Auto-commit          | ❌ Can rollback if transaction used     | ✔ Auto-commit → cannot rollback   |
| Auto Increment Reset | ❌ No (continues from last value)       | ✔ Yes (resets to 1)               |
| Triggers             | ✔ `BEFORE/AFTER DELETE` triggers fire  | ❌ DELETE triggers **do NOT fire** |
| Disk space released  | ❌ No                                   | ✔ Yes (table storage freed)       |
| Locks                | Row-level locking                      | Table-level locking               |

### 🔑 Why DELETE is slower

`DELETE` removes rows **one by one** and logs each deletion in the transaction log.

### 🔑 Why TRUNCATE is faster

`TRUNCATE` removes data by **deallocating all storage pages at once** — it does not log each row.

### ⚠️ RULE OF THUMB (Interviews love this)

| Use          | When                                                                           |
| ------------ | ------------------------------------------------------------------------------ |
| **DELETE**   | You want to remove **specific rows** or maintain **transaction safety**        |
| **TRUNCATE** | You want to **quickly remove all data** and **reset the table to empty state** |

### Quick Example

```sql
DELETE FROM employees WHERE department = 'HR';
-- removes only HR employees
```

```sql
TRUNCATE TABLE employees;
-- removes ALL employees and resets AUTO_INCREMENT
```

---

