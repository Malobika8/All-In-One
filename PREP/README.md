### ✅ JPA Core

* Entity states & transitions
* `persist` vs `merge`
* Persistence context & dirty checking
* `flush()` vs `commit()`
* `find()` vs `getReference()`

### ✅ Relationships

* Owning vs inverse side
* `mappedBy`
* Cascade vs `orphanRemoval`
* Lazy vs eager fetching

### ✅ JPQL

* Joins, subqueries, grouping, DTO projections
* `JOIN` vs `JOIN FETCH`
* Pagination limitations

### ✅ Performance

* First-level vs second-level cache
* N+1 problem + fixes:

  * `JOIN FETCH`
  * `@EntityGraph`
  * `@BatchSize`

### ✅ Concurrency

* Optimistic locking (`@Version`)
* Pessimistic locking (`PESSIMISTIC_WRITE`)

## Optional Advanced

* Query cache vs second-level cache
* `@NamedQuery`
* Flush modes
* `@MapsId`
* Composite keys


