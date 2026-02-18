# We try to add departments and employees in the beginning itself through CoomandLineRunner. But we get an exception. What could be the cause?
```
package com.practice.SpringPractice.dataloader;

import com.practice.SpringPractice.model.Department;
import com.practice.SpringPractice.model.Employee;
import com.practice.SpringPractice.respository.DepartmentRepo;
import com.practice.SpringPractice.respository.EmployeeRepo;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.CommandLineRunner;
import org.springframework.stereotype.Component;

import java.util.List;

@Component
public class DataLoader implements CommandLineRunner {

    @Autowired
    private EmployeeRepo employeeRepo;

    @Autowired
    private DepartmentRepo departmentRepo;

    @Override
    public void run(String... args) throws Exception {
        if(departmentRepo.count()==0){
            Department d1 = new Department();
            d1.setName("IT");
            d1.setLocation("Bangalore");
            d1.setCode(101L);

            Department d2 = new Department();
            d2.setName("HR");
            d2.setLocation("Bangalore");
            d2.setCode(102L);

            Department d3 = new Department();
            d3.setName("Finance");
            d3.setLocation("Mumbai");
            d3.setCode(103L);

            departmentRepo.saveAll(List.of(d1, d2, d3));
        }

        // 2️⃣ Fetch all departments
        List<Department> departments = departmentRepo.findAll();

        // Safety check
        if (departments.isEmpty()) {
            throw new RuntimeException("No departments found even after inserting!");
        }

        if(employeeRepo.count() > 0) return; // only once

        for(int i=1; i<=3000; i++) {
            Employee emp = new Employee();
            emp.setName("Employee " + i);
            emp.setSalary(3000L + (i * 10));

            // Assign department in round-robin
            Department dept = departments.get(i % departments.size());
            emp.setDepartment(dept);

            employeeRepo.save(emp);
        }
    }
}
```

```
java.lang.RuntimeException: No departments found even after inserting!
	at com.practice.SpringPractice.dataloader.DataLoader.run(DataLoader.java:48) ~[classes/:na]
```

## Explanation:

### The problem

* Hibernate **doesn’t immediately flush inserts to the database** until it needs to (or transaction commits).
* `departmentRepository.findAll()` **may run in the same transaction**, but **if something with transactional context is misconfigured** or `saveAll` didn’t flush yet, `findAll()` can still return empty.
* That triggers your RuntimeException.

### How to fix

#### Option 1 — **Flush after saveAll**

```java
departmentRepository.saveAll(List.of(d1, d2, d3));
departmentRepository.flush(); // <-- force flush to DB immediately
```

* Now `findAll()` will definitely see the inserted rows.

#### Option 2 — **Assign directly instead of fetching again**

```java
List<Department> departments = List.of(d1, d2, d3);
```
* Since you already have the Department objects from saveAll, no need to call `findAll()` again.

#### Option 3 — **Use transaction properly**

* Make sure `DataLoader.run()` is inside a **transactional context** (Spring Boot will auto-wrap `CommandLineRunner` in a transaction if you annotate class or method with `@Transactional`)
* Then `findAll()` should see the inserts.

### 1. Default Flush Mode in Spring Boot / Hibernate

* **FlushModeType.AUTO** is the default.
* Meaning: **before executing a query**, Hibernate should flush all pending changes in the persistence context to the DB.
* So normally, your `findAll()` **should see the entities you just `saveAll()`**.

### 2. When flush might NOT happen

Even in `AUTO` mode, a query **won’t trigger a flush** if:

1. **The query is a native SQL query** instead of JPQL → Hibernate doesn’t manage flush automatically
2. **The query is inside a different transaction or persistence context** → your uncommitted entities are invisible
3. **The session/persistence context was cleared or closed** before query executes → unlikely in CommandLineRunner, but possible if something else is messing with context
4. **You used read-only transactions** (e.g., `@Transactional(readOnly = true)`) → flush is skipped intentionally for performance
5. **Batch insert / caching / JDBC driver issues** → some inserts are delayed in batch and not flushed immediately

### 3. Likely scenario in your case

* You didn’t mark `readOnly = true`, and the flush mode is AUTO.
* But Hibernate **may delay flush until it thinks it’s necessary**.

```java
departmentRepository.saveAll(...);
List<Department> departments = departmentRepository.findAll();
```

* Hibernate sometimes decides **it hasn’t reached the flush point** yet before `findAll()`
* Especially if you have **cascade, ID generation, or entity manager peculiarities**
* Result → `findAll()` query executes → DB still empty → exception

### How to guarantee safety

1. **Call flush explicitly** after inserts:

```java
departmentRepository.saveAll(List.of(d1, d2, d3));
departmentRepository.flush(); // forces SQL execution
```

2. **Or just use the entities you inserted** instead of querying again:

```java
List<Department> departments = List.of(d1, d2, d3);
```

* No query → avoids any flush uncertainty
* Safe in same transaction

✅ **TL;DR**

* `findAll()` normally **flushes automatically** with default flush mode (AUTO)
* But Hibernate **may not flush in some edge cases** → your “no departments found” error can happen
* Explicit `flush()` or using the in-memory entities avoids the problem







