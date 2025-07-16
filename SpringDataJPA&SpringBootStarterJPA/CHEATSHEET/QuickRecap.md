# ✅ Spring Data JPA – Quick Revision Sheet (For Interviews)

---

## 1. **Spring Data JPA Hierarchy**

| Interface                    | Features                                               |
| ---------------------------- | ------------------------------------------------------ |
| `CrudRepository<T, ID>`      | Basic CRUD: save, findById, deleteById, etc.           |
| `PagingAndSortingRepository` | Adds paging and sorting (`findAll(Pageable)` etc.)     |
| `JpaRepository<T, ID>`       | Full feature set: CRUD + Paging + JPA-specific helpers |

✅ We always prefer `JpaRepository` — it inherits everything.

---

## 2. **Derived Query Methods (Method Name Queries)**

### 🔹 Basic Filters:

```java
List<Employee> findByName(String name);
List<Employee> findBySalaryGreaterThan(int salary);
List<Employee> findByDepartment_DepartmentName(String name);
```

### 🔹 Advanced Filters:

```java
List<Employee> findByNameStartingWith(String prefix);
List<Employee> findByNameContainingIgnoreCase(String keyword);
List<Employee> findBySalaryBetween(int min, int max);
List<Employee> findBySalaryIsNotNull();
```

### 🔹 Top/N Results:

```java
List<Employee> findTop3ByDepartment_DepartmentNameOrderBySalaryDesc(String departmentName);
```

### 🔹 Combined:

```java
List<Employee> findByDepartment_DepartmentNameInAndSalaryIsNotNullOrderBySalaryDesc(List<String> names);
```

---

## 3. **Paging & Sorting**

### 🔹 Using Pageable:

```java
Page<Employee> findByNameContainingIgnoreCase(String name, Pageable pageable);
```

### 🔹 Creating a Pageable:

```java
Pageable pageable = PageRequest.of(0, 5, Sort.by("salary").descending());
```

### 🔹 Multiple Sort Criteria:

```java
Sort sort = Sort.by("department.departmentName").ascending()
               .and(Sort.by("salary").descending());
```

---

## 4. **@Query (JPQL / Native)**

### 🔹 JPQL with DTO:

```java
@Query("SELECT new com.test.EmployeeSalaryDTO(e.name, e.salary) FROM Employee e WHERE e.salary > :sal")
List<EmployeeSalaryDTO> findBySalary(@Param("sal") int salary);
```

### 🔹 Aggregation + Group By + Having:

```java
@Query("SELECT new com.test.DepartmentAvgSalaryDTO(e.department.departmentName, AVG(e.salary)) FROM Employee e GROUP BY e.department.departmentName HAVING AVG(e.salary) > :sal")
List<DepartmentAvgSalaryDTO> findWithAvgSalary(@Param("sal") int salary);
```

---

## 5. **Native Query with DTO (@NamedNativeQuery + @SqlResultSetMapping)**

### 🔹 Example:

```sql
SELECT d.dep_name AS departmentName, COUNT(e.id) AS count
FROM employee e
JOIN department d ON e.dep_id = d.id
GROUP BY d.dep_name
HAVING COUNT(e.id) > 3
```

### 🔹 DTO Mapping:

```java
@SqlResultSetMapping(
  name = "DepartmentEmployeeCountDTOMapping",
  classes = @ConstructorResult(
    targetClass = DepartmentEmployeeCountDTO.class,
    columns = {
      @ColumnResult(name = "departmentName", type = String.class),
      @ColumnResult(name = "count", type = Long.class)
    }
  )
)
```

### 🔹 Usage:

```java
@NamedNativeQuery(
  name = "Employee.findDepartmentAndEmployee",
  query = "...",
  resultSetMapping = "DepartmentEmployeeCountDTOMapping"
)
```

---

## 6. **Best Practices**

✅ Use method name queries where possible
✅ Use `@Query` only for complex queries
✅ Use native queries only when:

* You need DB-specific features
* JPQL doesn’t support the query

✅ Prefer pagination for large datasets
✅ Always test custom queries + DTO mappings

---

