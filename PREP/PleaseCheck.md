Please refer to the below:

https://github.com/Malobika8/All-In-One/tree/Hibernate/PREP

# Question:

When you call `entityManager.persist(entity)` on a **Transient** entity, what state does it move to, and when is the SQL `INSERT` actually executed?

### Answer:

After `persist(entity)`, the object moves from **Transient → Persistent** state.

But for the **second part** — the SQL `INSERT` is **not** necessarily executed immediately after `persist()`.

* In JPA, `persist()` just makes the entity **managed** by the persistence context.
* The actual `INSERT` SQL is sent **at flush time** — which could happen:

  1. Automatically **before** a transaction commit
  2. If you explicitly call `entityManager.flush()`
  3. Or if the persistence provider flushes due to a query execution that requires up-to-date data

So `persist()` ≠ "immediate insert" — it’s "schedule insert".


