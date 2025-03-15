# JDBC

## How does it work?

### **How the Selected Driver Provides Implementation**

JDBC itself is just a specification. It defines a set of **interfaces** and **APIs** (like `java.sql.Driver`, `Connection`, `Statement`, `ResultSet`, etc.) but does not provide the actual implementations. The implementations are provided by **database vendors** through their respective JDBC drivers.

Here's how it works step-by-step:

---

### **1. JDBC Specification and Interfaces**
JDBC provides a standardized way for Java applications to interact with databases. It defines interfaces like:
- `java.sql.Driver`
- `java.sql.Connection`
- `java.sql.Statement`
- `java.sql.PreparedStatement`
- `java.sql.ResultSet`

These interfaces specify the methods and behaviors required for database communication but do not contain any implementation.

---

### **2. Database-Specific JDBC Drivers**
Database vendors (like Oracle, MySQL, PostgreSQL) provide **JDBC driver implementations**. These drivers:
- Implement the `java.sql.Driver` interface.
- Provide the actual logic for communicating with the database server.

For example:
- The **MySQL JDBC driver** (`com.mysql.cj.jdbc.Driver`) implements all the necessary logic to interact with a MySQL database.
- The **Oracle JDBC driver** (`oracle.jdbc.OracleDriver`) implements the same interfaces but with Oracle-specific logic.

---

### **3. How Drivers Are Selected and Used**
When your application requests a database connection, the following happens:

#### **Step 1: Driver Registration**
- The database driver must be registered with the `DriverManager`.
- This can be done either:
  1. **Manually**: Using `DriverManager.registerDriver(new com.mysql.cj.jdbc.Driver());`.
  2. **Automatically**: Modern drivers include a `META-INF/services/java.sql.Driver` file. This file contains the driver class name, and the Java Service Provider Interface (SPI) mechanism automatically loads it.

#### **Step 2: Connection Request**
- You call `DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "user", "password")`.
- The `DriverManager` iterates through the list of registered drivers and selects the one that matches the URL prefix (`jdbc:mysql` in this case).

#### **Step 3: Driver Implementation**
- The selected driver (`com.mysql.cj.jdbc.Driver`) is responsible for:
  - Parsing the URL.
  - Establishing a network connection with the database server.
  - Returning an object that implements `java.sql.Connection`.

#### **Step 4: Further Operations**
- The `Connection` object returned by the driver allows the application to create `Statement` or `PreparedStatement` objects.
- These objects, implemented by the driver, handle SQL execution and return `ResultSet` objects (also implemented by the driver) to provide query results.

---

### **4. Example with MySQL JDBC Driver**
Here’s what happens when you use the MySQL JDBC driver:

#### Code Example:
```java
import java.sql.*;

public class JDBCExample {
    public static void main(String[] args) {
        try {
            // Load the MySQL driver class (optional with modern drivers)
            Class.forName("com.mysql.cj.jdbc.Driver");

            // Establish a connection
            Connection con = DriverManager.getConnection(
                "jdbc:mysql://localhost:3306/mydb", "root", "password");

            // Create a statement
            Statement stmt = con.createStatement();

            // Execute a query
            ResultSet rs = stmt.executeQuery("SELECT * FROM students");

            // Process the result
            while (rs.next()) {
                System.out.println("ID: " + rs.getInt("id"));
                System.out.println("Name: " + rs.getString("name"));
            }

            // Close the connection
            con.close();
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

#### Behind the Scenes:
1. **DriverManager.getConnection**:
   - Finds the MySQL driver because of the `jdbc:mysql` URL prefix.
   - Calls the `connect()` method of the `com.mysql.cj.jdbc.Driver` class.

2. **`connect()` Method**:
   - Parses the URL.
   - Establishes a connection to the MySQL server.
   - Returns a `Connection` object implemented by the MySQL driver.

3. **`Statement` and `ResultSet`**:
   - When you create a `Statement` or execute a query, the MySQL driver provides implementations of `Statement` and `ResultSet`.

---

### **5. Summary**

- JDBC provides the **specifications** (interfaces) for database interaction.
- Database vendors provide **JDBC drivers** that implement these specifications with database-specific logic.
- The **driver selected by `DriverManager`** based on the URL handles all the actual database communication, including connection establishment, query execution, and result retrieval.
- You, as the developer, work with the JDBC interfaces, while the driver takes care of the implementation details.

## Notes

*By default, JDBC operates in auto-commit mode, meaning each SQL statement is executed and committed immediately. However, if you need to control transactions manually, you can disable auto-commit and manage transactions explicitly using commit() and rollback().*
