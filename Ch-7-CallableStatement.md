## CallableStatement

You call stored procedures in JDBC using **CallableStatement**.

Consider the stored procedure in database,

```
CREATE PROCEDURE getEmployee(IN empId INT, OUT empName VARCHAR(50))
BEGIN
    SELECT name INTO empName FROM Employee WHERE id = empId;
END;
```

To use it:

1. Use `prepareCall()` with the procedure signature
   Example: `{call getEmployee(?, ?)}`
2. Set **IN parameters** using `setXXX()`
3. Register **OUT parameters** using `registerOutParameter()`
4. Execute using `execute()`
5. Retrieve OUT parameters using `getXXX()`

# ✅ **Correct JDBC Code for the Given Stored Procedure**

```java
String sql = "{ call getEmployee(?, ?) }";

try (Connection con = DriverManager.getConnection(url, user, pass);
     CallableStatement cs = con.prepareCall(sql)) {

    // Set IN parameter
    cs.setInt(1, 1);

    // Register OUT parameter
    cs.registerOutParameter(2, Types.VARCHAR);

    // Execute stored procedure
    cs.execute();

    // Read OUT parameter
    String empName = cs.getString(2);

    System.out.println("Employee Name: " + empName);

} catch (SQLException ex) {
    ex.printStackTrace();
}
```

---

