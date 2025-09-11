## 🔹 1. What is an Index?

* An **index** is like the index of a book.
* Instead of scanning every page (table row), the database uses the index to quickly locate the rows it needs.
* Internally, most databases use a **B-Tree** structure for indexes.

👉 Without index → **full table scan** (slow).
👉 With index → **index seek** (fast).

## 🔹 2. Types of Indexes

- ### Clustered Index

* Defines the **physical order** of data in the table.
* A table can have **only one clustered index** (because rows can be stored only in one order).
* Example: A table of Employees with `PRIMARY KEY (emp_id)` → that’s usually the clustered index.

👉 Data is stored in the order of `emp_id`.

- ### ✅ Non-Clustered Index

* A separate structure that points to the data (like a lookup).
* A table can have **many non-clustered indexes**.
* Useful for speeding up queries on non-primary key columns.

👉 Think of it as a “phone book” with names → pointing to page numbers.

- ### ✅ Covering Index

* A non-clustered index that **includes all the columns** required by the query.
* So the database doesn’t even need to go back to the base table.

Example:

```sql
CREATE INDEX idx_orders_customer_amount 
ON Orders(customer_id, amount);
```

If you run:

```sql
SELECT customer_id, amount FROM Orders WHERE customer_id = 101;
```

👉 The query is fully answered from the index (faster).

## 3. When Indexes Help vs Hurt

✅ **Indexes improve performance for:**

* `WHERE` conditions
* `JOIN`s
* `ORDER BY` and `GROUP BY`

❌ **Indexes hurt performance for:**

* `INSERT`, `UPDATE`, `DELETE` → because the index itself must also be updated.
* Too many indexes = slow writes.

## 4. Index Traps

* **Q: Can a table have multiple clustered indexes?**
  ❌ No, only one (data can be ordered in only one way).
* **Q: Do indexes always speed up queries?**
  ❌ No, if the table is small, full scan is sometimes faster.
* **Q: What’s the trade-off of having too many indexes?**
  👉 Fast reads but slow writes.

---

# Let's understand how exactly it works

### 1. Without Index → Full Table Scan

Suppose you have **1 million rows** in `Orders`:

```sql
SELECT * FROM Orders WHERE customer_id = 101;
```

👉 Without index:

* The database checks **every single row** in the table (`customer_id = ?`).
* That’s **1 million comparisons**.

This is called a **full table scan**.
Good if the table is tiny, but horrible if the table is huge.

### 2. With Index → Fast Lookup

Now imagine you create an index on `customer_id`:

```sql
CREATE INDEX idx_customer ON Orders(customer_id);
```

👉 What happens internally:

* The database builds a **B-Tree** (balanced tree) structure for `customer_id`.
* All customer IDs are sorted, with pointers to the actual rows in the table.

So instead of scanning 1 million rows, the DB can do a **binary search** in the index.

#### How it works:

1. Database looks at the index (which is much smaller than the full table).
2. It quickly finds `customer_id = 101` using tree search (logarithmic time).
3. The index stores **row pointers** → direct links to where the actual rows are in the table.
4. It fetches those rows directly.

👉 Instead of **1 million comparisons**, maybe just **20 tree steps** + a few row fetches. 🚀

### 3. Does Index Scan Itself?

Yes — but that’s **the whole point**:

* Scanning a B-Tree index is **way faster** than scanning a raw table.
* Because the index is sorted and optimized for searching.

So the cost is:

* Scan index (tiny, fast).
* Jump to exact rows in the table (direct pointers, not scanning).

### 4. Example: Book Analogy

Imagine a book with 1,000 pages.
You want to find the word “Index.”

* **Without index** → read all 1,000 pages.
* **With index** → go to the index at the back → see “Index → page 765” → jump straight there.

Yes, you still had to scan the **index pages**, but that’s a **tiny scan** compared to the whole book.

### 5. Covering Index (Even Faster)

Sometimes the index **already contains all the columns** you need.
Then the database doesn’t even go to the table — it answers directly from the index.

Example:

```sql
CREATE INDEX idx_customer_amount ON Orders(customer_id, amount);
```

Query:

```sql
SELECT amount FROM Orders WHERE customer_id = 101;
```

👉 No table lookup needed, because `customer_id` and `amount` are already in the index.

This is called a **covering index**.

---

So the real purpose of an index:

* **Avoid scanning the whole table**.
* Use a smaller, sorted structure (B-Tree) to jump directly to the needed rows.

