### What is a CTE?

A **CTE** is a temporary result set that you can reference within a `SELECT`, `INSERT`, `UPDATE`, or `DELETE` statement.
It’s defined using the `WITH` keyword.

**Syntax:**

```sql
WITH cte_name AS (
    SELECT ...
)
SELECT * FROM cte_name;
```

Think of it like a **named subquery** that you can reuse.

---

### Example 1: Simple CTE

```sql
WITH HighValueOrders AS (
    SELECT order_id, customer_id, amount
    FROM Orders
    WHERE amount > 400
)
SELECT * FROM HighValueOrders;
```

👉 This makes the query more readable compared to writing the subquery inline.

---

### Example 2: Using CTE with Join

```sql
WITH CustomerTotals AS (
    SELECT customer_id, SUM(amount) AS total_amount
    FROM Orders
    GROUP BY customer_id
)
SELECT c.name, ct.total_amount
FROM Customers c
JOIN CustomerTotals ct
  ON c.customer_id = ct.customer_id;
```

---

## Consider the tables

#### **Customers**

| customer\_id | name  |
| ------------ | ----- |
| 101          | Alice |
| 102          | Bob   |
| 103          | Carol |
| 104          | David |

#### **Orders**

| order\_id | customer\_id | amount |
| --------- | ------------ | ------ |
| 1         | 101          | 500    |
| 2         | 102          | 300    |
| 3         | 103          | 450    |
| 4         | 101          | 250    |
| 5         | 102          | 600    |
| 6         | 104          | 150    |

### Question: Write a query (using **CTE**) to find customers who have placed orders worth **more than 700 in total**.

#### Explanation:

```sql
WITH totalCte AS (
    SELECT o.customer_id, c.name, SUM(o.amount) AS total
    FROM Customers c
    JOIN Orders o 
      ON c.customer_id = o.customer_id
    GROUP BY o.customer_id, c.name
)
SELECT name, total
FROM totalCte
WHERE total > 700;
```

---

## Chained CTE's

### Syntax

You can define more than one CTE by separating them with a comma:

```sql
WITH cte1 AS (
    SELECT ...
),
cte2 AS (
    SELECT ...
)
SELECT ...
FROM cte1
JOIN cte2 ON ...;
```

### Example with our **Customers** and **Orders** tables

**Goal:**

1. First CTE → calculate total order amount per customer.
2. Second CTE → filter only customers who spent more than 700.
3. Final query → join back to show details.

```sql
WITH CustomerTotals AS (
    SELECT customer_id, SUM(amount) AS total
    FROM Orders
    GROUP BY customer_id
),
HighValueCustomers AS (
    SELECT customer_id, total
    FROM CustomerTotals
    WHERE total > 700
)
SELECT c.name, h.total
FROM Customers c
JOIN HighValueCustomers h
  ON c.customer_id = h.customer_id;
```

#### Result (from our sample data)

| name  | total |
| ----- | ----- |
| Alice | 750   |
| Bob   | 900   |

### Question: Write **two-CTE query** to get:

1. CTE1 → average order amount per customer.
2. CTE2 → customers whose **average order amount** is more than **400**.
3. Final query → show customer name + average.

#### Explanation:

```sql
WITH cte1 AS (
    SELECT c.customer_id, c.name, AVG(o.amount) AS average
    FROM Customers c
    JOIN Orders o ON c.customer_id = o.customer_id
    GROUP BY c.customer_id, c.name
),
cte2 AS (
    SELECT customer_id, name, average
    FROM cte1
    WHERE average > 400
)
SELECT name, average
FROM cte2;
```



