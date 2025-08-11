### **1️⃣ `find()`**

* **Immediately hits the database** to fetch the entity data.
* Returns the actual entity object with all its fields populated.
* If the entity doesn’t exist, returns `null`.
* Example:

  ```java
  MyEntity e = em.find(MyEntity.class, 1);
  ```

  At this point, the DB is queried right away.

---

### **2️⃣ `getReference()`**

* **Does NOT hit the database immediately** — returns a **lazy proxy** of the entity.
* The DB query is executed **only when you try to access a property** (except the ID).
* If the entity doesn’t exist, it throws **`EntityNotFoundException`** when the proxy is accessed.
* Example:

  ```java
  MyEntity e = em.getReference(MyEntity.class, 1);
  ```

  Here, no DB call is made until you do something like `e.getName()`.

---

💡 **Key points:**

* Use `find()` when you know you need the full entity immediately.
* Use `getReference()` for performance when you only need a reference (like for setting relationships) without loading all fields.

---

