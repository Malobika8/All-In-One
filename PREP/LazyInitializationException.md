## LazyInitializationException

* When a **LAZY association** is accessed **outside the persistence context** (e.g., after the `EntityManager` is closed or the transaction ends), JPA **cannot fetch the data** from the database.
* Example:

```java
Department dept = entityManager.find(Department.class, 1L);
entityManager.close(); // persistence context closed

int size = dept.getEmployees().size(); // LazyInitializationException
```

* Key point: **The proxy needs an active persistence context** to load the data.

* If the child collection is **empty**, no exception is thrown — the exception occurs only when JPA tries to fetch data and **cannot access the database**.

---

> *LAZY fetch requires an active persistence context. Accessing the association outside it triggers `LazyInitializationException`.*

---


