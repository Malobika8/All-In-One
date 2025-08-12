## ✅ Step 9: Native Queries in Spring Data JPA

### 🔹 Why Native Queries?

Sometimes JPQL isn't enough — you might need:

* Complex joins or DB-specific functions
* Access to **views**, stored procedures
* Better performance using **SQL hints**

That’s when you use **native SQL** with Spring Data JPA.

#### Basic Native Query Example

```java
@Query(value = "SELECT * FROM employee WHERE salary > :sal", nativeQuery = true)
List<Employee> findHighEarners(@Param("sal") int salary);
```

#### Native SQL to DTO? Use `@SqlResultSetMapping`

JPQL can map directly to DTOs.
But native SQL **cannot** do it automatically — so you define a **result set mapping**.

---

# Write a native query to:

> ✅ Select only `id` and `name` of employees whose salary is greater than 90000
> ✅ Map result to a DTO:

```java
public class EmployeeNameDTO {
    private int id;
    private String name;

    public EmployeeNameDTO(int id, String name) {
        this.id = id;
        this.name = name;
    }

    // Getters and setters
}
```

### Your task:

* Define the DTO
* Define `@NamedNativeQuery` + `@SqlResultSetMapping` on the `Employee` entity
* Write repository method to fetch `EmployeeNameDTO`

### Sol:

```java
@Entity
@NamedNativeQuery(
    name = "Employee.findBySalary",
    query = "SELECT id, name FROM employee WHERE salary > 90000",
    resultSetMapping = "EmployeeNameDTOMapping"
)
@SqlResultSetMapping(
    name = "EmployeeNameDTOMapping",
    classes = @ConstructorResult(
        targetClass = org.test.EmployeeNameDTO.class,
        columns = {
            @ColumnResult(name = "id", type = Integer.class),
            @ColumnResult(name = "name", type = String.class)
        }
    )
)
public class Employee {
    @Id
    int id;
    String name;
    int salary;

    @ManyToOne
    @JoinColumn(name = "dep_id")
    Department department;
}
```
```java
@Query(nativeQuery = true, name = "Employee.findBySalary")
List<EmployeeNameDTO> findBySalary();
```

---

# Write a native query that:

> ✅ Retrieves all **departments**
> ✅ Along with the **number of employees in each department**
> ✅ Only include departments where the employee count is **greater than 3**
> ✅ Map the result to a DTO:

```java
public class DepartmentEmployeeCountDTO {
    private String departmentName;
    private Long count;

    public DepartmentEmployeeCountDTO(String departmentName, Long count) {
        this.departmentName = departmentName;
        this.count = count;
    }

    // Getters and setters
}
```

👉 Your task:

* Write the native SQL
* Add `@NamedNativeQuery` + `@SqlResultSetMapping`
* Write the repository method

### Sol:

```

@Query(name="Employee.findDepartmentAndEmployee", nativeQuery=true)
public List<DepartmentEmployeeCountDTO> findEmployeeAndDepartment();

public class DepartmentEmployeeCountDTO {
    private String departmentName;
    private Long count;

    public DepartmentEmployeeCountDTO(String departmentName, Long count) {
        this.departmentName = departmentName;
        this.count = count;
    }
    // Getters and setters
}

@Entity
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
@SqlResultSetMapping(
    name = "DepartmentEmployeeCountDTOMapping",
    classes = @ConstructorResult(
        targetClass = org.test.DepartmentEmployeeCountDTO,
        columns = {
            @ColumnResult(name="departmentName", type=String.class),
            @ColumnResult(name="count", type=Long.class)
        }
    )
    )
@NamedNativeQuery(
    name = "Employee.findDepartmentAndEmployee",
    query = "select d.departmentName, count(e) from employee e inner join department d on e.dep_id=d.id group by d.departmentName having count(e)>3",
    resultSetMapping = "DepartmentEmployeeCountDTOMapping"
    )
public class Employee{
    @Id
    int id;
    String name;
    int salary;
    
    @ManyToOne
    @JoinColumn(name = "dep_id")
    Department department;
}

@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class Department{
    @Id
    int id;
    String departmentName;
    
    @OneToMany(mappedBy="department")
    List<Employee> employee;
}
```




