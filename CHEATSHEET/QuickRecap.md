**Comprehensive cheatsheet of EntityManager methods in JPA/Hibernate**, focused on **query result-related methods**, including return types. This will help recall what method returns what, especially while using `EntityManager` for fetching data.

---

### ✅ **EntityManager Query Result Methods – Cheatsheet**

| **Method**                                                                 | **Return Type**        | **Description**                                          |
| -------------------------------------------------------------------------- | ---------------------- | -------------------------------------------------------- |
| `createQuery(String jpql)`                                                 | `Query`                | Creates a JPQL query (untyped).                          |
| `createQuery(String jpql, Class<T> resultClass)`                           | `TypedQuery<T>`        | Creates a typed JPQL query.                              |
| `createNamedQuery(String name)`                                            | `Query`                | Creates an untyped named query.                          |
| `createNamedQuery(String name, Class<T> resultClass)`                      | `TypedQuery<T>`        | Creates a typed named query.                             |
| `createNativeQuery(String sql)`                                            | `Query`                | Creates an SQL (native) query.                           |
| `createNativeQuery(String sql, Class<T> resultClass)`                      | `Query`                | Maps native query result to entity class.                |
| `createNativeQuery(String sql, String resultSetMapping)`                   | `Query`                | Uses a defined SQL result set mapping.                   |
| `find(Class<T> entityClass, Object primaryKey)`                            | `T`                    | Finds an entity by primary key.                          |
| `getReference(Class<T> entityClass, Object primaryKey)`                    | `T`                    | Lazy proxy for an entity. Throws exception if not found. |
| `createStoredProcedureQuery(String procedureName)`                         | `StoredProcedureQuery` | For stored procedures.                                   |
| `createStoredProcedureQuery(String procedureName, Class... resultClasses)` | `StoredProcedureQuery` | With result class mapping.                               |

---

### ✅ **Query Execution Result Methods (from Query/TypedQuery)**

| **Method**          | **Return Type** | **Used For**                                                                  |
| ------------------- | --------------- | ----------------------------------------------------------------------------- |
| `getResultList()`   | `List<T>`       | Gets all results of a query.                                                  |
| `getSingleResult()` | `T`             | Gets single result, throws `NoResultException` or `NonUniqueResultException`. |
| `executeUpdate()`   | `int`           | For update/delete queries; returns number of rows affected.                   |
| `unwrap(Class<T>)`  | `T`             | Unwraps to native Hibernate query if needed.                                  |

---

### ✅ **StoredProcedureQuery Result Methods**

| **Method**                                      | **Return Type** | **Used For**                                |
| ----------------------------------------------- | --------------- | ------------------------------------------- |
| `getOutputParameterValue(String/Integer param)` | `Object`        | Gets output param from stored proc.         |
| `getResultList()`                               | `List`          | Gets result list (if procedure returns it). |
| `getSingleResult()`                             | `Object`        | Gets single result.                         |

---

### ✅ **Special Helper Methods from EntityManager**

| **Method**                | **Return Type** | **Used For**                                    |
| ------------------------- | --------------- | ----------------------------------------------- |
| `contains(Object entity)` | `boolean`       | Checks if entity is in persistence context.     |
| `flush()`                 | `void`          | Synchronizes persistence context with DB.       |
| `clear()`                 | `void`          | Clears persistence context (detaches all).      |
| `merge(T entity)`         | `T`             | Merges detached entity and returns managed one. |
| `persist(Object entity)`  | `void`          | Makes transient entity persistent.              |
| `remove(Object entity)`   | `void`          | Removes managed entity.                         |

---

### ✅ **Example: Fetching with TypedQuery**

```java
TypedQuery<String> tq = em.createQuery("SELECT e.name FROM Employee e", String.class);
List<String> names = tq.getResultList(); // returns List<String>
```

### ✅ **Example: Single Result**

```java
TypedQuery<Employee> tq = em.createQuery("SELECT e FROM Employee e WHERE e.id = :id", Employee.class);
tq.setParameter("id", 101);
Employee emp = tq.getSingleResult(); // returns one Employee or throws exception
```

---
