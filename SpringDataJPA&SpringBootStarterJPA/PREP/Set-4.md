## Paging & Sorting in Spring Data JPA

#### Why use Paging and Sorting?

When dealing with large datasets:

* You **don’t want to load everything at once**
* You often want to **show sorted, paginated results** (e.g., in a UI table)
  
#### Interfaces You’ll Use:

| Interface                    | Purpose                           |
| ---------------------------- | --------------------------------- |
| `PagingAndSortingRepository` | Adds paging + sorting capability  |
| `JpaRepository`              | Already includes paging & sorting |

So if you're extending `JpaRepository`, you're good.

#### Step-by-Step Usage

Let’s say we have:

```java
public interface EmployeeRepository extends JpaRepository<Employee, Integer> {
    
    Page<Employee> findByDepartment_DepartmentName(String departmentName, Pageable pageable);
}
```

#### Explanation:

* `Pageable` is passed as an argument to support both paging & sorting
* Return type `Page<Employee>` gives you:

  * List of employees
  * Page metadata (total pages, current page, etc.)

#### Usage in Code:

```java
Pageable pageable = PageRequest.of(0, 5, Sort.by("salary").descending());
Page<Employee> page = employeeRepository.findByDepartment_DepartmentName("HR", pageable);

List<Employee> employees = page.getContent();
```

#### This fetches:

* First page (`page 0`)
* 5 employees
* From `"HR"` department
* Sorted by salary descending

---

# Write a repository method that:

* Returns a `Page<Employee>`
* Filters by `name` starting with a given prefix
* Accepts a `Pageable` for sorting and pagination

### Sol:

```
Page<Employee> findByNameStartingWith(String str, Pageable pageable);

public List<Employee> findByName(String str){
    Pageable pageable = PageRequest.of(0, 5)
    Page<Employee> pageResult = repository.findByNameStartingWith(str, pageable);
    
    List<Employee> list = pageResult.getContent();
    
    return list;
}
```

#### What This Does:

* Fetches **first 5 employees** whose name starts with the given string
* Returns **only the content** (`List<Employee>`)
* Efficient & pagination-safe

---

### What Else You Can Do with Paging

You can also:

```java
PageRequest.of(page, size, Sort.by("salary").descending());
```

Or multiple sort:

```java
Sort sort = Sort.by("department.departmentName").ascending().and(Sort.by("salary").descending());
Pageable pageable = PageRequest.of(0, 10, sort);
```

---

# Write a repository method to:

- Return a Page<Employee>
- Where salary is between two values (say min and max)
- And results are sorted by name in ascending order

### Sol:

```
Page<Employee> findBySalaryBetween(int min, int max, Pageable pageable);

public List<Employee> findByName(int min, int max){
    Sort sort = Sort.by("name").ascending();
    Pageable pageable = PageRequest.of(0, 5, sort);
    Page<Employee> pageResult = repository.findBySalaryBetween(min, max, pageable);
    
    List<Employee> list = pageResult.getContent();
    
    return list;
}
```

---

# Write a method to:

* Return the **top 3 employees** in a given department
* Ordered by **salary descending**
* No need to use `Pageable` — use method name query

### Sol:

```
List<Employee> findTop3ByDepartment_DepartmentNameOrderBySalaryDesc(String departmentName);
```

---

# Write a method that:

- Returns a Page<Employee>
- Filters employees whose name contains a given substring
- Sorts results by salary descending, then name ascending

### Sol:

```
Page<Employee> findByNameContainingIgnoreCase(String str, Pageable pageable);
```
```
public List<Employee> findEmployee(String str) {
    Sort sort = Sort.by("salary").descending().and(Sort.by("name").ascending()); // ✅ Fix
    Pageable pageable = PageRequest.of(0, 5, sort);

    Page<Employee> pageResult = repository.findByNameContainingIgnoreCase(str, pageable); // ✅ Fix

    return pageResult.getContent();
}
```

---

# How about filtering by salary > X, paginated and sorted by department name ascending?

### Sol:

```
List<Employee> findBySalaryGreaterThan(int salary, Pageable pageable);

public List<Employee> findEmployee(int salary){
    Sort sort = Sort.by("department.departmentName").ascending();
    Pageable pageable = PageRequest.of(0, 5, sort);
    Page<Employee> pageResult = repository.findBySalaryGreaterThan(salary.pageable);
    
    List<Employee> list = pageResult.getContent();
    
    return list;
}
```

---

# Write a method to:

- Return a page of employees
- From a list of department names
- Whose salary is not null
- Ordered by salary descending

### Sol:

```
Page<Employee> findByDepartment_DepartmentNameInAndSalaryIsNotNullOrderBySalaryDesc(List<String> departmentNames, Pageable pageable);

public List<Employee> findEmployee(List<String> departmentNames){
    Pageable pageable = PageRequest.of(0, 5);
    Page<Employee> pageResult = repository.findByDepartment_DepartmentNameInAndSalaryIsNotNullOrderBySalaryDesc(departmentNames, pageable);
    
    List<Employee> list = pageResult.getContent();
    
    return list;
}
```
