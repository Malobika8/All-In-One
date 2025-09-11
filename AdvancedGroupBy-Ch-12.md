## 🔹 1. GROUP BY ROLLUP

`ROLLUP` gives you **subtotals + grand total**.

### Example:

**Sales Table**

| region | product | amount |
| ------ | ------- | ------ |
| East   | Pen     | 100    |
| East   | Pencil  | 50     |
| West   | Pen     | 200    |
| West   | Pencil  | 150    |

Query:

```sql
SELECT region, product, SUM(amount) AS total_sales
FROM Sales
GROUP BY ROLLUP(region, product);
```

### Result:

| region | product | total\_sales              |
| ------ | ------- | ------------------------- |
| East   | Pen     | 100                       |
| East   | Pencil  | 50                        |
| East   | NULL    | 150   ← subtotal for East |
| West   | Pen     | 200                       |
| West   | Pencil  | 150                       |
| West   | NULL    | 350   ← subtotal for West |
| NULL   | NULL    | 500   ← grand total       |

👉 `ROLLUP` = subtotals + grand total.

---

## 🔹 2. GROUP BY CUBE

`CUBE` gives you **all combinations** of grouping (more detailed than ROLLUP).

Query:

```sql
SELECT region, product, SUM(amount) AS total_sales
FROM Sales
GROUP BY CUBE(region, product);
```

### Result:

| region | product | total\_sales                |
| ------ | ------- | --------------------------- |
| East   | Pen     | 100                         |
| East   | Pencil  | 50                          |
| West   | Pen     | 200                         |
| West   | Pencil  | 150                         |
| East   | NULL    | 150   ← subtotal by region  |
| West   | NULL    | 350   ← subtotal by region  |
| NULL   | Pen     | 300   ← subtotal by product |
| NULL   | Pencil  | 200   ← subtotal by product |
| NULL   | NULL    | 500   ← grand total         |

👉 `CUBE` = every possible subtotal + grand total.

---

## 🔹 3. GROUPING SETS

`GROUPING SETS` lets you **customize which subtotals** you want.

Query:

```sql
SELECT region, product, SUM(amount) AS total_sales
FROM Sales
GROUP BY GROUPING SETS ((region), (product), ());
```

### Result:

| region | product | total\_sales        |
| ------ | ------- | ------------------- |
| East   | NULL    | 150                 |
| West   | NULL    | 350                 |
| NULL   | Pen     | 300                 |
| NULL   | Pencil  | 200                 |
| NULL   | NULL    | 500   ← grand total |

👉 Only the subtotals you asked for, nothing extra.

---

✅ So in short:

* **ROLLUP** → hierarchy totals (like Region → Product → Grand Total).
* **CUBE** → all possible totals.
* **GROUPING SETS** → custom totals.

---

