# What are the steps to connect a Java application to a database using JDBC? List all the steps in order and explain each briefly.

### Sol:

**JDBC Workflow:**

1. **Load the JDBC Driver** (optional in newer versions of JDBC, but still good to know):

   ```java
   Class.forName("com.mysql.cj.jdbc.Driver");
   ```

   > This step loads the database-specific driver class into memory.

2. **Establish the Connection**:

   ```java
   Connection connection = DriverManager.getConnection(
       "jdbc:mysql://localhost:3306/dbname", "username", "password");
   ```

   > This creates a session with the database.

3. **Create a Statement / PreparedStatement**:

   ```java
   Statement stmt = connection.createStatement();
   ```

   or

   ```java
   PreparedStatement pstmt = connection.prepareStatement("SELECT * FROM users WHERE id = ?");
   ```

4. **Execute SQL Queries**:

   ```java
   ResultSet rs = stmt.executeQuery("SELECT * FROM table1");
   while (rs.next()) {
       System.out.println(rs.getInt(1));
   }
   ```

5. **Close Resources**:

   ```java
   rs.close();
   stmt.close();
   connection.close();
   ```

   > Always close `ResultSet`, `Statement`, and `Connection` in reverse order of creation.

---

# Write a Java method to fetch and print all employee names from a table `employees` using JDBC. Assume the table has columns: `id (int)` and `name (varchar)`.

**Requirements:**

* Use `Connection`, `Statement`, and `ResultSet`.
* Print each employee's name.

### Sol:

```java
import java.sql.*;

public class Main {
    public static void main(String[] args) {
        try {
            Connection connection = getConnection();
            
            Statement statement = connection.createStatement();
            ResultSet rs = statement.executeQuery("SELECT * FROM employees");
            
            while (rs.next()) {
                System.out.println("id: " + rs.getInt(1) + " , name: " + rs.getString(2));
            }

            rs.close();
            statement.close();
            connection.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }

    public static Connection getConnection() throws Exception {
        Class.forName("com.mysql.cj.jdbc.Driver"); // use your DB driver

        String url = "jdbc:mysql://localhost:3306/your_db"; // Replace with your DB details
        String user = "root";
        String password = "your_password";

        return DriverManager.getConnection(url, user, password);
    }
}
```

---

# What is the difference between `Statement` and `PreparedStatement` in JDBC? Give real use cases and also tell me which one is better and why.

### Sol:

**Statement vs PreparedStatement**

**1. `Statement`:**

* Used for **static SQL queries** — where the query string doesn’t change dynamically.
* Example:

  ```java
  Statement stmt = connection.createStatement();
  ResultSet rs = stmt.executeQuery("SELECT * FROM users");
  ```

**2. `PreparedStatement`:**

* Used for **dynamic SQL queries** with input parameters.
* Provides **built-in protection against SQL injection**.
* Pre-compiles the query once and executes it multiple times with different values (better performance).
* Example:

  ```java
  PreparedStatement pstmt = connection.prepareStatement(
      "SELECT username FROM users WHERE password = ?");
  pstmt.setString(1, "mypassword");
  ResultSet rs = pstmt.executeQuery();
  ```

**3. SQL Injection Risk with `Statement`:**

* If you write:

  ```java
  String query = "SELECT * FROM users WHERE username = '" + userInput + "'";
  ```

  and input is `' OR '1'='1`, it becomes:

  ```sql
  SELECT * FROM users WHERE username = '' OR '1'='1'
  ```

  ➤ This bypasses authentication! 🛑

**4. Conclusion:**

* ✅ Use `PreparedStatement` for dynamic input.
* ✅ Use `Statement` only for simple, static queries with no input.

---

# Write a method to fetch all employees from `employees` table where department = ? Use `PreparedStatement`, and print `id`, `name`, and `department`.

Method signature:

```java
public static void printEmployeesByDept(String departmentName)
```

### Sol:

```java
import java.sql.*;

public class Main {

    public static void printEmployeesByDept(String departmentName) {
        Connection connection = null;
        PreparedStatement pstmt = null;
        ResultSet rs = null;

        try {
            connection = getConnection();

            String sql = "SELECT * FROM employees WHERE department = ?";
            pstmt = connection.prepareStatement(sql);
            pstmt.setString(1, departmentName);

            rs = pstmt.executeQuery();

            while (rs.next()) {
                System.out.println("Id: " + rs.getInt("id"));
                System.out.println("Name: " + rs.getString("name"));
                System.out.println("Department: " + rs.getString("department"));
                System.out.println("--------------------");
            }
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try { if (rs != null) rs.close(); } catch (Exception ignored) {}
            try { if (pstmt != null) pstmt.close(); } catch (Exception ignored) {}
            try { if (connection != null) connection.close(); } catch (Exception ignored) {}
        }
    }

    public static Connection getConnection() throws Exception {
        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/your_db";
        String username = "root";
        String password = "your_password";

        return DriverManager.getConnection(url, username, password);
    }
}
```

---

# What is SQL Injection and how does PreparedStatement prevent it?

### Sol:

**SQL Injection** is a **security vulnerability** that occurs when user input is directly embedded into an SQL query without validation or escaping.
This allows attackers to manipulate the query and execute unintended commands.

#### **Example using Statement (vulnerable):**

```java
String sql = "SELECT * FROM users WHERE username = '" + user + "' AND password = '" + pass + "'";
```

If attacker inputs:
`username = 'anything'`
`password = ' OR '1'='1'`
Then final SQL becomes:

```sql
SELECT * FROM users WHERE username = 'anything' AND password = '' OR '1'='1'
```

➤ Since `'1'='1'` is always true, the attacker **bypasses authentication**.

#### **How `PreparedStatement` prevents this:**

```java
PreparedStatement pstmt = connection.prepareStatement(
    "SELECT * FROM users WHERE username = ? AND password = ?");
pstmt.setString(1, user);
pstmt.setString(2, pass);
```

* Here, the values are **treated as parameters**, not part of the SQL logic.
* Even if attacker inputs `' OR '1'='1'`, it is passed as a **literal string**, **not executable SQL**.
* Hence, the structure of the query remains safe.

#### Tip:

* PreparedStatements also **cache and reuse** execution plans → improves performance for repeated queries.

---
