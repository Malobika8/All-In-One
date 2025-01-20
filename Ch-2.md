### Difference Between `Statement`, `PreparedStatement`, and `CallableStatement` in JDBC

| **Aspect**             | **`Statement`**                              | **`PreparedStatement`**                            | **`CallableStatement`**                           |
|-------------------------|----------------------------------------------|---------------------------------------------------|--------------------------------------------------|
| **Purpose**            | Used for executing **simple SQL queries**.  | Used for executing **parameterized SQL queries**. | Used for executing **stored procedures** in a database. |
| **Query Structure**    | The query is provided directly as a **string**. | The query is precompiled with placeholders (`?`). | Calls stored procedures using the `{call}` syntax. |
| **Performance**        | Lower performance as the query is **parsed and compiled** each time it is executed. | Higher performance as the query is **compiled once** and reused with different parameters. | Optimized for calling stored procedures, which are precompiled. |
| **Example Usage**      | ```java Statement stmt = con.createStatement(); ResultSet rs = stmt.executeQuery("SELECT * FROM users"); ``` | ```java PreparedStatement pstmt = con.prepareStatement("SELECT * FROM users WHERE id = ?"); pstmt.setInt(1, 101); ResultSet rs = pstmt.executeQuery(); ``` | ```java CallableStatement cstmt = con.prepareCall("{call getUserDetails(?)}"); cstmt.setInt(1, 101); ResultSet rs = cstmt.executeQuery(); ``` |
| **SQL Injection Risk** | High, as the query string is concatenated with user inputs. | Low, as parameters are set separately and the query structure is fixed. | Low, since stored procedures encapsulate the logic. |
| **Reusability**        | Not reusable. Each query execution involves a new compilation. | Reusable with different parameter values, reducing overhead. | Designed for reuse but specific to stored procedure logic. |
| **Functionality**      | Basic. Supports queries like `SELECT`, `INSERT`, `UPDATE`, `DELETE`. | Supports all functionalities of `Statement`, with added parameterization and batch execution. | Specialized for invoking stored procedures with **IN, OUT, and INOUT parameters**. |
| **Best Use Case**      | For **simple, static queries** where parameters are not required. | For queries executed multiple times with **dynamic inputs**. | For databases with **complex logic encapsulated in stored procedures**. |

---

### Detailed Explanation and Code Examples

#### 1. **`Statement`**
- **Description**: Executes static SQL queries. Each execution involves sending the SQL statement to the database for compilation.
- **Example**:
  ```java
  Statement stmt = con.createStatement();
  String query = "SELECT * FROM employees";
  ResultSet rs = stmt.executeQuery(query);

  while (rs.next()) {
      System.out.println("Employee ID: " + rs.getInt("id"));
  }
  ```

#### 2. **`PreparedStatement`**
- **Description**: Precompiled SQL queries that support dynamic parameters. Reduces the overhead of query compilation on repeated execution.
- **Example**:
  ```java
  String query = "SELECT * FROM employees WHERE department_id = ?";
  PreparedStatement pstmt = con.prepareStatement(query);
  pstmt.setInt(1, 10);  // Setting parameter value
  ResultSet rs = pstmt.executeQuery();

  while (rs.next()) {
      System.out.println("Employee Name: " + rs.getString("name"));
  }
  ```

#### 3. **`CallableStatement`**
- **Description**: Used to call stored procedures in the database. Supports input (`IN`), output (`OUT`), and input-output (`INOUT`) parameters.
- **Example**:
  ```java
  CallableStatement cstmt = con.prepareCall("{call getEmployeeDetails(?)}");
  cstmt.setInt(1, 101);  // Input parameter
  ResultSet rs = cstmt.executeQuery();

  while (rs.next()) {
      System.out.println("Employee Name: " + rs.getString("name"));
  }
  ```

---

### Summary of Use Cases

- Use **`Statement`** when:
  - Queries are simple and unlikely to change.
  - There are no input parameters.

- Use **`PreparedStatement`** when:
  - Queries involve dynamic parameters.
  - The same query will be executed multiple times.
  - Preventing SQL injection is critical.

- Use **`CallableStatement`** when:
  - Working with stored procedures for encapsulating business logic.
  - Input and output parameters need to be handled efficiently. 

Each type is suited for specific scenarios, and selecting the right one ensures optimal performance and security.
