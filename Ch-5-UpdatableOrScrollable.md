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
