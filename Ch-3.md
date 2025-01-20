In JDBC, you decide between `executeQuery()` and `executeUpdate()` based on the type of SQL operation you are performing. Here's a clear guide on when to use each:

---

### **1. `executeQuery()`**

- **Purpose**: 
  - Use `executeQuery()` for SQL **SELECT statements**.
  - It retrieves data from the database and returns a **ResultSet** containing the query results.

- **Return Type**: 
  - `ResultSet` (a table of data from the query).

- **Best Use Cases**:
  - Fetching rows from a database.
  - Reading data without modifying the database.

- **Example**:
  ```java
  String query = "SELECT * FROM students WHERE grade = ?";
  PreparedStatement pstmt = con.prepareStatement(query);
  pstmt.setString(1, "A");  // Set grade parameter
  ResultSet rs = pstmt.executeQuery();

  while (rs.next()) {
      System.out.println("Student ID: " + rs.getInt("id"));
      System.out.println("Name: " + rs.getString("name"));
  }
  ```

---

### **2. `executeUpdate()`**

- **Purpose**: 
  - Use `executeUpdate()` for SQL **INSERT**, **UPDATE**, and **DELETE statements**.
  - It modifies the database by adding, updating, or deleting rows.

- **Return Type**: 
  - An `int` indicating the number of rows affected by the query.

- **Best Use Cases**:
  - Inserting new rows into a table.
  - Updating existing data.
  - Deleting rows from a table.

- **Example**:
  ```java
  String query = "UPDATE students SET grade = ? WHERE id = ?";
  PreparedStatement pstmt = con.prepareStatement(query);
  pstmt.setString(1, "B");  // Set new grade
  pstmt.setInt(2, 101);     // Set student ID
  int rowsUpdated = pstmt.executeUpdate();

  System.out.println("Rows Updated: " + rowsUpdated);
  ```

---

### **Key Differences**

| Aspect                 | `executeQuery()`                            | `executeUpdate()`                             |
|------------------------|---------------------------------------------|----------------------------------------------|
| **Used For**           | `SELECT` queries (fetching data).          | `INSERT`, `UPDATE`, `DELETE` queries (data modification). |
| **Return Type**        | `ResultSet` (query results).               | `int` (number of rows affected).            |
| **Database Changes**   | Does not modify the database.              | Modifies the database.                      |

---

### **3. What About `execute()`?**

If you are unsure about the type of query (e.g., dynamic queries), you can use `execute()`. This method:
- Returns `true` if the query is a `SELECT` statement (indicating that a `ResultSet` is available).
- Returns `false` for `INSERT`, `UPDATE`, or `DELETE` queries (indicating an update count is available).

**Example**:
```java
boolean isResultSet = stmt.execute("SELECT * FROM students");
if (isResultSet) {
    ResultSet rs = stmt.getResultSet();
    while (rs.next()) {
        System.out.println(rs.getString("name"));
    }
} else {
    int rowsAffected = stmt.getUpdateCount();
    System.out.println("Rows affected: " + rowsAffected);
}
```

---

### Summary
- Use **`executeQuery()`** for reading data (`SELECT`).
- Use **`executeUpdate()`** for modifying data (`INSERT`, `UPDATE`, `DELETE`).
- Use **`execute()`** when the query type is not known in advance.
