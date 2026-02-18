# 🧠 Situation 1 — “Update API Works But Data Not Updated”

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



