## 🔹 What is a Transaction?

A **transaction** is a logical unit of work that groups one or more SQL operations together.
Either **all succeed** (commit) or **all fail** (rollback).

👉 Example (Bank transfer):

```sql
-- Transfer 500 from Alice → Bob
BEGIN;

UPDATE Accounts SET balance = balance - 500 WHERE account_id = 1; -- Alice
UPDATE Accounts SET balance = balance + 500 WHERE account_id = 2; -- Bob

COMMIT;
```

* If both updates succeed → changes are saved.
* If one update fails → `ROLLBACK` restores original balances.

## 🔹 ACID Properties

These are guarantees a database provides for transactions:

1. **Atomicity** – *All or nothing.*

   * If one part fails, the whole transaction fails.
   * Ensures **no partial updates**.
   * E.g., in bank transfer: money can’t disappear if only Alice’s account was updated.

2. **Consistency** – *Database rules remain valid.*

   * Ensures integrity constraints (PK, FK, check constraints) are not violated.
   * E.g., total money in system stays same after transfer.

3. **Isolation** – *Transactions don’t affect each other midway.*

   * Prevents issues like dirty reads, non-repeatable reads.
   * Controlled using **isolation levels**

4. **Durability** – *Once committed, it’s permanent.*

   * Even if server crashes, committed data is safe (stored on disk/logs).

## 🔹 Commands in Transactions

* `BEGIN` / `START TRANSACTION` → start a transaction.
* `COMMIT` → permanently save changes.
* `ROLLBACK` → undo changes since transaction began.
* `SAVEPOINT name; ROLLBACK TO name;` → roll back part of a transaction.

👉 Example with savepoint:

```sql
BEGIN;

UPDATE Accounts SET balance = balance - 500 WHERE account_id = 1;
SAVEPOINT after_alice;

UPDATE Accounts SET balance = balance + 500 WHERE account_id = 2;

-- Oops! Something went wrong, rollback only Bob’s update
ROLLBACK TO after_alice;

COMMIT;
```
---

## 🔹 Transaction Problems

#### 1. **Dirty Read**

* One transaction reads **uncommitted** data from another transaction.
* If the other transaction rolls back, the first one read something that never really existed.

👉 Example:

* **T1:** `UPDATE Accounts SET balance = balance - 500 WHERE account_id = 1;` (not committed yet)
* **T2:** `SELECT balance FROM Accounts WHERE account_id = 1;` → sees reduced balance
* Then **T1 does ROLLBACK** → T2 saw a “ghost value.”

#### 2. **Non-Repeatable Read**

* Same query in the **same transaction** gives different results because another transaction modified the data in between.

👉 Example:

* **T1:** `SELECT balance FROM Accounts WHERE account_id = 1;` → gets `1000`
* **T2:** `UPDATE Accounts SET balance = 1200 WHERE account_id = 1; COMMIT;`
* **T1 again:** `SELECT balance FROM Accounts WHERE account_id = 1;` → now sees `1200` instead of `1000`.
* Data **changed mid-transaction** → non-repeatable read.

#### 3. **Phantom Read**

* A transaction re-runs a query and **new rows appear/disappear** because another transaction inserted/deleted rows.

👉 Example:

* **T1:** `SELECT * FROM Orders WHERE amount > 1000;` → gets 5 rows
* **T2:** `INSERT INTO Orders VALUES (9999, 101, '2025-09-11', 2000); COMMIT;`
* **T1 again:** `SELECT * FROM Orders WHERE amount > 1000;` → now gets 6 rows
* The “phantom row” appeared.

📌 Summary Table:

| Problem                 | Cause                                            |
| ----------------------- | ------------------------------------------------ |
| **Dirty Read**          | Read uncommitted data                            |
| **Non-Repeatable Read** | Same row updated by another transaction          |
| **Phantom Read**        | New rows inserted/deleted by another transaction |

---

## 🔹 SQL Isolation Levels

Each level **prevents some problems but allows others**, balancing **consistency vs performance**.

#### 1. **READ UNCOMMITTED** (lowest level)

* Transactions can **see uncommitted changes** of others.
* **Dirty reads possible** ✅
* Non-repeatable reads possible ✅
* Phantom reads possible ✅
* Almost never used in production (unsafe).

#### 2. **READ COMMITTED**

* A transaction only sees data that has been **committed**.
* **Dirty reads prevented** ❌
* Non-repeatable reads possible ✅
* Phantom reads possible ✅
* **Default in: Oracle, SQL Server, PostgreSQL.**

👉 Example:

* If T1 updates but hasn’t committed → T2 **cannot** see it.
* But if T1 commits after T2’s first read, then T2’s second read may give a new value (non-repeatable).

#### 3. **REPEATABLE READ**

* Guarantees that **if you read a row twice, it won’t change** during your transaction.
* Prevents **non-repeatable reads** ❌
* Prevents **dirty reads** ❌
* **Phantom reads still possible** ✅
* **Default in MySQL (InnoDB).**

👉 Example:

* T1 reads balance twice → same result both times.
* But if T2 inserts a new row matching T1’s WHERE condition, T1 may see new rows later (phantoms).

#### 4. **SERIALIZABLE** (highest level)

* Transactions are fully isolated, as if run **one after another in sequence**.
* Prevents **dirty reads ❌, non-repeatable reads ❌, phantom reads ❌**.
* But it’s **slow** (uses locks or MVCC to simulate serial execution).

👉 Example:

* If T1 is reading rows WHERE amount > 1000, T2 **cannot insert a new matching row** until T1 finishes.

📌 **Summary Table**

| Isolation Level  | Dirty Read  | Non-Repeatable Read | Phantom Read | Performance |
| ---------------- | ----------- | ------------------- | ------------ | ----------- |
| Read Uncommitted | ✅ Allowed   | ✅ Allowed           | ✅ Allowed    | Fastest     |
| Read Committed   | ❌ Prevented | ✅ Allowed           | ✅ Allowed    | Medium      |
| Repeatable Read  | ❌ Prevented | ❌ Prevented         | ✅ Allowed    | Slower      |
| Serializable     | ❌ Prevented | ❌ Prevented         | ❌ Prevented  | Slowest     |

---

# **Question: Banking System Isolation**

You are designing a **banking application** with the following requirements:

1. Users frequently check their account balances (read-heavy).
2. Money transfers must never allow **dirty reads** or **inconsistent balances**.
3. Performance is also important because there are thousands of concurrent users.

👉 **Question:**

* Which **isolation level** would you choose here?
* Why not the other levels?

### Explanation:

#### Why **Repeatable Read** makes sense:

* Prevents **dirty reads** → ✔ money transfer safety.
* Prevents **non-repeatable reads** → ✔ balances won’t suddenly change inside the same transaction.
* Still allows good performance → ✔ because it avoids full serial execution.
* This is why **MySQL (InnoDB)** chose it as the **default**.

#### But the catch:

* **Phantom reads** are still possible.

  * Example: If you check *all* accounts with balance > 1000, new rows could appear mid-transaction.
  * Not usually a problem for single-account banking operations, but important in **aggregate queries**.

#### Why not others?

* **Read Uncommitted** → unsafe, allows dirty reads ❌
* **Read Committed** → better, but still allows non-repeatable reads ❌
* **Serializable** → safest, but too slow for thousands of concurrent users ❌

- Repeatable Read is correct for most banking systems where performance and consistency must balance.
- In critical cases (like end-of-day settlement reports across all accounts), banks may temporarily use Serializable.
  
---




