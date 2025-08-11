### **DriverManager**

* **Older approach** to getting JDBC connections.
* You explicitly call:

  ```java
  Connection con = DriverManager.getConnection(url, user, pass);
  ```
* No built-in pooling support — you’d need to manage connections manually or integrate with a pooling library yourself.
* Tightly coupled to the JDBC driver class (often requires `Class.forName(...)` in older code).

---

### **DataSource**

* Introduced in JDBC 2.0 as the **preferred** connection factory.
* Allows connection acquisition without hardcoding driver details — configured externally (e.g., via JNDI in enterprise apps).
* Often wraps a **connection pool implementation** (HikariCP, DBCP, C3P0, etc.).
* More flexible: supports connection pooling and distributed transactions (`XADataSource`).

---

💡 *“Which should you prefer in production?”*, answer: **`DataSource`** — because it decouples configuration from code and integrates well with connection pooling.

---

```java
import com.zaxxer.hikari.HikariConfig;
import com.zaxxer.hikari.HikariDataSource;
import java.sql.*;

public class EmployeeCountExample {

    public static Connection getConnection() throws SQLException {
        HikariConfig config = new HikariConfig();
        config.setJdbcUrl("jdbc:mysql://localhost:3306/yourdb");
        config.setUsername("yourusername");
        config.setPassword("yourpassword");
        config.setMaximumPoolSize(10);

        HikariDataSource ds = new HikariDataSource(config);
        return ds.getConnection();
    }

    public static void main(String[] args) {
        try (Connection con = getConnection();
             Statement stmt = con.createStatement();
             ResultSet rs = stmt.executeQuery("SELECT COUNT(*) FROM employee")) {

            if (rs.next()) {
                System.out.println("Employee count: " + rs.getInt(1));
            }

        } catch (SQLException e) {
            e.printStackTrace();
        }
    }
}
```

---

* Uses **`HikariConfig`** for clean config separation.
* Returns an actual `Connection`.
* Uses try-with-resources for **safe closing**.
* Demonstrates **pooling with HikariCP** and a simple query.

---


