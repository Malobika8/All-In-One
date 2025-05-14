### **Scrollable and Updatable `ResultSet` in JDBC**

In JDBC, a **`ResultSet`** is by default:
- **Forward-only**: You can only move the cursor forward through the rows.
- **Read-only**: You cannot modify the data it holds.

However, JDBC provides options to make a `ResultSet` **scrollable** and/or **updatable**, allowing for advanced functionality.

---

### **1. Scrollable `ResultSet`**
A scrollable `ResultSet` allows the cursor to move in both directions or jump to a specific row.

#### **Types of Scrollable `ResultSet`**
- **`TYPE_FORWARD_ONLY`** (Default): Cursor can only move forward (not scrollable).
- **`TYPE_SCROLL_INSENSITIVE`**:
  - Cursor can move forward, backward, or to an absolute/relative position.
  - Does not reflect changes made to the database after the `ResultSet` is created.
- **`TYPE_SCROLL_SENSITIVE`**:
  - Same as `TYPE_SCROLL_INSENSITIVE`, but reflects changes made to the database after the `ResultSet` is created.

#### **Example: Scrollable `ResultSet`**
```java
Statement stmt = con.createStatement(
    ResultSet.TYPE_SCROLL_INSENSITIVE, 
    ResultSet.CONCUR_READ_ONLY
);
ResultSet rs = stmt.executeQuery("SELECT * FROM students");

// Move the cursor to the last row
if (rs.last()) {
    System.out.println("Last Student ID: " + rs.getInt("id"));
}

// Move the cursor to the first row
rs.first();
System.out.println("First Student Name: " + rs.getString("name"));

// Move the cursor to the 3rd row
rs.absolute(3);
System.out.println("3rd Student Name: " + rs.getString("name"));

// Move the cursor one row backward
rs.previous();
System.out.println("Previous Student Name: " + rs.getString("name"));
```

---

### **2. Updatable `ResultSet`**
An updatable `ResultSet` allows you to modify the data it holds and update the database directly through the `ResultSet`.

#### **How to Create an Updatable `ResultSet`**
- Use `ResultSet.CONCUR_UPDATABLE` as the concurrency mode when creating the `Statement` or `PreparedStatement`.

#### **Example: Updatable `ResultSet`**
```java
Statement stmt = con.createStatement(
    ResultSet.TYPE_SCROLL_INSENSITIVE, 
    ResultSet.CONCUR_UPDATABLE
);
ResultSet rs = stmt.executeQuery("SELECT id, name FROM students");

// Move to the first row
if (rs.first()) {
    // Update the name in the ResultSet
    rs.updateString("name", "Updated Name");
    
    // Commit the update to the database
    rs.updateRow();
}

// Insert a new row into the ResultSet
rs.moveToInsertRow();
rs.updateInt("id", 101);
rs.updateString("name", "New Student");
rs.insertRow();

// Delete the current row
rs.absolute(2);
rs.deleteRow();
```

---

### **3. Key Differences**

| Feature                     | **Scrollable `ResultSet`**                           | **Updatable `ResultSet`**                          |
|-----------------------------|-----------------------------------------------------|--------------------------------------------------|
| **Purpose**                 | Enables moving the cursor in any direction.         | Allows modifying, inserting, or deleting rows in the database. |
| **Cursor Movements**        | Supports forward, backward, absolute, and relative. | Same as scrollable if scrollable is enabled.     |
| **Reflects Database Changes** | Sensitive (`TYPE_SCROLL_SENSITIVE`) reflects changes, insensitive (`TYPE_SCROLL_INSENSITIVE`) does not. | Not applicable.                                 |
| **Concurrency Mode**        | `ResultSet.CONCUR_READ_ONLY`                        | `ResultSet.CONCUR_UPDATABLE`                     |

---

### **4. Considerations**
1. **Performance**:
   - Scrollable and updatable `ResultSet` require more resources and are slower than forward-only, read-only `ResultSet`.
   - Use these features only when necessary.

2. **Driver Support**:
   - Not all JDBC drivers support scrollable or updatable `ResultSet`. Check your database and driver documentation.

3. **Batch Updates**:
   - For bulk updates, it may be more efficient to use `PreparedStatement` with batch execution rather than relying on an updatable `ResultSet`.

---

### **Summary**
- Use **Scrollable `ResultSet`** when you need to navigate data in different directions or jump to specific rows.
- Use **Updatable `ResultSet`** when you need to modify, insert, or delete rows directly from the `ResultSet`.
- Example of a combined scrollable and updatable `ResultSet`:
   ```java
   Statement stmt = con.createStatement(
       ResultSet.TYPE_SCROLL_INSENSITIVE, 
       ResultSet.CONCUR_UPDATABLE
   );
   ResultSet rs = stmt.executeQuery("SELECT * FROM students");
   ```

Here's a **step-by-step working example** that demonstrates the behavior of `TYPE_SCROLL_INSENSITIVE` vs `TYPE_SCROLL_SENSITIVE` using JDBC with a simple in-memory H2 database.

---

## ✅ Example: See Whether `TYPE_SCROLL_SENSITIVE` Reflects DB Updates

### 📦 Requirements:

* H2 database (`h2-1.x.x.jar`)
* JDBC-compatible Java setup

---

### 🚀 Step 1: Java Code

```java
import java.sql.*;

public class ScrollSensitivityDemo {
    public static void main(String[] args) throws Exception {
        // Load H2 driver
        Class.forName("org.h2.Driver");

        // Create in-memory DB
        Connection conn = DriverManager.getConnection("jdbc:h2:mem:testdb", "sa", "");

        Statement setupStmt = conn.createStatement();
        setupStmt.execute("CREATE TABLE employee (id INT PRIMARY KEY, name VARCHAR(100), salary INT)");
        setupStmt.execute("INSERT INTO employee VALUES (1, 'Alice', 5000)");
        setupStmt.execute("INSERT INTO employee VALUES (2, 'Bob', 6000)");

        // Use SCROLL_SENSITIVE
        Statement stmt = conn.createStatement(
                ResultSet.TYPE_SCROLL_SENSITIVE,
                ResultSet.CONCUR_UPDATABLE
        );

        ResultSet rs = stmt.executeQuery("SELECT * FROM employee");

        // Move to second row (Bob)
        rs.absolute(2);
        System.out.println("Before DB update: " + rs.getString("name") + ", salary = " + rs.getInt("salary"));

        // Simulate external update
        Statement updateStmt = conn.createStatement();
        updateStmt.executeUpdate("UPDATE employee SET salary = 9000 WHERE id = 2");

        // Now refresh and print again
        rs.refreshRow(); // Required for many drivers to see latest row data
        System.out.println("After DB update:  " + rs.getString("name") + ", salary = " + rs.getInt("salary"));

        rs.close();
        stmt.close();
        conn.close();
    }
}
```

---

### 🧾 Output (Expected with driver support for SCROLL\_SENSITIVE):

```
Before DB update: Bob, salary = 6000
After DB update:  Bob, salary = 9000
```

---

### 🔁 What to Try:

* Run this with `TYPE_SCROLL_INSENSITIVE` — and you'll see **no change** in salary even after `refreshRow()`.
* Run with `TYPE_SCROLL_SENSITIVE` — and `refreshRow()` may show the **updated** salary.
* Behavior **depends on JDBC driver**. H2 supports basic sensitivity. Oracle/PostgreSQL/MySQL vary.

---

### ✅ Recap:

| Action                   | INSENSITIVE Result | SENSITIVE Result |
| ------------------------ | ------------------ | ---------------- |
| `resultSet.getInt()`     | Old value          | Possibly updated |
| `resultSet.refreshRow()` | No effect          | Triggers reload  |

---
