# Cheat Sheet: JDBC Notes

| Topic                              | Summary                                                                          |
| ---------------------------------- | -------------------------------------------------------------------------------- |
| `Connection`                       | Created via `DriverManager.getConnection(...)`                                   |
| `Statement` vs `PreparedStatement` | Use `Statement` for static SQL, `PreparedStatement` for dynamic (safer + faster) |
| `ResultSet`                        | Used to read query results row by row                                            |
| SQL Injection                      | Prevented by `PreparedStatement` (binds values safely)                           |
| Batching                           | Use `addBatch()` + `executeBatch()` to send multiple updates at once             |
| Transactions                       | Use `setAutoCommit(false)`, `commit()`, `rollback()` for atomic operations       |
| Try-with-resources                 | Closes `Connection`, `Statement`, `ResultSet` automatically                      |
| `executeQuery()`                   | For `SELECT` — returns `ResultSet`                                               |
| `executeUpdate()`                  | For `INSERT`, `UPDATE`, `DELETE` — returns row count                             |
| `execute()`                        | For DDL or unknown type — returns boolean                                        |
