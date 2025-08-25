## 📘 What are Joins?

A **JOIN** lets you query data from **two or more tables** based on a related column (usually a key).

👉 Example:

* `students` table (student details)
* `courses` table (course details)

Instead of keeping all info in one big table, we **normalize** data into separate tables, then **join** when needed.

---

### Example Tables

#### 1. `students`

| student\_id | name  | age | course\_id |
| ----------- | ----- | --- | ---------- |
| 1           | Aditi | 22  | 101        |
| 2           | Raj   | 21  | 102        |
| 3           | Sneha | 23  | 103        |
| 4           | Aman  | 22  | 102        |
| 5           | Ravi  | 24  | 103        |

#### 2. `courses`

| course\_id | course\_name |
| ---------- | ------------ |
| 101        | Physics      |
| 102        | Math         |
| 103        | CS           |

---

## 📘 Types of Joins

1. **INNER JOIN** → returns rows where there’s a match in both tables.
2. **LEFT JOIN** → returns all rows from left table, and matched rows from right table.
3. **RIGHT JOIN** → returns all rows from right table, and matched rows from left table.
4. **FULL OUTER JOIN** → returns all rows from both tables (matched and unmatched).
5. **SELF JOIN** → joining a table with itself.

---

## 🔹 Example Query

**Get student names with their course names** (INNER JOIN):

```sql
SELECT s.name, c.course_name
FROM students s
INNER JOIN courses c
ON s.course_id = c.course_id;
```

👉 Output:

| name  | course\_name |
| ----- | ------------ |
| Aditi | Physics      |
| Raj   | Math         |
| Sneha | CS           |
| Aman  | Math         |
| Ravi  | CS           |

---

## 🔹 Practice Problems

Based on `students` and `courses` tables above:

1. Show each student’s name with their course name.
2. Show all students and their courses, but include students even if they don’t have a matching course (`LEFT JOIN`).
3. Show all courses and the students enrolled in them (`RIGHT JOIN`).
4. Show all students and all courses (even if no match) (`FULL OUTER JOIN`).

1. SELECT s.name, c.course_name 
FROM students s 
INNER JOIN courses c 
ON s.course_id = c.course_id;

2. SELECT s.name, c.course_name 
FROM students s 
LEFT JOIN courses c 
ON s.course_id = c.course_id;

3. SELECT s.name, c.course_name 
FROM students s 
RIGHT JOIN courses c 
ON s.course_id = c.course_id;

4. SELECT s.name, c.course_name 
FROM students s 
FULL OUTER JOIN courses c 
ON s.course_id = c.course_id;

---

## 🔹 Realistic JOIN Practice Problems

1. Show **all students with their course name** (include students who don’t have a course).
2. Show **all courses with their enrolled students** (include courses with no students).
3. Show the list of students who **don’t have a course assigned**.
4. Show the list of courses that **have no students enrolled**.
5. Show the **total number of students per course** (including courses with zero students).

1. SELECT s.name, c.course_name 
FROM students s 
LEFT JOIN courses c 
ON s.course_id = c.course_id;

2. SELECT c.course_name, s.name 
FROM courses c 
LEFT JOIN students s 
ON c.course_id = s.course_id;

3. SELECT s.name 
FROM students s 
LEFT JOIN courses c 
ON s.course_id = c.course_id 
WHERE c.course_id IS NULL;

4. SELECT c.course_name 
FROM courses c 
LEFT JOIN students s 
ON c.course_id = s.course_id 
WHERE s.student_id IS NULL;

5. SELECT c.course_name, COUNT(s.student_id) AS student_count
FROM courses c 
LEFT JOIN students s 
ON c.course_id = s.course_id 
GROUP BY c.course_name;

