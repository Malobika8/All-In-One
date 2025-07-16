# You want a repository that supports:

* Basic CRUD
* Sorting results by salary descending
* Pagination

👉 Which Spring Data JPA interface should you extend?

### Sol:

Would extend JpaRepository because it inherits from both CrudRepository and PagingAndSortingRepository, and it also adds useful JPA-specific methods like findAllById, flush, and saveAll.
It’s the most complete and commonly used interface in Spring Data JPA.

---

## Derived Query Methods in Spring Data JPA

*(a.k.a. method-name-based queries)*

#### What are these?

Spring Data JPA lets you define queries **just by naming methods properly** in your repository interface.
No SQL, no JPQL — Spring parses the method name and builds the query!

#### Example:

```java
public interface EmployeeRepository extends JpaRepository<Employee, Integer> {
    List<Employee> findBySalaryGreaterThan(int salary);
}
```

✅ Spring auto-generates this:

```sql
SELECT * FROM employee WHERE salary > ?
```

#### 🔤 Common Keywords You Can Use

| Keyword                                            | Meaning                 |
| -------------------------------------------------- | ----------------------- |
| `findBy...`                                        | Start of a query method |
| `And`, `Or`                                        | Combine conditions      |
| `GreaterThan`, `LessThan`, `Between`               | Range conditions        |
| `Like`, `StartingWith`, `EndingWith`, `Containing` | Pattern matching        |
| `In`, `NotIn`                                      | For collections         |
| `IsNull`, `IsNotNull`                              | Null checks             |
| `OrderBy`                                          | Sorting                 |
| `Top`, `First`                                     | Limit result            |

#### Sample Queries:

```java
List<Employee> findByDepartment_DepartmentName(String name);
List<Employee> findByNameStartingWith(String prefix);
List<Employee> findBySalaryBetween(int min, int max);
List<Employee> findByNameIn(List<String> names);
List<Employee> findTop3ByOrderBySalaryDesc();
```

---

# Write a method in your `EmployeeRepository` that:

* Returns all employees in the **"IT"** department
* Whose salary is **greater than 70000**

### Sol:

```
List<Employee> findByDepartment_DepartmentNameAndSalaryGreaterThan(String departmentName, int salary);
```

---

# Write a repository method to:

✅ Find all employees whose name starts with "M"
✅ And salary is less than 80000

### Sol:

```
List<Employee> findByNameStartingWithAndSalaryLessThan(String str, int salary);
```

---

# Write a repository method to:

✅ Find top 5 highest-paid employees
✅ From the "HR" department
✅ Ordered by salary in descending order

### Sol:

In Spring Data JPA, Top5 should appear at the start, like findTop5By...

```
List<Employee> findTop5ByDepartment_DepartmentNameOrderBySalaryDesc(String departmentName);
```

---

# Write a repository method to:

> ✅ Find all employees whose name **contains `"a"`** (case-insensitive)
> ✅ And whose salary is **between 50000 and 100000**
> ✅ Order the results by name ascending

### Sol:

- Parameter order must match the method signature
- Contains is case-sensitive → we’ll use ContainingIgnoreCase for case-insensitive search

```
List<Employee> findByNameContainingIgnoreCaseAndSalaryBetweenOrderByNameAsc(String str, int min, int max);
```

---

# Write a repository method to:

✅ Find all employees who belong to any one of several departments (passed as a list of names)
✅ And whose salary is not null

### Sol:

```
List<Employee> findByDepartment_DepartmentNameInAndSalaryIsNotNull(List<String> departmentNames);
```




