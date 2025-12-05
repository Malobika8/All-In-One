# PL/SQL Stage 1 — What is PL/SQL?

SQL → Used only to query and manipulate data.

PL/SQL → SQL + Programming features
Meaning: It adds programming capabilities like variables, loops, conditions, procedures, functions, triggers, etc.

Think of PL/SQL as:

> “A programming language that runs inside Oracle Database.”

## Structure of a PL/SQL Block (Fundamental)

Every PL/SQL block has 3 parts:

```plsql
DECLARE        -- (Optional) define variables
BEGIN          -- (Mandatory) write logic
  -- statements;
EXCEPTION      -- (Optional) handle errors
  -- error logic;
END;
/
```

The `/` tells Oracle to execute the block.

---

### ✔ Example 1 — The smallest PL/SQL program

```plsql
BEGIN
  DBMS_OUTPUT.PUT_LINE('Hello PL/SQL');
END;
/
```

Output:

```
Hello PL/SQL
```

---

## Declaring and using variables

Syntax:

```plsql
DECLARE
  variable_name datatype [:= initial_value];
BEGIN
  -- logic
END;
/
```

### ✔ Example with variables

```plsql
DECLARE
  emp_name VARCHAR2(30) := 'John';
  emp_salary NUMBER := 50000;
BEGIN
  DBMS_OUTPUT.PUT_LINE('Employee: ' || emp_name);
  DBMS_OUTPUT.PUT_LINE('Salary: ' || emp_salary);
END;
/
```

Expected Output:

```
Employee: John
Salary: 50000
```

### Create a block with:

* A variable `p_name` (VARCHAR2)
* A variable `p_age` (NUMBER)
* Set values in the variable and print them using DBMS_OUTPUT.

Sample format you should print:

```
Name: <value>
Age: <value>
```

```
DECLARE
  p_name VARCHAR2(20) := 'piyush';
  p_age NUMBER := 22;
BEGIN
  DBMS_OUTPUT.PUT_LINE('name: ' || p_name);
  DBMS_OUTPUT.PUT_LINE('age: ' || p_age);
END;
/
```

### Write a PL/SQL block that:

* Declares a number variable `score` with value `85`
* If score is **>= 90**, print `"Grade: A"`
* Else if score is **>= 75**, print `"Grade: B"`
* Else print `"Grade: C"`

📌 Use `IF / ELSIF / ELSE`
📌 Print using `DBMS_OUTPUT.PUT_LINE`

```
DECLARE
  score NUMBER := 85;
BEGIN
  IF score >= 90 THEN
    DBMS_OUTPUT.PUT_LINE('Grade: A');
  ELSIF score >= 75 THEN
    DBMS_OUTPUT.PUT_LINE('Grade: B');
  ELSE
    DBMS_OUTPUT.PUT_LINE('Grade: C');
  END IF;
END;
/
```

### Good attempt — logic idea is right 👏
But there are **3 mistakes**:

---

### ❗ Mistakes

| Mistake                                     | Fix                              |
| ------------------------------------------- | -------------------------------- |
| Missing `ELSIF` keyword                     | `ELSE IF` is not valid in PL/SQL |
| Second condition wrongly uses `>= 90` again | Should be `>= 75`                |
| Missing `THEN` after conditions             | Required                         |
| Missing `/` on new line after END;          | Needed to run block              |

---

### 🔧 Corrected version (for learning)

```sql
DECLARE
  score NUMBER := 85;
BEGIN
  IF score >= 90 THEN
    DBMS_OUTPUT.PUT_LINE('Grade: A');
  ELSIF score >= 75 THEN
    DBMS_OUTPUT.PUT_LINE('Grade: B');
  ELSE
    DBMS_OUTPUT.PUT_LINE('Grade: C');
  END IF;
END;
/
```

---

### Write a PL/SQL block that:

* Declares a variable `marks := 40`
* If marks is **>= 35** ➜ print `"Result: PASS"`
* If marks is **>= 75** ➜ also print `"Distinction"`
* Else print `"Result: FAIL"`

❗ Note: Distinction should print **only if PASS** and **>= 75**

```
DECLARE
  marks NUMBER := 40;
BEGIN
  IF marks >= 35 THEN
    DBMS_OUTPUT.PUT_LINE('Result: PASS');
    IF marks >= 75 THEN
      DBMS_OUTPUT.PUT_LINE('Distinction');
    END IF;
  ELSE
    DBMS_OUTPUT.PUT_LINE('Result: FAIL');
  END IF;
END;
/
```

---

### 


You're almost there — very good nested IF logic 👏
Just **one small syntax mistake** is stopping execution.

---

### ❗ Mistake

```
if marks >= 75) then
                ↑ extra closing parenthesis
```

Also, PL/SQL keywords should be uppercase for readability (not mandatory, just good practice).

---

### ✔ Corrected version

```sql
DECLARE
  marks NUMBER := 40;
BEGIN
  IF marks >= 35 THEN
    DBMS_OUTPUT.PUT_LINE('Result: PASS');
    IF marks >= 75 THEN
      DBMS_OUTPUT.PUT_LINE('Distinction');
    END IF;
  ELSE
    DBMS_OUTPUT.PUT_LINE('Result: FAIL');
  END IF;
END;
/
```

---

### Write a PL/SQL block that prints numbers from **1 to 5** using a `WHILE LOOP`.

Output must be:

```
1
2
3
4
5
```

```
DECLARE
  num NUMBER := 1;
BEGIN
  WHILE num <= 5 LOOP
    DBMS_OUTPUT.PUT_LINE(num);
    num := num + 1;
  END LOOP;
END;
/
```
---

### Write a PL/SQL block using a **FOR LOOP** to print:

```
Table of 6
6 x 1 = 6
6 x 2 = 12
6 x 3 = 18
6 x 4 = 24
6 x 5 = 30
```

Requirements:

* Use `FOR i IN 1..5 LOOP`
* Use multiplication
* Use `DBMS_OUTPUT.PUT_LINE`

```
BEGIN
  DBMS_OUTPUT.PUT_LINE('Table of 6');
  FOR i IN 1..5 LOOP
    DBMS_OUTPUT.PUT_LINE('6 X ' || i || ' = ' || (6 * i));
  END LOOP;
END;
/
```

---

### Write a PL/SQL block that:

* Loops from **1 to 10**
* Print only **even numbers**
* Output format should be:

```
2
4
6
8
10
```

```
BEGIN
  FOR num IN 1..10 LOOP
    IF num % 2 = 0 THEN
      DBMS_OUTPUT.PUT_LINE(num);
    END IF;
  END LOOP;
END;
/
```

---

### Write a PL/SQL block that:

* Uses a **FOR loop from 1 to 10**
* Sum all numbers (1 + 2 + ... + 10)
* After the loop, print:

```
Total Sum = 55
```

Hints:

* Use a variable `sum_num NUMBER := 0;`
* Add inside loop: `sum_num := sum_num + i;`

```
DECLARE
  sum_num NUMBER := 0;
  num NUMBER;
BEGIN
  FOR num IN 1..10 LOOP
    sum_num := sum_num + num;
  END LOOP;
  DBMS_OUTPUT.PUT_LINE('Total sum = ' || sum_num);
END;
/
```
---

### Write a PL/SQL block that:

* Declares a number `n := 5`
* Calculates **factorial of n**
* Print output in this format:

```
Factorial of 5 = 120
```

Hints:

* Use a loop
* Initialize `fact := 1`
* Multiply inside loop:

  ```
  fact := fact * i;
  ```

```
DECLARE
  n NUMBER := 5;
  fact NUMBER := 1;
BEGIN
  WHILE n >= 1 LOOP
    fact := fact * n;
    n := n - 1;            -- decrease to avoid infinite loop
  END LOOP;

  DBMS_OUTPUT.PUT_LINE('Factorial of 5 = ' || fact);
END;
/
```
