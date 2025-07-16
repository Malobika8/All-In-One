# Task: 

- Write the **`Employee` entity** with:

  * `id`, `name`, `salary`
  * A `@ManyToOne` relationship with `Department`

- Write the `Department` entity class with:

  * `id`, `departmentName`
  * A `@OneToMany` list of `Employee`s mapped from the other side

### Sol:

```java
@Entity
@Getter
@Setter
@NoArgsConstructor
@AllArgsConstructor
public class Employee{
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

---

# Write a JPQL query to fetch each department’s name and the number of employees in that department.

### Sol:

```java
TypedQuery<DepartmentEmployeeDTO> tq = em.createQuery(
    "SELECT new com.example.dto.DepartmentEmployeeDTO(e.department.departmentName, COUNT(e)) " +
    "FROM Employee e " +
    "GROUP BY e.department.departmentName",
    DepartmentEmployeeDTO.class
);
```

---

# Write a JPQL query to fetch: All employees who work in the "HR" department

### Sol:

```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("pu");
EntityManager em = emf.createEntityManager();
TypedQuery<Employee> tq = em.createQuery("select e from Employee e where e.department.departmentName='HR'", Employee.class);
List<Employee> list = tq.getResultList();
```

---

# Write a JPQL query to: Fetch all department names and their average salaries, but only for departments where the average is more than 60,000

### Sol:

```java
EntityManagerFactory emf = Persistence.createEntityManagerFactory("pu");
EntityManager em = emf.createEntityManager();
TypedQuery<DepartmentSalaryDTO> tq = em.createQuery("select new com.test.DepartmentSalaryDTO(e.department.departmentName, AVG(e.salary)) from Employee e group by e.department.departmentName having AVG(e.salary)>60000", DepartmentSalaryDTO.class);
List<DepartmentSalaryDTO> list = tq.getResultList();
```

---

