# Understanding

| Feature          | Procedure                | Function                            |
| ---------------- | ------------------------ | ----------------------------------- |
| Returns a value  | ❌ cannot return directly | ✔ must return a value               |
| Used in SELECT   | ❌                        | ✔ allowed                           |
| Purpose          | Perform an action        | Perform calculation & return result |
| RETURN statement | Optional                 | Mandatory                           |

## PROCEDURE – Syntax

```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters...)
IS / AS
BEGIN
  -- logic
END;
```

To run a procedure:

```sql
BEGIN
  procedure_name(parameters...);
END;
/
```

---

## Question 1 — Create your first procedure

Create a procedure `say_hello` that:

* Takes **1 input parameter**: `p_name VARCHAR2`
* Prints:

  ```
  Hello <name>
  ```

Example output when name = `'Piyush'`:

```
Hello Piyush
```

### ->

```
CREATE OR REPLACE PROCEDURE say_hello(p_name IN VARCHAR2)
AS
BEGIN
  DBMS_OUTPUT.PUT_LINE('Hello ' || p_name);
END;
/

BEGIN
  say_hello('Piyush');
END;
/
```

---

## Question 2

Create a procedure `print_sum` that:

* Takes **two input numbers**: `p_num1`, `p_num2`
* Prints:

  ```
  Sum = <result>
  ```

Example:

```
Sum = 45
```

### ->

```
CREATE OR REPLACE PROCEDURE print_sum(p_num1 IN NUMBER, p_num2 IN NUMBER)
AS
  sum_val NUMBER;
BEGIN
  sum_val := p_num1 + p_num2;
  DBMS_OUTPUT.PUT_LINE('Sum = ' || sum_val);
END;
/

BEGIN
  print_sum(10, 35);
END;
/
```
