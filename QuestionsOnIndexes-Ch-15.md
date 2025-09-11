## **Question 1:** Clustered index is only for primary keys?

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

## **Question 2: Conceptual**

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

## **Question 3: True/False**

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

## **Question 4:** 
