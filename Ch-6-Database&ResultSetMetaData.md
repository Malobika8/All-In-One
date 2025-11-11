# DatabaseMetaData vs ResultSetMetaData

## **1. DatabaseMetaData**

**Think of it as: *“Information about the database itself.”***

You use it when you want to know:

* Which database you are connected to
* Version of DB
* What tables exist
* What columns exist in a specific table
* What features the DB supports
* Whether it supports transactions, batch updates, etc.

✅ **Example uses in real-life:**

* Tools like IntelliJ, DBeaver, Hibernate use this to explore DB schema.
* Frameworks use it to auto-generate tables or validate schema.

### ✅ **Code Example**

```java
Connection con = DriverManager.getConnection(url, user, pass);
DatabaseMetaData dbmd = con.getMetaData();

System.out.println(dbmd.getDatabaseProductName());
System.out.println(dbmd.getDatabaseProductVersion());

// List all tables
ResultSet tables = dbmd.getTables(null, null, "%", null);
while (tables.next()) {
    System.out.println("Table: " + tables.getString("TABLE_NAME"));
}
```

---

# **2. ResultSetMetaData**

**Think of it as: *“Information about the columns in a ResultSet.”***

Whenever you run a `SELECT` query and get a `ResultSet`, you can inspect:

* Number of columns
* Column names
* Column data types
* Whether a column is nullable
* Whether it is auto-increment
* Column display size

✅ **Useful when:**

* You don’t know query structure at compile-time
* You are writing a generic table printer
* You are building a DB tool or ORM-like feature

### ✅ **Code Example**

```java
Statement stmt = con.createStatement();
ResultSet rs = stmt.executeQuery("SELECT id, name, salary FROM Employee");

ResultSetMetaData rsmd = rs.getMetaData();

int columnCount = rsmd.getColumnCount();
System.out.println("Total columns: " + columnCount);

for (int i = 1; i <= columnCount; i++) {
    System.out.println("Column " + i + ": " + rsmd.getColumnName(i));
    System.out.println("Type: " + rsmd.getColumnTypeName(i));
}
```

---

### ✅ **DatabaseMetaData**

> “DatabaseMetaData provides information about the database: DB name, version, driver name, supported features, available tables, schemas, etc.”

### ✅ **ResultSetMetaData**

> “ResultSetMetaData provides information about the columns in a ResultSet: number of columns, column names, types, nullability, auto-increment, etc.”

---

