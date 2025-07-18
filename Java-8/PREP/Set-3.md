# Calculate the total salary of all employees.

### Sol:

```
int total= list.stream()
        .map(emp->emp.getSalary())
        .reduce(0, (a,b)->a+b);
```
OR
```
int total = list.stream()
    .collect(Collectors.reducing(0, emp->emp.getSalary(), (a,b)->a+b));
```

---

# Find employee with max salary.

### Sol:

```
int total = list.stream()
        .map(emp->emp.getSalary())
        .max((s1,s2)->s1-s2).get();
```

---

# You are given the same List<Employee>.

Write a stream expression to:
- Find any employee whose salary > 30000
- Print their name if present
- Otherwise, print "No employee found"

### Sol:

#### Version using `ifPresent()`:

```java
list.stream()
    .filter(emp -> emp.getSalary() > 30000)
    .findAny()
    .ifPresent(emp -> System.out.println(emp.getName()));
```

If you also want a default message:

#### Version with `orElse()`:

```java
Employee result = list.stream()
    .filter(emp -> emp.getSalary() > 30000)
    .findAny()
    .orElse(null);

if (result != null) {
    System.out.println(result.getName());
} else {
    System.out.println("No employee found");
}
```

#### Or Using `Optional.ifPresentOrElse()` (Java 9+):

If you’re using Java 9 or higher:

```java
list.stream()
    .filter(emp -> emp.getSalary() > 30000)
    .findAny()
    .ifPresentOrElse(
        emp -> System.out.println(emp.getName()),
        () -> System.out.println("No employee found")
    );
```

---

# Find the first employee across all departments whose salary is greater than 40000, and print their name.

Use:
- flatMap() to flatten employees from all departments
- filter() to find salary > 40000
- findFirst() + Optional handling to print their name or "No high-salary employee found"

### Sol:

```
Optional<Employee> result = department.stream()
            .map(dep -> dep.getEmployees())
            .flatMap(emps->emps.stream())
            .filter(emp->emp.getSalary()>40000)
            .findFirst();
            
        if (result.isPresent()) {
            System.out.println(result.get().getName());
        } else {
            System.out.println("No high-salary employee found");
        }
```

---

# Got it! Let’s sharpen your **method reference skills** by converting some common lambdas into method references.

---

# Convert each lambda to a method reference

**1. Lambda:**

```java
list.stream()
    .map(s -> s.toUpperCase())
    .collect(Collectors.toList());
```

**2. Lambda:**

```java
list.stream()
    .filter(x -> x.isEmpty())
    .collect(Collectors.toList());
```

**3. Lambda:**

```java
list.stream()
    .forEach(x -> System.out.println(x));
```

**4. Lambda:**

```java
employees.stream()
    .map(emp -> emp.getName())
    .collect(Collectors.toList());
```

**5. Lambda:**

```java
list.stream()
    .sorted((a, b) -> a.compareTo(b))
    .collect(Collectors.toList());
```

### Sol:

```
list.stream()
    .map(String::toUpperCase)              // no parentheses
    .collect(Collectors.toList());

list.stream()
    .filter(String::isEmpty)               // no parentheses
    .collect(Collectors.toList());

list.stream()
    .forEach(System.out::println);         // correct

employees.stream()
    .map(Employee::getName)                // no parentheses
    .collect(Collectors.toList());

list.stream()
    .sorted(Integer::compareTo)            // correct
    .collect(Collectors.toList());
```

