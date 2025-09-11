# **Question 1:** Clustered index is only for primary keys?

### Explanation:

Not necessarily — but in practice, **it usually is**. Let me clarify carefully.

#### **1️⃣ What a clustered index really is**

* A **clustered index** defines the **physical order of rows in a table**.
* **Only one clustered index per table** (because rows can be stored in only one order).
* It **does not have to be the primary key**, but primary keys **often make the natural choice** for clustered indexes because:

  * They are unique
  * Frequently queried
  * Good for range queries

#### **2️⃣ Clustered index on a non-primary key**

* You **can** create a clustered index on a non-primary column if your DB allows it.
* Example (SQL Server):

```sql
CREATE CLUSTERED INDEX idx_order_date ON Orders(order_date);
```

* Now rows are physically ordered by `order_date` instead of `order_id`.
* But you can’t also make `order_id` clustered at the same time.

#### **3️⃣ Key Points**

| Feature             | Clustered Index | Primary Key             |
| ------------------- | --------------- | ----------------------- |
| Physical row order  | Yes             | No (logical constraint) |
| Uniqueness enforced | Optional        | Yes                     |
| Only one per table  | Yes             | N/A                     |
| Typical usage       | Often PK        | Always PK               |

So: **primary key → often clustered**, but clustered index **can exist on any column** (unique or not).

# **Question 2: Conceptual**

You have a table `Orders`:

| order\_id | customer\_id | order\_date | amount |
| --------- | ------------ | ----------- | ------ |

You frequently run these queries:

1. `SELECT * FROM Orders WHERE order_id = 1001;`
2. `SELECT * FROM Orders WHERE customer_id = 101;`
3. `SELECT SUM(amount) FROM Orders WHERE customer_id = 101;`

**Question:**

* Which columns would you index?
* Which type of index would you choose for each query?

### Explanation:

1. Query: `SELECT * FROM Orders WHERE order_id = 1001;`

* index on `order_id`
* **clustered index** makes sense here because `order_id` is usually the primary key.

2. Query: `SELECT * FROM Orders WHERE customer_id = 101;`

* **non-clustered index** on `customer_id`.
* This allows fast lookup by customer without changing the physical table order.

3. Query: `SELECT SUM(amount) FROM Orders WHERE customer_id = 101;`

* index on `customer_id`
* Optional improvement: **covering index** on `(customer_id, amount)`

#### Index Plan

| Query                    | Index Column(s)        | Type of Index            |
| ------------------------ | ---------------------- | ------------------------ |
| `WHERE order_id=1001`    | order\_id              | Clustered (primary key)  |
| `WHERE customer_id=101`  | customer\_id           | Non-clustered            |
| `SELECT SUM(amount) ...` | (customer\_id, amount) | Covering (non-clustered) |

---

# **Question 3: True/False**

For each statement, answer True or False:

1. A table can have multiple clustered indexes.
2. Non-clustered indexes store the actual rows of the table.
3. Covering indexes can make queries faster by avoiding table lookups.
4. Clustered indexes are always faster than non-clustered indexes for all queries.
   
### Explanation:

| Statement                                                                         | Answer     | Correct? | Explanation                                                                                             |
| --------------------------------------------------------------------------------- | --------------- | -------- | ------------------------------------------------------------------------------------------------------- |
| 1. A table can have multiple clustered indexes                                    | No              | ✅        | Only one clustered index per table; rows can only be physically ordered one way.                        |
| 2. Non-clustered indexes store the actual rows of the table                       | No              | ✅        | Non-clustered indexes store keys + pointers to rows, not the rows themselves.                           |
| 3. Covering indexes can make queries faster by avoiding table lookups             | Yes             | ✅        | If the query only needs columns in the index, the DB can answer from the index alone.                   |
| 4. Clustered indexes are always faster than non-clustered indexes for all queries | Not necessarily | ✅        | Clustered indexes are fast for range queries and primary key lookups, but not always for other queries. |

---

# **Question 4:** Write SQL statements to:

1. Create a **clustered index** on `order_id` in the `Orders` table.
2. Create a **non-clustered index** on `customer_id` in the `Orders` table.
3. Create a **covering index** on `(customer_id, amount)` in the `Orders` table.

| order\_id | customer\_id | order\_date | amount |
| --------- | ------------ | ----------- | ------ |
| 1001      | 101          | 2025-01-01  | 500    |
| 1002      | 102          | 2025-01-02  | 300    |
| 1003      | 101          | 2025-01-03  | 200    |
| 1004      | 103          | 2025-01-03  | 400    |
| 1005      | 101          | 2025-01-04  | 600    |

### Explanation:

1. **Clustered index on `order_id`**

```sql
CREATE CLUSTERED INDEX ci1 ON Orders(order_id);
```

2. **Non-clustered index on `customer_id`**

```sql
CREATE NONCLUSTERED INDEX ci2 ON Orders(customer_id);
```

3. **Covering index on `(customer_id, amount)`**

```sql
CREATE NONCLUSTERED INDEX ci3 ON Orders(customer_id) INCLUDE (amount);
```

👉 Why?

* `(customer_id)` → index key (used for lookups)
* `INCLUDE (amount)` → makes this a **covering index**, so queries needing `SUM(amount)` for a customer don’t need to hit the table at all.

Version `CREATE INDEX ci3 ON Orders(customer_id, amount)` would still create a multi-column index, but not necessarily a **covering index** in the strict sense.

So the big difference:
- customer_id, amount in key → both used for filtering/sorting
- customer_id key + INCLUDE(amount) → customer_id used for filtering, amount just stored to cover query
  
---

# Composite VS Covering index

### **Case 1: Composite index**

```sql
CREATE NONCLUSTERED INDEX idx1 ON Orders(customer_id, amount);
```

* This means both `customer_id` and `amount` are part of the **index key**.
* The index is sorted first by `customer_id`, then (inside each customer) by `amount`.
* So it can be used for queries like:

  ```sql
  SELECT * FROM Orders WHERE customer_id = 101;
  SELECT * FROM Orders WHERE customer_id = 101 AND amount = 500;
  SELECT * FROM Orders ORDER BY customer_id, amount;
  ```
* ✅ Great for queries filtering **by both customer and amount**.
* ❌ But if your query only needs to *sum* `amount`, the DB may still read many index entries unnecessarily.

### **Case 2: Covering index**

```sql
CREATE NONCLUSTERED INDEX idx2 ON Orders(customer_id) INCLUDE (amount);
```

* Here, **only `customer_id`** is the index key (sorted).
* `amount` is **stored in the index leaf pages** but **not part of the sort order**.
* This is very efficient for queries like:

  ```sql
  SELECT SUM(amount) 
  FROM Orders 
  WHERE customer_id = 101;
  ```

  * The DB finds rows by `customer_id` using the index.
  * Since `amount` is included, it doesn’t need to go back to the table → **no extra lookup**.

### 🔑 Key Difference

* **Composite index (customer\_id, amount)** → sorted by both columns, useful for filtering/sorting on both.
* **Covering index (customer\_id INCLUDE amount)** → sorted only by `customer_id`, but “covers” the query because `amount` is available in the index → avoids table lookups.

✅ Think of **INCLUDE** as saying:
*"I don’t want this column for filtering or sorting, but please keep it in the index so I don’t have to hit the table later."*

---

## Let’s walk through what happens inside the DB engine with and without a **covering index**.

We’ll use this query:

```sql
SELECT SUM(amount)
FROM Orders
WHERE customer_id = 101;
```

### Case 1: No Index

* The DB has no index on `customer_id`.
* Execution plan: **Full Table Scan**

  * Reads every row in `Orders`
  * Checks if `customer_id = 101`
  * Adds up the amounts.
* 🔴 Very slow if table = millions of rows.

### Case 2: Composite Index `(customer_id, amount)`

```sql
CREATE NONCLUSTERED INDEX idx1 ON Orders(customer_id, amount);
```

* Execution plan:

  1. DB seeks directly to all rows with `customer_id = 101` (fast).
  2. Since `amount` is part of the index key, the index entries already contain it.
  3. DB sums the amounts **without going back to the table**.
* ✅ Efficient, because both filter column (`customer_id`) and aggregation column (`amount`) are inside the index.
* ⚠️ But this index is sorted by both columns, so maintaining it on inserts/updates is a bit heavier.

### Case 3: Covering Index `(customer_id) INCLUDE (amount)`

```sql
CREATE NONCLUSTERED INDEX idx2 ON Orders(customer_id) INCLUDE (amount);
```

* Execution plan:

  1. DB seeks on `customer_id = 101` (fast).
  2. `amount` is stored in the leaf nodes (not sorted by it, but available).
  3. DB reads all `amount` values for that customer directly from the index.
* ✅ Even more lightweight than composite index, because the sort order is **only on `customer_id`**.
* ✅ Still avoids going back to the base table.

#### ⚖️ Comparison

| Query                                | Composite Index `(customer_id, amount)` | Covering Index `(customer_id) INCLUDE (amount)` |
| ------------------------------------ | --------------------------------------- | ----------------------------------------------- |
| Lookup by `customer_id` only         | ✅ Works                                 | ✅ Works                                         |
| Lookup by `customer_id` AND `amount` | ✅ Very efficient (sorted by both)       | ❌ Less efficient (not sorted by amount)         |
| SUM(amount) by customer              | ✅ Works (amount in index key)           | ✅ Works (amount in INCLUDE)                     |
| Maintenance (INSERT/UPDATE cost)     | Higher (2-column sort)                  | Lower (1-column sort, extra column just stored) |

👉 So the **choice depends on workload**:

* If you often filter by both `customer_id` AND `amount`, go composite.
* If you mostly filter by `customer_id` and just need `amount` for aggregation, go covering.

<img width="1536" height="1024" alt="image" src="https://github.com/user-attachments/assets/8001e733-4be6-46d8-8e98-91364009e65f" />

---

# **Question 4: Scenario**

Your table has **1 million rows**. You notice that this query is **very slow**:

```sql
SELECT * 
FROM Orders 
WHERE order_date = '2025-01-01';
```

**Question:**

* How would you improve performance using indexes?
* Would you choose clustered, non-clustered, or covering index? Why?

### Explanation:

#### Why **non-clustered index** on `order_date`

* Query is filtering by `order_date`.
* Without an index → full table scan (1M rows checked).
* With **non-clustered index** on `order_date`:

  * DB engine can jump directly to the entries where `order_date = '2025-01-01'`.
  * Then it fetches only those rows from the table.

#### ❓ Why not clustered index?

* You *could* make `order_date` the clustered index, but:

  * Typically, `order_id` (the PK) is the clustered index.
  * You can’t have two clustered indexes.
  * If you switch it to `order_date`, inserts might get expensive (since new rows won’t always come in date order).

#### ❓ Covering index?

* If your query was:

  ```sql
  SELECT order_id, amount 
  FROM Orders 
  WHERE order_date = '2025-01-01';
  ```

  then you might use:

  ```sql
  CREATE NONCLUSTERED INDEX idx_orderdate ON Orders(order_date) INCLUDE (order_id, amount);
  ```

  * That way, the DB doesn’t need to touch the base table at all.

---

# **Question 5: Mixed Index Scenario**

You have this `Orders` table with **1 million rows**:

| order\_id (PK) | customer\_id | order\_date | amount |
| -------------- | ------------ | ----------- | ------ |

The following queries are common in the app:

1.

```sql
SELECT * 
FROM Orders 
WHERE order_id = 12345;
```

2.

```sql
SELECT order_id, amount 
FROM Orders 
WHERE customer_id = 101;
```

3.

```sql
SELECT SUM(amount) 
FROM Orders 
WHERE customer_id = 101 
AND order_date BETWEEN '2025-01-01' AND '2025-01-31';
```

**Question:**

* Which indexes would you create to optimize all three queries?
* Would you use clustered, non-clustered, or covering indexes (or a mix)?

### Explanation:

1. **Query 1**

```sql
SELECT * 
FROM Orders 
WHERE order_id = 12345;
```

* Best index: **Clustered index on `order_id`** (since `order_id` is usually the PK).

```sql
CREATE CLUSTERED INDEX ci1 ON Orders(order_id);
```

2. **Query 2**

```sql
SELECT order_id, amount 
FROM Orders 
WHERE customer_id = 101;
```

```sql
CREATE NONCLUSTERED INDEX ci2 
ON Orders(customer_id) 
INCLUDE (order_id, amount);
```

* This way the DB can satisfy the query *entirely from the index* → no table lookup.

 3. **Query 3**

```sql
SELECT SUM(amount) 
FROM Orders 
WHERE customer_id = 101 
AND order_date BETWEEN '2025-01-01' AND '2025-01-31';
```

* Best index: **non-clustered composite index** on `(customer_id, order_date)` and include `amount`.
* Why?

  * Customer filter → index seek
  * Date range → ordered traversal
  * Amount included → no table lookup

```sql
CREATE NONCLUSTERED INDEX ci3 
ON Orders(customer_id, order_date) 
INCLUDE (amount);
```

---

# **Question 6: Trick Scenario**

You have a `Logs` table with **50 million rows**:

| log\_id (PK) | user\_id | log\_date | action\_type |
| ------------ | -------- | --------- | ------------ |

The system runs this query very often:

```sql
SELECT *
FROM Logs
WHERE action_type = 'LOGIN';
```

👉 Important details:

* There are only **3 possible values** for `action_type`: `'LOGIN'`, `'LOGOUT'`, `'PURCHASE'`.
* Distribution: `'LOGIN'` makes up **80%** of the rows.

**Question:**

* Would creating a non-clustered index on `action_type` help this query?
* Why or why not?
* What alternative strategy might be better here?







