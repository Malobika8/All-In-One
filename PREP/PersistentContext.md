## Persistence Context (1st Level Cache)

#### What is Persistence Context?

> The **persistence context** is the in-memory store of **managed entities**
> It is maintained by the `EntityManager`

You can think of it as JPA’s internal **first-level cache**

#### Key Points:

* Every `EntityManager` has **its own** persistence context
* If you call `em.find(Employee.class, 1)` twice — it hits the DB only the **first time**
* Second time → it returns the entity from the persistence context

#### Example:

```java
Employee e1 = em.find(Employee.class, 1); // hits DB
Employee e2 = em.find(Employee.class, 1); // returns from cache (same instance)
System.out.println(e1 == e2); // true
```

---

# You call `em.find(Employee.class, 1)` twice within the same transaction. Will it hit the DB both times?

### Sol:

- The first call to em.find(Employee.class, 1) will hit the database and load the entity into the persistence context (1st-level cache).
- The second call, within the same EntityManager, will return the same managed instance from the cache — no DB hit.

This only works within the same EntityManager. If you close and reopen EM, the cache is gone — and it will hit the DB again.

---

# Second-Level Cache in Hibernate (JPA)

#### What is Second-Level Cache?

> The **first-level cache** (persistence context) is bound to a single `EntityManager`.
> The **second-level cache** is a shared, optional cache that survives across multiple sessions / entity managers.

#### Key Differences:

| Feature             | 1st-Level Cache             | 2nd-Level Cache                                           |
| ------------------- | --------------------------- | --------------------------------------------------------- |
| Scope               | Per `EntityManager`         | Per `SessionFactory` / application-wide                   |
| Enabled by default? | ✅ Yes                       | ❌ No — must be configured manually                        |
| Managed by          | JPA / Hibernate core        | Hibernate + external provider (Ehcache, Infinispan, etc.) |
| Use case            | Short-term identity caching | Long-term caching between requests                        |

#### How Second-Level Cache Works

* When you load an entity, Hibernate can **store it in a shared cache**
* Later, even if a new `EntityManager` is used, Hibernate can return the entity from this cache instead of querying the DB

#### To Enable 2nd-Level Cache (Hibernate):

1. Add a caching provider (e.g., Ehcache, Infinispan)

2. Configure Hibernate:

   ```properties
   hibernate.cache.use_second_level_cache=true
   hibernate.cache.region.factory_class=org.hibernate.cache.ehcache.EhCacheRegionFactory
   hibernate.cache.use_query_cache=true
   ```

3. Annotate entity with:

   ```java
   @Cacheable
   @org.hibernate.annotations.Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
   ```

#### Example:

```java
@Entity
@Cacheable
@org.hibernate.annotations.Cache(usage = CacheConcurrencyStrategy.READ_WRITE)
public class Employee {
    ...
}
```

---

# What’s the key difference between 1st-level and 2nd-level cache in JPA/Hibernate?

### Sol:

First-level cache is automatically managed by the EntityManager. It's local and only valid during that entity manager's life — once you close it, the cache is gone.
Second-level cache is optional and shared across entity managers. It's managed by the EntityManagerFactory (or Hibernate's SessionFactory) and allows data to be cached between multiple sessions.
First-level is always enabled, second-level must be explicitly configured and needs a caching provider like Ehcache.

---

# Can query results be cached too?

### Sol:

Yes, using Hibernate's query cache, which is separate from second-level entity cache. It requires hibernate.cache.use_query_cache=true and marking queries as cacheable.

---

# Great! Here's a **real-world caching scenario** to test your understanding of 1st-level vs 2nd-level cache:

---

# Use Case Challenge

You have:

* `Employee` entity is marked with `@Cacheable` and 2nd-level cache is enabled using Ehcache.
* You have **two separate EntityManager instances**.

Code:

```java
EntityManager em1 = emf.createEntityManager();
Employee e1 = em1.find(Employee.class, 1);
em1.close();

EntityManager em2 = emf.createEntityManager();
Employee e2 = em2.find(Employee.class, 1);
em2.close();
```

Assume employee with ID 1 exists in the DB.

#### What happens?

* How many DB hits occur in total?
* Which cache(s) are used?
* Will `e1 == e2` be true?

### Sol:

✔ Only one DB hit → from em1.find(...)
✔ Entity is then stored in second-level cache
✔ em2.find(...) retrieves from second-level cache, no DB hit
✔ e1 == e2 is false → different EntityManager = different Java object instances

Even though the entity is shared across sessions via 2nd-level cache, each EntityManager returns a new managed copy of the entity — so == comparison fails.

