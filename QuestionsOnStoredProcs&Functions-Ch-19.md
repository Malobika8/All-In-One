# Q1. Function for Bonus

Write a function `calculateBonus(salary DECIMAL(10,2), grade CHAR(1))` that:

* Adds **20% bonus** if grade = `'A'`
* Adds **10% bonus** if grade = `'B'`
* Otherwise no bonus
  Return the final amount (salary + bonus).

### Explanation:

```sql
DELIMITER $$

CREATE FUNCTION calculateBonus(salary DECIMAL(10,2), grade CHAR(1))
RETURNS DECIMAL(10,2)
DETERMINISTIC
BEGIN
    DECLARE finalSalary DECIMAL(10,2);

    SET finalSalary = salary;

    IF grade = 'A' THEN
        SET finalSalary = salary + (0.2 * salary);
    ELSEIF grade = 'B' THEN
        SET finalSalary = salary + (0.1 * salary);
    END IF;

    RETURN finalSalary;
END$$

DELIMITER ;
```

---

# Q2. Stored Procedure for Department Employees

Write a stored procedure `getEmployeesByDept(deptId INT)` that selects and returns all employees from the `employees` table who belong to the given department.

### Explanation:

```sql
DELIMITER $$

CREATE PROCEDURE getEmployeesByDept(IN deptId INT)
BEGIN
    SELECT * 
    FROM employees
    WHERE dept_id = deptId;
END$$

DELIMITER ;
```

To call it ->

```sql
CALL getEmployeesByDept(101);
```

---

# Q3. Function for Leap Year

Write a function `isLeapYear(y INT)` that returns:

* `1` if the year is a leap year
* `0` otherwise

### Explanation:

```sql
DELIMITER $$

CREATE FUNCTION isLeapYear(y INT)
RETURNS INT
DETERMINISTIC
BEGIN
    DECLARE result INT;

    IF (y % 400 = 0) THEN
        SET result = 1;
    ELSEIF (y % 100 = 0) THEN
        SET result = 0;
    ELSEIF (y % 4 = 0) THEN
        SET result = 1;
    ELSE
        SET result = 0;
    END IF;

    RETURN result;
END$$

DELIMITER ;
```

---

# Q4. Stored Procedure for Salary Hike

Write a stored procedure `hikeSalary(empId INT, hikePercent DECIMAL(5,2))` that:
* Increases the salary of the employee with `empId` by `hikePercent`.

### Explanation:

```sql
DELIMITER $$

CREATE PROCEDURE hikeSalary(IN empId INT, IN hikePercent DECIMAL(5,2))
BEGIN
    UPDATE employees
    SET salary = salary + (salary * (hikePercent / 100))
    WHERE emp_id = empId;
END$$

DELIMITER ;
```

to call ->

```sql
CALL hikeSalary(101, 10);  -- gives employee 101 a 10% hike
```

---

# Q5. Function with DETERMINISTIC

Write a function `circleArea(radius DECIMAL(10,2))` that:

* Returns the area of a circle (π \* r²).
* Mark it as `DETERMINISTIC`.

### Explanation:

```sql
DELIMITER $$

CREATE FUNCTION circleArea(radius DECIMAL(10,2))
RETURNS DECIMAL(18,4)
DETERMINISTIC
BEGIN
    RETURN PI() * radius * radius;
END$$

DELIMITER ;
```

to call ->

```sql
SELECT circleArea(10);
-- Output: 314.1590
```





