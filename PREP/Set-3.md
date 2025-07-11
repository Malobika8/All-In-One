### ✅ **What is a JDBC Transaction?**

In JDBC, a transaction is a **set of operations that should either all succeed or all fail**.

By default, JDBC is in **auto-commit mode**, which means each statement is immediately committed.

### Why Use Transactions?

* Suppose you're transferring money between accounts:

  * Deduct from one account ✅
  * Add to another ✅
    ➤ If one fails, **rollback** both to avoid inconsistency 💣

### Key Methods:

| Method                            | Description                          |
| --------------------------------- | ------------------------------------ |
| `connection.setAutoCommit(false)` | Begin transaction manually           |
| `connection.commit()`             | Finalize transaction                 |
| `connection.rollback()`           | Cancel changes if any failure occurs |

---

# Write JDBC code that transfers balance between two accounts (fromId → toId).

Assume:

* Table: `accounts(id INT, balance INT)`
* Deduct 100 from `fromId`
* Add 100 to `toId`
* Use transactions, rollback on failure

**Method Signature:**

```java
public static void transferAmount(int fromId, int toId, int amount)
```

### Sol:

```java
import java.sql.*;

public class Main {

    public static void transferAmount(int fromId, int toId, int amount) {
        Connection connection = null;
        PreparedStatement ps1 = null;
        PreparedStatement ps2 = null;

        try {
            connection = getConnection();
            connection.setAutoCommit(false); // Start transaction

            String debitSQL = "UPDATE accounts SET balance = balance - ? WHERE id = ?";
            String creditSQL = "UPDATE accounts SET balance = balance + ? WHERE id = ?";

            ps1 = connection.prepareStatement(debitSQL);
            ps1.setInt(1, amount);
            ps1.setInt(2, fromId);
            ps1.executeUpdate();

            ps2 = connection.prepareStatement(creditSQL);
            ps2.setInt(1, amount);
            ps2.setInt(2, toId);
            ps2.executeUpdate();

            connection.commit(); // Success
            System.out.println("Transaction successful.");
        } catch (Exception e) {
            System.out.println("Transaction failed: " + e.getMessage());
            try {
                if (connection != null) connection.rollback(); // Rollback on error
            } catch (Exception rollbackEx) {
                System.out.println("Rollback failed: " + rollbackEx.getMessage());
            }
        } finally {
            try { if (ps1 != null) ps1.close(); } catch (Exception ignored) {}
            try { if (ps2 != null) ps2.close(); } catch (Exception ignored) {}
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

