## ✅ **What is JDBC Batching?**

**JDBC Batching** allows you to execute **multiple SQL statements in a single round-trip** to the database.

👉 Without batching:

```java
for (Emp emp : employees) {
    pstmt.setString(1, emp.getName());
    pstmt.executeUpdate(); // One query per round-trip 🚫
}
```

👉 With batching:

```java
for (Emp emp : employees) {
    pstmt.setString(1, emp.getName());
    pstmt.addBatch(); // Collect statements ✅
}
pstmt.executeBatch(); // Send all at once ✅
```

## ✅ **When is Batching Used?**

* Inserting multiple records (e.g., import CSV, bulk upload)
* Updating many rows at once
* Reducing network/database round-trips

---

# Write a method that inserts 3 employees into a table using JDBC batch. Assume table `employees(id INT, name VARCHAR)`. Use PreparedStatement with batch.

**Method signature:**

```java
public static void insertEmployeesInBatch(List<Employee> employees)
```

(Assume `Employee` is a class with `int id` and `String name`.)

### Sol:

```java
import java.sql.*;
import java.util.List;

public class Main {

    public static void insertEmployeesInBatch(List<Employee> employees) {
        Connection connection = null;
        PreparedStatement ps = null;

        try {
            connection = getConnection();

            String sql = "INSERT INTO employees (id, name) VALUES (?, ?)";
            ps = connection.prepareStatement(sql);

            for (Employee emp : employees) {
                ps.setInt(1, emp.getId());
                ps.setString(2, emp.getName());
                ps.addBatch();
            }

            ps.executeBatch();
            System.out.println("Batch insert completed.");
        } catch (Exception e) {
            e.printStackTrace();
        } finally {
            try { if (ps != null) ps.close(); } catch (Exception ignored) {}
            try { if (connection != null) connection.close(); } catch (Exception ignored) {}
        }
    }

    public static Connection getConnection() throws Exception {
        Class.forName("com.mysql.cj.jdbc.Driver");

        String url = "jdbc:mysql://localhost:3306/your_db";
        String user = "root";
        String password = "your_password";

        return DriverManager.getConnection(url, user, password);
    }
}
```

#### `Employee` Class:

```java
public class Employee {
    private int id;
    private String name;

    // Constructor
    public Employee(int id, String name) {
        this.id = id;
        this.name = name;
    }

    // Getters
    public int getId() { return id; }
    public String getName() { return name; }
}
```
