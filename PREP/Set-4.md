## **TRY-WITH-RESOURCES in JDBC**

# What is try-with-resources in JDBC and why should you use it? Write a JDBC snippet using try-with-resources to fetch all employees.

### Your Task:

1. Explain **what try-with-resources does**.
2. Then write this method:

```java
public static void fetchAllEmployees()
```

It should:

* Use `try-with-resources`
* Connect to DB
* Query `SELECT * FROM employees`
* Print `id` and `name`

### Sol:

> In JDBC, **try-with-resources** is a feature introduced in Java 7 that allows us to **automatically close resources** like `Connection`, `Statement`, and `ResultSet`.
> Any object that implements `AutoCloseable` (which all JDBC resources do) will be **closed automatically** at the end of the `try` block, even if an exception occurs.
> This eliminates the need for an explicit `finally` block and prevents resource leaks.

```java
import java.sql.*;

public class Main {

    public static void fetchAllEmployees() {
        String sql = "SELECT * FROM employees";

        try (
            Connection connection = getConnection();
            Statement stmt = connection.createStatement();
            ResultSet rs = stmt.executeQuery(sql)
        ) {
            while (rs.next()) {
                System.out.println("Id: " + rs.getInt("id") + ", Name: " + rs.getString("name"));
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static Connection getConnection() throws Exception {
        Class.forName("com.mysql.cj.jdbc.Driver");
        return DriverManager.getConnection(
            "jdbc:mysql://localhost:3306/your_db", "root", "your_password");
    }
}
```

---

# What does `executeQuery()` return?

### Sol:

It returns a ResultSet containing data from a SELECT statement.

---

# What does `executeUpdate()` return?

### Sol:

It returns an int representing the number of rows affected by an INSERT, UPDATE, or DELETE.

---

# Can you use `PreparedStatement` to execute DDL statements (like CREATE)?

### Sol:

You can use PreparedStatement for DDL (like CREATE TABLE) but you'll typically use execute() since executeUpdate() or executeQuery() are not ideal for non-DML/SELECT.

---

# What is connection pooling and why is it useful?

### Sol:

Connection Pooling is a technique where a pool of database connections is maintained and reused instead of creating new connections for every request.
This improves performance by reducing the overhead of creating/closing DB connections frequently.

In real apps, tools like HikariCP, Apache DBCP, or C3P0 are used.

---

# Suppose you want to call a **stored procedure** named `raiseSalary` that takes an `employeeId` and `increment` as input parameters, and returns the updated salary as output. Can you write a JDBC code snippet using `CallableStatement`?

### Sol:

1. **Creating a stored procedure** syntax depends on the DB (Oracle, MySQL, PostgreSQL, etc.), but the idea is:

   * `IN` parameters (inputs).
   * `OUT` parameters (outputs).

   Example (MySQL style):

   ```sql
   CREATE PROCEDURE raiseSalary (
       IN empId INT,
       IN inc INT,
       OUT updated_salary INT
   )
   BEGIN
       UPDATE employee 
       SET salary = salary + inc
       WHERE id = empId;

       SELECT salary INTO updated_salary 
       FROM employee 
       WHERE id = empId;
   END;
   ```
2. **CallableStatement in JDBC**

   * Use `connection.prepareCall()`.
   * For OUT params, you must **register** them before executing.
   * Execution returns `true/false`, not the OUT value directly. You fetch OUT params separately.

```java
CallableStatement cs = connection.prepareCall("{call raiseSalary(?, ?, ?)}");

// Set IN parameters
cs.setInt(1, 101);    // employeeId
cs.setInt(2, 5000);   // increment

// Register OUT parameter
cs.registerOutParameter(3, java.sql.Types.INTEGER);

// Execute
cs.execute();

// Get OUT parameter value
int updatedSalary = cs.getInt(3);
System.out.println("Updated Salary: " + updatedSalary);

cs.close();
```
