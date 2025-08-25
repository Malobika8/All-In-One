## 📘 Aggregate Functions in SQL

1. **COUNT()** → counts rows
2. **SUM()** → adds values
3. **AVG()** → average
4. **MIN()** → minimum
5. **MAX()** → maximum

---

### Example Table (`students`)

| student\_id | name  | age | course  |
| ----------- | ----- | --- | ------- |
| 1           | Aditi | 22  | Physics |
| 2           | Raj   | 21  | Math    |
| 3           | Sneha | 23  | CS      |
| 4           | Aman  | 22  | Math    |
| 5           | Ravi  | 24  | CS      |

---

## 🔹 Queries to Practice

Write SQL for these:

1. Count how many students are in the table.
2. Find the **average age** of students.
3. Get the **minimum age** of students.
4. Get the **maximum age** of students.
5. Count how many students are enrolled in **CS**.
6. Find the **average age of students in Math**.

---

- SELECT COUNT(student_id) FROM students;
- SELECT AVG(age) FROM students;
- SELECT MIN(age) FROM students;
- SELECT MAX(age) FROM students;
- SELECT COUNT(student_id) FROM students WHERE course = 'CS';
- SELECT AVG(age) FROM students WHERE course = 'Math';


