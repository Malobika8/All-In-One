# Use `map()` to Transform Object Fields

You now have a list of `Employee` objects:

```java
class Employee {
    String name;
    int salary;

    Employee(String name, int salary) {
        this.name = name;
        this.salary = salary;
    }

    public String getName() { return name; }
    public int getSalary() { return salary; }
}
```

Now the problem:

> Given a `List<Employee>`, write a stream operation to:
>
> * Filter employees with salary > 30000
> * Return their **names** in a List

### Sol:

```
List<Employee> list = new ArrayList<>();
        Employee emp1 = new Employee("pika", 30000);
        Employee emp2 = new Employee("lama", 40000);
        
        list.add(emp1);
        list.add(emp2);
        
        List<String> names = list.stream()
            .filter(emp -> emp.getSalary()>30000)
            .map(emp -> emp.getName())
            .collect(Collectors.toList());
            
        System.out.println(names);
```

---

# Combine filter(), map(), and collect() to a Map
You’re given a list of Employee objects.

- Filter employees with salary > 25000
- Collect them into a Map<String, Integer> where:
  - key = employee name
  - value = salary

### Sol:

```java
List<Employee> list = new ArrayList<>();
        Employee emp1 = new Employee("pika", 30000);
        Employee emp2 = new Employee("lama", 40000);
        
        list.add(emp1);
        list.add(emp2);
        
      Map<String, Integer> mapEmp = list.stream()
            .filter(emp -> emp.getSalary()>25000)
            .collect(Collectors.toMap(emp->emp.getName(), emp->emp.getSalary()));
            
        mapEmp.entrySet()
            .forEach(entry -> System.out.println(entry.getKey() + " , " + entry.getValue()));
```

---

# Coding Problem:

You are given:

```java
List<Employee> list = Arrays.asList(
    new Employee("pika", 30000),
    new Employee("lama", 40000),
    new Employee("arun", 25000),
    new Employee("john", 35000)
);
```

Write a Stream expression to:
  * Filter employees with salary > 25000
  * Extract their names
  * Sort the names alphabetically
  * Collect them into a `List<String>`

### Sol:

```java
List<String> finalList = list.stream()
            .filter(emp -> emp.getSalary()>25000)
            .map(emp -> emp.getName())
            .sorted()
            .collect(Collectors.toList());
        
        System.out.println(finalList);
```

---

# Coding Problem:

You are given a list of `Employee` where each employee has a `name`, `salary`, and a `department`.

```java

class Employee {
    String name;
    int salary;
    String department;

    Employee(String name, int salary, String department) {
        this.name = name;
        this.salary = salary;
        this.department = department;
    }

    public String getName() { return name; }
    public int getSalary() { return salary; }
    public int getDepartment() { return department; }
}
```

> Group the employees by department using Streams and return a `Map<String, List<Employee>>`
> (i.e., department → list of employees in that department)

### Sol:

Collectors.groupingBy(): returns a Map<K, List<V>>

```java
List<Employee> list = Arrays.asList(
        new Employee("pika", 30000, "hr"),
        new Employee("lama", 40000, "it"),
        new Employee("arun", 25000, "it"),
        new Employee("john", 35000, "hr")
        );

        Map<String, List<Employee>> finalMap = list.stream()
            .collect(Collectors.groupingBy(emp->emp.getDepartment()));
        
        System.out.println(finalMap);
```

---

# What if we want to have Map<String, List<String>)?

### Sol:

```java
List<Employee> list = Arrays.asList(
        new Employee("pika", 30000, "hr"),
        new Employee("lama", 40000, "it"),
        new Employee("arun", 25000, "it"),
        new Employee("john", 35000, "hr")
        );

        Map<String, List<String>> finalMap = list.stream()
            .collect(Collectors.groupingBy(emp->emp.getDepartment(), Collectors.mapping(emp->emp.getName(), Collectors.toList())));
        
        System.out.println(finalMap);
```

---

# Coding Problem:

You are given this list:

```java
List<Employee> list = Arrays.asList(
    new Employee("pika", 30000, "hr"),
    new Employee("lama", 40000, "it"),
    new Employee("arun", 25000, "it"),
    new Employee("john", 35000, "hr"),
    new Employee("ankit", 27000, "finance")
);
```

> Write a stream to partition employees into two groups:
  - **Key `true`** → salary > 30000
  - **Key `false`** → salary <= 30000
  - Return:

  ```java
  Map<Boolean, List<Employee>>
  ```

### Sol:

```java
Map<Boolean, List<Employee>> finalList = list.stream()
        .collect(Collectors.partitioningBy(emp->emp.getSalary()>30000));
        
System.out.println(finalList);
```















