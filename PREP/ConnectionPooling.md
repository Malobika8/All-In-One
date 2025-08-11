### **What is Connection Pooling in JDBC?**

* A technique where a pool (collection) of **pre-created, reusable database connections** is maintained.
* When the application needs a connection, it borrows one from the pool instead of creating a new one.
* After use, the connection is returned to the pool for reuse rather than closed permanently.

---

### **Why use it?**

1. **Performance** – Establishing a DB connection is expensive (network handshake, authentication, resource allocation).
2. **Scalability** – Pools limit the max number of open DB connections, preventing resource exhaustion.
3. **Resource Management** – Idle connections are monitored and closed if necessary.

---

### **Popular Connection Pooling Libraries/Frameworks**

* **HikariCP** (fastest, widely used with Spring Boot)
* **Apache DBCP** (Apache Commons)
* **C3P0**
* Application servers like **Tomcat JDBC Pool**, **WildFly** have built-in pools.

---

*"Does JDBC itself provide connection pooling?"* — the answer is **No**.

* JDBC API does not implement pooling.
* Pooling is implemented by **third-party libraries** or the **application server**.
* JDBC **DataSource** interface is used by pooling implementations to hand out connections.

---

**Q12 (Theory)**
In JDBC, what is the difference between using `DriverManager` and using a `DataSource` for getting connections?
