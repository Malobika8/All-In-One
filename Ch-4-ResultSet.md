### **What is a `ResultSet` in JDBC?**

A **`ResultSet`** is a Java object provided by JDBC that represents the result of a SQL query executed on a database. It acts as a cursor pointing to the data retrieved from the database, allowing applications to iterate through rows and access column values.

<img width="1104" alt="Screenshot 2025-01-20 at 8 17 28 PM" src="https://github.com/user-attachments/assets/c6294bbc-9203-4a7a-bfea-5c386e2f2dce" />

---

### **Key Features of `ResultSet`**
1. **Holds Query Results**:
   - Stores the data retrieved by a `SELECT` query.
   - Data is accessed row by row.

2. **Cursor-Based Navigation**:
   - The `ResultSet` has a cursor that starts **before the first row** and moves one row at a time.
   - The `next()` method is used to move the cursor.

3. **Data Access**:
   - Provides methods to access column values by column name or column index.
   - Data can be retrieved in various formats like `int`, `String`, `Date`, etc.

4. **Read-Only by Default**:
   - By default, a `ResultSet` is read-only and forward-only.
   - However, it can be made scrollable and updatable using specific options.

---

### **Types of `ResultSet`**
`ResultSet` can be configured based on:
1. **Scrollability**:
   - **Forward-only (`TYPE_FORWARD_ONLY`)**:
     - Default type.
     - Cursor moves only forward.
   - **Scrollable (`TYPE_SCROLL_INSENSITIVE` or `TYPE_SCROLL_SENSITIVE`)**:
     - Allows moving the cursor forward, backward, or to a specific row.

2. **Updatability**:
   - **Read-only (`CONCUR_READ_ONLY`)**:
     - Default mode.
     - Data in the `ResultSet` cannot be updated.
   - **Updatable (`CONCUR_UPDATABLE`)**:
     - Allows modifying data directly in the `ResultSet`.

---

### **Common Methods in `ResultSet`**

| **Method**                  | **Description**                                                   |
|-----------------------------|-------------------------------------------------------------------|
| `next()`                    | Moves the cursor to the next row. Returns `false` if no more rows exist. |
| `getInt(String columnLabel)`| Retrieves an integer value from a column.                        |
| `getString(int columnIndex)`| Retrieves a string value from a column using its index (1-based). |
| `absolute(int rowNumber)`   | Moves the cursor to the specified row (for scrollable `ResultSet`). |
| `previous()`                | Moves the cursor to the previous row (for scrollable `ResultSet`). |
| `updateString(String columnLabel, String value)` | Updates the value of a column (for updatable `ResultSet`). |
| `close()`                   | Closes the `ResultSet` and releases database resources.          |

---

### **How to Use `ResultSet`**
1. **Executing a Query**:
   A `ResultSet` is obtained by executing a `SELECT` query using a `Statement` or `PreparedStatement`.

   ```java
   String query = "SELECT id, name FROM students";
   Statement stmt = con.createStatement();
   ResultSet rs = stmt.executeQuery(query);
   ```

2. **Iterating Through Rows**:
   Use the `next()` method to move the cursor and retrieve column values.

   ```java
   while (rs.next()) {
       int id = rs.getInt("id"); // Access by column label
       String name = rs.getString(2); // Access by column index (1-based)
       System.out.println("ID: " + id + ", Name: " + name);
   }
   ```

3. **Closing the `ResultSet`**:
   Always close the `ResultSet` after use to free up resources.

   ```java
   rs.close();
   ```

---

### **Advantages of `ResultSet`**
- Simplifies the process of accessing and iterating through query results.
- Supports multiple data types for retrieving column values.
- Allows direct updates to the database when using an **updatable ResultSet**.

---

### **Best Practices**
1. Always close the `ResultSet`, `Statement`, and `Connection` objects to avoid resource leaks.
2. Prefer column labels (`getString("columnName")`) over indexes for better readability.
3. Use scrollable or updatable `ResultSet` only when necessary, as they have higher memory overhead.

---

### Example: Working with `ResultSet`
```java
try (Connection con = DriverManager.getConnection("jdbc:mysql://localhost:3306/mydb", "user", "password");
     Statement stmt = con.createStatement();
     ResultSet rs = stmt.executeQuery("SELECT id, name FROM students")) {

    while (rs.next()) {
        int id = rs.getInt("id");
        String name = rs.getString("name");
        System.out.println("ID: " + id + ", Name: " + name);
    }
} catch (SQLException e) {
    e.printStackTrace();
}
```

This example demonstrates how to execute a query, iterate through the `ResultSet`, and access column data.

## FYI

If you create a `ResultSet` with:

```java
ResultSet.TYPE_SCROLL_SENSITIVE
ResultSet.CONCUR_READ_ONLY
```

It means:

---

### ✅ What This Combination Does

| Feature                       | Behavior                                                                        |
| ----------------------------- | ------------------------------------------------------------------------------- |
| **Scrollability**             | Yes — you can move forward, backward, to any row                                |
| **Sensitivity to DB Changes** | Yes — the `ResultSet` **reflects updates** made to the database while it's open |
| **Updatability**              | ❌ No — you **cannot** modify the data using this `ResultSet` (read-only)        |

---

### 🧠 Example Use Case

* You want to **scroll through** the data in both directions.
* You **do not intend to update** data via the `ResultSet`.
* You **want to see real-time changes** made by others (or by triggers, etc.) in the database **while** the `ResultSet` is still open.

---

### ⚠️ Important Caveats

* Not all JDBC drivers or databases **support `TYPE_SCROLL_SENSITIVE`**.

  * For example, **MySQL Connector/J** does **not support it** — it silently downgrades it to `TYPE_SCROLL_INSENSITIVE`.
* Performance may degrade if the JDBC driver has to check the database frequently to reflect changes.

---

### 🧪 Example

```java
Statement stmt = conn.createStatement(
    ResultSet.TYPE_SCROLL_SENSITIVE,
    ResultSet.CONCUR_READ_ONLY
);

ResultSet rs = stmt.executeQuery("SELECT * FROM employees");

// Assume another user updates this employee's name in the DB
Thread.sleep(5000); // Simulate delay
rs.absolute(1); // Move to first row again (may refresh row data)

System.out.println(rs.getString("name")); // Might show updated name (if driver supports it)
```

---

### ✅ Summary

Using `TYPE_SCROLL_SENSITIVE` with `CONCUR_READ_ONLY`:

* Gives you **real-time visibility of changes**
* **No permission to update/delete**
* Depends on **driver and DB support**

