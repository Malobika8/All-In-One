## Writing Custom JPQL with `@Query` in Spring Data JPA

#### Why use `@Query`?

While method names are great, they:

* Can get too long/awkward for complex queries
* May not cover all scenarios (joins, projections, subqueries)

👉 That’s where `@Query` shines — it lets you write **custom JPQL** inside repository interfaces.

#### Syntax Example:

```java
@Query("SELECT e FROM Employee e WHERE e.salary > :sal")
List<Employee> getEmployeesWithSalaryAbove(@Param("sal") int salary);
```

✅ You can use named parameters like `:sal`, or use positional `?1`, `?2`

#### Sample Use Cases:

```java
// Employees in a specific department
@Query("SELECT e FROM Employee e WHERE e.department.departmentName = :dept")
List<Employee> findByDept(@Param("dept") String department);

// Employees with names like "M%"
@Query("SELECT e FROM Employee e WHERE e.name LIKE :prefix%")
List<Employee> findByNameStartsWith(@Param("prefix") String prefix);

// Aggregate query: department name + avg salary
@Query("SELECT e.department.departmentName, AVG(e.salary) FROM Employee e GROUP BY e.department.departmentName")
List<Object[]> getAvgSalaryByDepartment();
```

#### Bonus: DTO Projection with `@Query`

```java
@Query("SELECT new com.example.dto.EmployeeNameDTO(e.id, e.name) FROM Employee e")
List<EmployeeNameDTO> getAllNames();
```

✅ This uses a **JPQL constructor expression** and works great with custom DTOs.

---

# Write a custom JPQL query using `@Query` to:

> ✅ Fetch only `name` and `salary` of employees
> ✅ Where salary is greater than 70000
> ✅ And map to a DTO: `EmployeeSalaryDTO(int id, String name, int salary)`

### Sol:

```
@Query("SELECT new org.test.EmployeeSalaryDTO(e.id, e.name, e.salary) FROM Employee e WHERE e.salary > :sal")
List<EmployeeSalaryDTO> findBySalary(@Param("sal") int salary);
```

---

# Write a custom @Query in your repository to:

✅ Fetch all employees
✅ Whose department name is "Finance"
✅ Return a DTO with:
   - Employee's name
   - Department's departmentName

### Sol:

```
@Query("SELECT new org.test.EmployeeDepartmentDTO(e.name, e.department.departmentName) FROM Employee e WHERE e.department.departmentName = :depName")
List<EmployeeDepartmentDTO> findByDepartmentName(@Param("depName") String departmentName);
```

---

# Write a query to:

✅ Fetch all departments
✅ Along with their average salary
✅ Only include departments where average salary > 60000
✅ Map the result to a DTO:

### Sol:

```
@Query("SELECT new org.test.DepartmentAvgSalaryDTO(e.department.departmentName, AVG(e.salary)) " +
       "FROM Employee e GROUP BY e.department.departmentName HAVING AVG(e.salary) > :sal")
List<DepartmentAvgSalaryDTO> findByDepartmentName(@Param("sal") double salary);
```

