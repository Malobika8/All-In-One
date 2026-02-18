# Situation 1 — “Update API Works But Data Not Updated”

### Interviewer says:

> We have an update API.
> It returns 200 OK.
> But database values are not changing.
> No errors in logs.
> What could be the reason?

### Given Code:

```java
public Employee update(int id, Employee employee) {
    Employee emp = employeeRepo.findById(id)
            .orElseThrow(() -> new RuntimeException("Not found"));

    emp.setName(employee.getName());
    emp.setDepartment(employee.getDepartment());
    emp.setSalary(employee.getSalary());

    return emp;
}
```

Controller:

```java
@PutMapping("/employee/{id}")
public ResponseEntity<Employee> update(@PathVariable int id,
                                       @RequestBody Employee employee) {
    return ResponseEntity.ok(employeeService.update(id, employee));
}
```

### Question For You

Why is the DB not updating?

1. Most likely cause
2. Other possible causes
3. How would you debug it in production

### Explanation

Look carefully at service:

```java
public Employee update(...) {
    Employee emp = employeeRepo.findById(id)
            .orElseThrow(...);

    emp.setName(...);
    emp.setDepartment(...);
    emp.setSalary(...);

    return emp;
}
```

⚠️ There is NO `@Transactional`
⚠️ There is NO `save()`

So what happens?

* `findById()` runs in its own repository transaction
* That transaction ends after method returns
* Entity becomes DETACHED
* You modify detached entity
* No dirty checking
* No flush
* No update

👉 DB won’t change.

> Most likely the service method is not transactional and save() is not being called, so the entity becomes detached and dirty checking does not persist changes.

#### Other Possible Causes 

1️⃣ No `@Transactional` and no save
2️⃣ readOnly = true used somewhere
3️⃣ Entity is detached manually (e.g., using DTO mapping incorrectly)
4️⃣ Database trigger rolling back silently
5️⃣ Exception happening but swallowed somewhere
6️⃣ Wrong datasource (updating test DB but checking prod DB)
7️⃣ Optimistic locking failure (`@Version`)
8️⃣ Hibernate flush mode set to MANUAL
9️⃣ ID mismatch — updating wrong entity
🔟 Caching issue (second-level cache)

Strong debugging answer:

1. Enable SQL logs:
   ```
   spring.jpa.show-sql=true
   logging.level.org.hibernate.SQL=DEBUG
   ```
2. Check if UPDATE query is generated.
   * If no update SQL → dirty checking issue / no transaction
   * If update SQL generated → check commit
3. Add log inside service:
   ```
   System.out.println(TransactionSynchronizationManager.isActualTransactionActive());
   ```
4. Check if method has `@Transactional`.
5. Verify datasource connection.

---

# If you were designing a high-concurrency system: Would you always use optimistic locking? Or are there cases where pessimistic locking is better?

### Explanation:

### Optimistic Locking — When It’s Best

Characteristics:

* No DB row lock
* Conflict checked at commit time
* Uses `@Version`
* Fails fast on conflict

Best for:

* ✅ Read-heavy systems
* ✅ Low probability of conflict
* ✅ Short transactions
* ✅ Web applications (user think-time between read & write)

Why?

Because holding DB locks during user think-time is dangerous.

Imagine:

User opens edit form
Goes for coffee ☕
Comes back after 5 minutes
Clicks Save

If you had pessimistic locking, that row would be locked for 5 minutes. That’s terrible.

So for most REST applications:

👉 Optimistic locking is preferred.

### Now About Write-Heavy Systems

> For write heavy systems pessimistic might be better.

This is sometimes true, but depends.

Pessimistic locking:

```java
@Lock(LockModeType.PESSIMISTIC_WRITE)
```

What it does:

* Acquires DB-level lock (`SELECT ... FOR UPDATE`)
* Other transactions must wait

Good when:

* High conflict probability
* Short transactions
* Critical financial operations
* Inventory deduction systems

Example:

* Stock trading
* Bank balance updates
* Payment systems

#### But Important Clarification

Pessimistic locking is NOT always better for write-heavy systems.

If contention is very high:

* Threads will block
* Throughput drops
* Deadlocks may occur
* DB becomes bottleneck

So decision depends on:

* Conflict frequency
* Transaction duration
* Business tolerance for retries

#### Clean Comparison

| Feature                | Optimistic | Pessimistic |
| ---------------------- | ---------- | ----------- |
| Locks row immediately  | ❌          | ✅           |
| Risk of deadlock       | ❌          | ✅           |
| Best for read-heavy    | ✅          | ❌           |
| Best for high-conflict | ❌          | ✅           |
| Scales better          | ✅          | ❌           |
| Requires retry logic   | ✅          | ❌           |

> When would you choose pessimistic over optimistic locking?

> I would choose pessimistic locking in high-conflict scenarios involving critical updates like financial transactions or inventory deduction, where preventing concurrent modification is more important than throughput. For most web applications with low conflict probability, optimistic locking is preferred because it scales better and avoids long-held database locks.

---

