`Collectors.groupingBy()` allows you to group stream elements based on a **classifier function** (e.g., by age, by category, by status).

It returns a `Map<K, List<V>>` — grouping values into a list by key.

---

### 📌 **Basic Syntax:**

```java
Map<Key, List<Value>> grouped = list.stream()
    .collect(Collectors.groupingBy(item -> classifierFunction));
```

---

### 🔧 **Example: Group Words by Length**

```java
List<String> words = Arrays.asList("apple", "banana", "pear", "fig");

Map<Integer, List<String>> groupedByLength = words.stream()
    .collect(Collectors.groupingBy(word -> word.length()));
```

🧾 Output:

```java
{
  3 = [fig],
  4 = [pear],
  5 = [apple],
  6 = [banana]
}
```

---

# Questions

### 💻 **Question 1: Group Students by Score Range (Pass/Fail)**

#### Given:

```java
class Student {
    String name;
    int score;

    Student(String name, int score) {
        this.name = name;
        this.score = score;
    }

    public String getName() { return name; }
    public int getScore() { return score; }
}

List<Student> students = Arrays.asList(
    new Student("Alice", 82),
    new Student("Bob", 67),
    new Student("Charlie", 90),
    new Student("David", 45),
    new Student("Eva", 75)
);
```

---

#### 🧠 Task:

* Group students as `"PASS"` if score ≥ 60 and `"FAIL"` otherwise
* Use `Collectors.groupingBy(...)`
* Print the grouped map

✅ **Perfectly done!**
You've implemented `Collectors.groupingBy()` with conditional grouping logic correctly.

✔️ Used:

* A **classifier function** that returns `"PASS"` or `"FAIL"`
* The result is a `Map<String, List<Student>>`
* Printed the grouped map directly

---

### ✍️ **Notes Recap: Grouping by Conditional Key**

```java
Map<String, List<Student>> result = students.stream()
    .collect(Collectors.groupingBy(student -> {
        if (student.getScore() >= 60) return "PASS";
        else return "FAIL";
    }));
```

🧾 Sample Output (map structure):

```java
{
  PASS=[Student@1a, Student@2b, Student@3c],
  FAIL=[Student@4d]
}
```

---

### 💻 **Question 2: Group Students by Score Band (e.g. "90+", "80-89", "Below 80")**

#### Task:

Group students into 3 buckets:

* `"90+"` for scores ≥ 90
* `"80-89"` for scores between 80–89
* `"Below 80"` for scores < 80

Use `Collectors.groupingBy()`
Print the result.

✅ **Excellent work!**
You've used `Collectors.groupingBy()` with multi-branch conditions to group students into score bands — and also iterated the map to print the groups clearly.

---

### ✍️ **Notes Recap: Grouping by Score Bands using `Collectors.groupingBy()`**

```java
Map<String, List<Student>> map = students.stream()
    .collect(Collectors.groupingBy(student -> {
        if (student.getScore() >= 90)
            return "90";
        else if (student.getScore() >= 80)
            return "80-89";
        else
            return "below 80";
    }));

map.entrySet().forEach(entry -> 
    System.out.println(entry.getKey() + ": " + entry.getValue()));
```

💡 The `entrySet()` + `forEach()` is a great way to print map content, especially when you're grouping.

---

🧾 **Sample Output:**

```
80-89: [Student{name='Alice', score=82}, Student{name='Eva', score=75}]
90: [Student{name='Charlie', score=90}]
below 80: [Student{name='Bob', score=67}, Student{name='David', score=45}]
```

💡 Override `toString()` in `Student` class for pretty output.

---

### 💻 **Question 3: Group Students by Score Range and Collect Only Names**

Enhance previous logic to:

* Keep same score bands: `"90"`, `"80-89"`, `"below 80"`
* Instead of collecting full `Student` objects, collect only **names**

So final map is `Map<String, List<String>>`

```

Map<String, List<String>> map = new HashMap<>();
        map = students.stream()
                .collect(Collectors.groupingBy(student -> {
                    if(student.getScore()>=90)
                        return "90";
                    else if(student.getScore()>=80)
                        return "80-89";
                    else
                        return "below 80";
                }, Collectors.mapping(student -> student.getName(), Collectors.toList())));

        map.entrySet().stream()
                .forEach(entry -> System.out.println(entry.getKey() + ": " + entry.getValue()));

```

---

### 💻 **Count Students Per Grade Band**

#### Given:

Same `Student` class and list:

```java
List<Student> students = Arrays.asList(
    new Student("Alice", 82),
    new Student("Bob", 67),
    new Student("Charlie", 90),
    new Student("David", 45),
    new Student("Eva", 75),
    new Student("Frank", 67),
    new Student("Grace", 90)
);
```

---

### 🧠 Task:

1. Group students into **grade bands**:

   * `"90+"` for scores ≥ 90
   * `"80-89"` for 80 to 89
   * `"60-79"` for 60 to 79
   * `"Below 60"` for < 60
2. Count how many students fall into each band.
3. Final result should be: `Map<String, Long>`
4. Print the map.

🧾 Example Output:

```
90+: 2
80-89: 1
60-79: 3
Below 60: 1
```
### ✅ What's Next in Collectors Practice:

1. `Collectors.toMap()`
2. `Collectors.joining()`
3. `Collectors.summarizingInt()`
4. `Collectors.partitioningBy()`
5. Nested collectors (e.g., `groupingBy + mapping`)

---

### 💻 **Collectors Practice – Question 1: Use `Collectors.toMap()`**

#### Given:

```java
List<Student> students = Arrays.asList(
    new Student("Alice", 82),
    new Student("Bob", 67),
    new Student("Charlie", 90)
);
```

#### 🧠 Task:

* Convert this list into a `Map<String, Integer>`
  where **key = student name**, and **value = student score**

**Use `Collectors.toMap()`**, and then print the map.

---

### 💻 **Collectors Practice – Question 2: Use `Collectors.joining()`**

#### Given:

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie");
```

#### 🧠 Task:

* Use streams to join all names into a **single string**:

  * separated by `, `
  * enclosed with `[` and `]`

**Expected Output:**

```
[Alice, Bob, Charlie]
```

Use `Collectors.joining()` for this.

---

### 💻 **Collectors Practice – Question 3: Use `Collectors.summarizingInt()`**

#### Given:

```java
List<Student> students = Arrays.asList(
    new Student("Alice", 82),
    new Student("Bob", 67),
    new Student("Charlie", 90),
    new Student("David", 45)
);
```

#### 🧠 Task:

Use `Collectors.summarizingInt()` to:

* Calculate and print:

  * count
  * sum
  * min
  * max
  * average

All from **student scores**.

```
List<Student> students = Arrays.asList(
                new Student("Alice", 82),
                new Student("Bob", 67),
                new Student("Charlie", 90),
                new Student("David", 45)
        );

        IntSummaryStatistics summaryStatistics = students.stream()
                .collect(Collectors.summarizingInt(student -> student.getScore()));

        System.out.println(summaryStatistics.getCount());
        System.out.println(summaryStatistics.getMax());
        System.out.println(summaryStatistics.getAverage());
        System.out.println(summaryStatistics.getMin());
        System.out.println(summaryStatistics.getSum());
```

---

### 💻 **Collectors Practice – Question 4: Use `Collectors.partitioningBy()`**

#### Given:

Same `students` list.

#### 🧠 Task:

* Use `partitioningBy()` to divide students into **two groups**:
  * Key = `true` for scores ≥ 60 (passed)
  * Key = `false` for scores < 60 (failed)
* Final map should be: `Map<Boolean, List<Student>>`
* Print the result

```
Map<Boolean, List<Student>> map = students.stream()
                .collect(Collectors.partitioningBy(student -> student.getScore()>=60));

        System.out.println(map);
```

---

Awesome! Let’s test all your **Collectors mastery** in one powerful mini-challenge.

---

### 💻 **Collectors Mini-Challenge: Employee Department Summary**

#### 👨‍💼 Given:

```java
class Employee {
    String name;
    String department;
    int salary;

    Employee(String name, String department, int salary) {
        this.name = name;
        this.department = department;
        this.salary = salary;
    }

    public String getName() { return name; }
    public String getDepartment() { return department; }
    public int getSalary() { return salary; }
}

List<Employee> employees = Arrays.asList(
    new Employee("Alice", "HR", 40000),
    new Employee("Bob", "Engineering", 70000),
    new Employee("Charlie", "HR", 42000),
    new Employee("David", "Engineering", 80000),
    new Employee("Eva", "Sales", 50000),
    new Employee("Frank", "Sales", 45000)
);
```

---

## 🧠 Final Task:

1. **Group employees by department**
2. For each department:
   * Collect a list of employee names
   * Find the **average salary**
3. Print the final results like this:

```
HR:
  Employees: [Alice, Charlie]
  Average Salary: 41000.0

Engineering:
  Employees: [Bob, David]
  Average Salary: 75000.0

Sales:
  Employees: [Eva, Frank]
  Average Salary: 47500.0
```

---

✅ Use:

* `Collectors.groupingBy(...)`
* `Collectors.mapping(...)`
* `Collectors.averagingInt(...)`


