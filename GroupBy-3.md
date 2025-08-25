## 📘 What is `GROUP BY`?

* `GROUP BY` is used with **aggregate functions** (`COUNT`, `SUM`, `AVG`, `MIN`, `MAX`)
* It groups rows **based on column values**, and then applies the aggregate on each group.

👉 Think of it as:
“Group rows that have the same value in a column, then calculate something for each group.”

---

### Example: Our `students` table

| student\_id | name  | age | course  |
| ----------- | ----- | --- | ------- |
| 1           | Aditi | 22  | Physics |
| 2           | Raj   | 21  | Math    |
| 3           | Sneha | 23  | CS      |
| 4           | Aman  | 22  | Math    |
| 5           | Ravi  | 24  | CS      |

---

## 🔹 Basic `GROUP BY` Examples

### 1. Count students per course

```sql
SELECT course, COUNT(student_id) 
FROM students
GROUP BY course;
```

👉 Output:

| course  | count |
| ------- | ----- |
| Physics | 1     |
| Math    | 2     |
| CS      | 2     |

---

### 2. Average age per course

```sql
SELECT course, AVG(age) 
FROM students
GROUP BY course;
```

---

### 3. Maximum age per course

```sql
SELECT course, MAX(age) 
FROM students
GROUP BY course;
```

---

## 🔹 Practice Tasks

Write queries for:

1. Find the **number of students** in each course.
2. Find the **average age** of students in each course.
3. Find the **youngest student’s age** in each course.
4. Find the **oldest student’s age** in each course.


1. SELECT course, COUNT(student_id) 
FROM students 
GROUP BY course;

2. SELECT course, AVG(age) 
FROM students 
GROUP BY course;

3. SELECT course, MIN(age) 
FROM students 
GROUP BY course;

4. SELECT course, MAX(age) 
FROM students 
GROUP BY course;

## 🔹 Trickier `GROUP BY` Questions

1. Show each **course** with the **total sum of ages** of its students.
2. Show each **course** with the **number of students and average age**.
3. Show the **maximum and minimum age** together for each course.
4. Show the **course name along with the list of student count, average, min, and max age** (all in one query).


1. SELECT course, SUM(age) 
FROM students 
GROUP BY course;

2. SELECT course, COUNT(student_id), AVG(age) 
FROM students 
GROUP BY course;

3. SELECT course, MAX(age), MIN(age) 
FROM students 
GROUP BY course;

4. SELECT 
    course, 
    COUNT(student_id) AS student_count, 
    AVG(age) AS average_age, 
    MIN(age) AS youngest_age, 
    MAX(age) AS oldest_age
   FROM students
   GROUP BY course;

---

## Problems with having clause

1. Show courses that have **more than 1 student**.
2. Show courses where the **average age is greater than 22**.
3. Show courses where the **maximum age is less than 24**.
4. Show courses with **at least 2 students** and an **average age above 21**.

1. SELECT course 
FROM students 
GROUP BY course 
HAVING COUNT(student_id) > 1;

2. SELECT course 
FROM students 
GROUP BY course 
HAVING AVG(age) > 22;

3. SELECT course 
FROM students 
GROUP BY course 
HAVING MAX(age) < 24;

4. SELECT course 
FROM students 
GROUP BY course 
HAVING COUNT(student_id) >= 2 
AND AVG(age) > 21;




