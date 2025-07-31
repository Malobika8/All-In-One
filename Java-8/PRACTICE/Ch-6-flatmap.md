## 🧠 `flatMap()` in Java 8 Streams**

`flatMap()` is used to **flatten a stream of streams** into a **single stream of elements**.

---

### 📌 **Why not just use `map()`?**

* `map()` returns **`Stream<Stream<T>>`** if you're mapping to a stream.
* `flatMap()` **flattens** that into a single `Stream<T>`.

---

### 🧾 Real-world use cases:

* Flattening a list of lists
* Splitting strings into words
* Flattening nested data structures (like `List<List<String>>`)

---

### 📘 Example: Using `map()` vs `flatMap()`

```java
List<String> words = Arrays.asList("java", "stream");

words.stream()
     .map(word -> word.split(""))          // Stream<String[]>
     .forEach(arr -> System.out.println(Arrays.toString(arr)));

// Using flatMap
words.stream()
     .map(word -> word.split(""))          // Stream<String[]>
     .flatMap(Arrays::stream)              // Stream<String>
     .forEach(System.out::println);
```

---

### 💡 Rule of thumb:

> Use `flatMap()` when each element maps to a **stream** and you want a **flattened result**.

---

### 💻 **flatMap – Question 1: Flatten a List of Lists**

#### Given:

```java
List<List<String>> names = Arrays.asList(
    Arrays.asList("Alice", "Bob"),
    Arrays.asList("Charlie", "David"),
    Arrays.asList("Eva")
);
```

#### 🧠 Task:

* Flatten this into a single `List<String>`
* Print each name

---

### 💻 **flatMap – Question 2: Split Sentences into Words**

#### Given:

```java
List<String> sentences = Arrays.asList(
    "Java is awesome",
    "Streams are powerful",
    "flatMap is useful"
);
```

#### 🧠 Task:

* Split each sentence into words
* Flatten the result
* Print all words individually

---

### 💻 **flatMap – Question 3: Unique Characters in Words**

#### Given:

```java
List<String> words = Arrays.asList("java", "stream", "code");
```

#### 🧠 Task:

* Split each word into characters
* Flatten all characters
* Remove duplicates using `distinct()`
* Collect and print the final `List<String>`

🧾 Expected Output:

```
[j, a, v, s, t, r, e, m, c, o, d]
```

---

## 💻 **Final Java 8 Streams Misc Challenge – "Course Enrollment Report"**

### 👩‍🎓 Given:

```java
class Student {
    String name;
    List<String> courses;

    Student(String name, List<String> courses) {
        this.name = name;
        this.courses = courses;
    }

    public String getName() { return name; }
    public List<String> getCourses() { return courses; }
}

List<Student> students = Arrays.asList(
    new Student("Alice", Arrays.asList("Java", "Spring", "SQL")),
    new Student("Bob", Arrays.asList("Java", "Python")),
    new Student("Charlie", Arrays.asList("Spring", "MongoDB")),
    new Student("David", Arrays.asList("Java", "SQL", "Python"))
);
```

---

### 🧠 Tasks:

You have to use `flatMap`, `Collectors`, and everything you've practiced to answer these:

---

### ✅ Task 1:

Print a **unique list of all courses** offered by the students (sorted alphabetically).

**Expected:**

```
[Java, MongoDB, Python, SQL, Spring]
```

---

### ✅ Task 2:

Build a `Map<String, Long>` that tells how many students are enrolled in each course.

**Expected:**

```
Java=3, Spring=2, SQL=2, Python=2, MongoDB=1
```

---

## 💻 **Bonus Challenge: Course → Comma-Separated Student Names**

### 👩‍🎓 Given (same `Student` list):

```java
List<Student> students = Arrays.asList(
    new Student("Alice", Arrays.asList("Java", "Spring", "SQL")),
    new Student("Bob", Arrays.asList("Java", "Python")),
    new Student("Charlie", Arrays.asList("Spring", "MongoDB")),
    new Student("David", Arrays.asList("Java", "SQL", "Python"))
);
```

---

### 🧠 Task:

✅ Create a `Map<String, String>` where:

* **Key** = course name
* **Value** = comma-separated names of students enrolled in that course

---

### 🧾 Sample Output:

```
Java = Alice, Bob, David  
Spring = Alice, Charlie  
SQL = Alice, David  
Python = Bob, David  
MongoDB = Charlie
```

---

**Hint**: You’ll need:

* `flatMap()` to flatten students by course
* `Collectors.groupingBy(...)`
* `Collectors.mapping(..., joining(","))`

```
Map<String, List<String>> map = students.stream()
        .flatMap(stu->stu.getCourses().stream().map(c->new String[]{
                stu.getName(),c}))
        .collect(Collectors.groupingBy(strArr->strArr[0], Collectors.mapping(strArr->strArr[1], Collectors.toList())));
        
        System.out.println(map);
```

