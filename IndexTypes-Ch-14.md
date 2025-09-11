Let's first see **visually how an index (B-Tree) works**, then cover the **different types of indexes**.

---

# 🔹 1. How a B-Tree Index Works (Step by Step)

Suppose we have a table `Orders`:

| order\_id | customer\_id | amount |
| --------- | ------------ | ------ |
| 1         | 105          | 300    |
| 2         | 101          | 500    |
| 3         | 109          | 700    |
| 4         | 101          | 250    |
| 5         | 120          | 900    |

We create an index:

```sql
CREATE INDEX idx_customer ON Orders(customer_id);
```

### (a) Full Table (unordered)

Normally, rows in a table are stored like this (unordered, scattered on disk):

```
[105] → row pointer 1
[101] → row pointer 2
[109] → row pointer 3
[101] → row pointer 4
[120] → row pointer 5
```

Searching for `customer_id = 101` → DB has to **check each row one by one**.

### (b) Index (B-Tree structure)

Index creates a **sorted tree** on `customer_id`:

```
          [105]
         /     \
     [101]     [109]
                 \
                 [120]
```

Each node stores:

* The key (`customer_id`)
* Pointers to the actual rows in the table

So in the index, `101` will point to rows (order\_id 2, order\_id 4).

### (c) Lookup

Now when we query:

```sql
SELECT * FROM Orders WHERE customer_id = 101;
```

Steps:

1. Go to the index root → check 105
   (since 101 < 105 → go left)
2. Found 101 in left branch.
3. Follow pointers → directly fetch row\_id 2 and row\_id 4 from the table.

👉 Instead of scanning **all rows**, DB did a **logarithmic search** in the index.
That’s the huge performance win.

### Analogy (book index again)

* Table = whole book
* Index = sorted back-of-book index
* Row pointers = page numbers
* Instead of flipping 1,000 pages → just look up the index.

---

# 🔹 2. Types of Indexes in SQL:

## **1. Clustered Index**

### ✅ Definition

* A **clustered index** determines the **physical order** of rows in the table.
* The table data is **sorted and stored on disk** according to the index key.
* Only **one clustered index per table** (because data can only be physically stored in one order).

### 🔹 Example Table (Clustered Index on `emp_id`)

| emp\_id | name  |
| ------- | ----- |
| 12      | Bob   |
| 33      | Carol |
| 45      | Alice |
| 50      | David |

* Rows are **physically stored** sorted by `emp_id`.

### 🔹 Insert Example (Page Splits)

* Each page can hold 4 rows. Current page:

| emp\_id | name  |
| ------- | ----- |
| 12      | Bob   |
| 33      | Carol |
| 45      | Alice |
| 50      | David |

* Insert `emp_id = 20, Eva` → Page 1 full → **page split**:

#### Page 1

| emp\_id | name |
| ------- | ---- |
| 12      | Bob  |
| 20      | Eva  |

#### Page 2

| emp\_id | name  |
| ------- | ----- |
| 33      | Carol |
| 45      | Alice |
| 50      | David |

* Rows remain **physically sorted**.
* B-Tree internal nodes updated to keep track of pages.

### 🔹 Pros

* Very fast for **range queries** (e.g., `WHERE emp_id BETWEEN 10 AND 50`).
* Good for **primary key lookups**.

### 🔹 Cons

* Slower inserts/updates/deletes in the middle of the key space (page splits happen).

## **2. Non-Clustered Index**

### ✅ Definition

* A **non-clustered index** is a **separate structure** that stores:

  * The indexed column(s) in sorted order
  * Pointers to the actual table rows

* Table rows **remain unordered**.

* You can have **many non-clustered indexes per table**.

### 🔹 Example Table (No order enforced)

| emp\_id | name  |
| ------- | ----- |
| 45      | Alice |
| 12      | Bob   |
| 33      | Carol |

Create non-clustered index:

```sql
CREATE INDEX idx_emp ON Employees(emp_id);
```

**Index Structure (B-Tree)**

```
[12] → points to row with emp_id=12
[33] → points to row with emp_id=33
[45] → points to row with emp_id=45
```

* Searching for `emp_id = 33` → DB searches the index, finds pointer → fetches the row in table.

### 🔹 Pros

* Fast lookups for columns other than the primary key.
* Multiple non-clustered indexes allowed per table.

### 🔹 Cons

* Extra storage for indexes.
* Slower inserts/updates/deletes (because indexes need maintenance).

## **3. Covering Index**

### ✅ Definition

* A **covering index** is a non-clustered index that **includes all columns required by a query**.
* The query can be answered **entirely from the index**, without looking at the table.

### 🔹 Example

Table: `Orders`

| order\_id | customer\_id | amount |
| --------- | ------------ | ------ |

Index:

```sql
CREATE INDEX idx_customer_amount ON Orders(customer_id, amount);
```

Query:

```sql
SELECT amount
FROM Orders
WHERE customer_id = 101;
```

* DB reads only the index → **no table lookup needed**.
* Faster than a normal non-clustered index where it would still fetch table rows.

### 🔹 Key Idea

* **Clustered index** → sorts the table itself.
* **Non-clustered index** → separate structure pointing to rows.
* **Covering index** → non-clustered index that already contains all needed columns → no table access needed.

# **4. Visual Summary**

| Feature         | Clustered Index               | Non-Clustered Index              | Covering Index                                  |
| --------------- | ----------------------------- | -------------------------------- | ----------------------------------------------- |
| Physical order  | Table rows sorted             | Table rows unordered             | Table rows unordered                            |
| Number allowed  | 1 per table                   | Multiple per table               | Multiple per table                              |
| Storage         | Table itself                  | Separate B-Tree structure        | Separate B-Tree structure (contains query cols) |
| Lookup          | Fast for primary key / ranges | Fast for indexed columns         | Super fast if query only uses indexed cols      |
| Inserts/Updates | Slower (page splits)          | Slightly slower (maintain index) | Slightly slower (maintain index)                |

✅ **Big Picture:**

* **Clustered index** → physical table order.
* **Non-clustered index** → separate lookup structure.
* **Covering index** → optimized non-clustered index that “covers” the query.

