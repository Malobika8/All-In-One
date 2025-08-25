# Spring Security – Using `JdbcUserDetailsManager` for Persistent User Storage

## 1. 🔄 Why Move from In-Memory to JDBC?

* **Problem with In-Memory storage**:

  * User credentials exist only in server memory.
  * Lost when server restarts → not practical for real applications.

* **Solution**:

  * Use `JdbcUserDetailsManager` → stores users in a **database** (e.g., MySQL).
  * Ensures **persistence** across restarts.

---

## 2. ⚙️ Setup for JDBC User Management

### Dependencies

* Need JDBC and MySQL driver dependencies in the project.

### `DataSource` Bean

```java
@Bean
public DataSource dataSource() {
    DriverManagerDataSource dataSource = new DriverManagerDataSource();
    dataSource.setDriverClassName("com.mysql.cj.jdbc.Driver");
    dataSource.setUrl("jdbc:mysql://localhost:3306/spring_security_demo");
    dataSource.setUsername("root");
    dataSource.setPassword("password");
    return dataSource;
}
```

* Provides database connectivity.
* Injected into `JdbcUserDetailsManager`.

### `JdbcUserDetailsManager` Bean

```java
@Bean
public UserDetailsManager userDetailsManager(DataSource dataSource) {
    return new JdbcUserDetailsManager(dataSource);
}
```

---

## 3. 🗄️ Database Schema Expectations

Spring Security expects **two specific tables** by default:

### (a) `users` table

Stores **username, password, and enabled status**.

```sql
CREATE TABLE users (
    username VARCHAR(50) NOT NULL PRIMARY KEY,
    password VARCHAR(100) NOT NULL,
    enabled BOOLEAN NOT NULL
);
```

### (b) `authorities` table

Stores **user roles**. Each user → one or more roles.

```sql
CREATE TABLE authorities (
    username VARCHAR(50) NOT NULL,
    authority VARCHAR(50) NOT NULL,
    CONSTRAINT fk_user FOREIGN KEY (username) REFERENCES users(username)
);
```

✅ Every user must have at least one entry in `authorities`.
✅ Roles are expected to have prefix `ROLE_`.

---

## 4. 🔍 Internals of `JdbcUserDetailsManager`

* `JdbcUserDetailsManager` internally uses **`JdbcTemplate`**.
* Example: when calling `createUser(user)`, it runs **SQL insert statements** into `users` and `authorities`.
* This removes the need for manual SQL writing (as long as schema matches).

---

## 5. 🛠️ Common Issues & Fixes

* **Missing Tables** → errors like `Table 'users' doesn't exist`.
  → Must create `users` and `authorities` tables exactly as expected.

* **Password Length Error** →

  * BCrypt encoded passwords are long (60+ chars).
  * Ensure `password` column is at least `VARCHAR(100)`.

* **Missing Authority** →

  * User without role → login fails.
  * Always add at least one authority in `authorities` table.

---

## 6. 🔑 Role Handling

* Stored in `authorities.authority` column.
* Spring Security automatically uses **`ROLE_` prefix** convention.
* Example:

  * In DB: `"ROLE_ADMIN"`
  * At runtime: checked as `hasRole("ADMIN")`.

---

## 7. 📊 Flow of User Registration with JDBC

```mermaid
flowchart TD
    A[User Submits Registration Form] --> B[Controller Creates UserDetails Object]
    B --> C[JdbcUserDetailsManager.createUser()]
    C --> D[Insert into users table]
    C --> E[Insert into authorities table]
    D & E --> F[User Persisted in DB]
    F --> G[Authentication Loads User from DB on Login]
```

---

## 8. ❓ Key Clarifications from the Session

* **JDBC vs JPA**:

  * `JdbcUserDetailsManager` uses raw JDBC.
  * Developers can replace it with JPA/Hibernate for custom table design.

* **Custom Schema**:

  * Default schema reduces boilerplate.
  * But in real apps, you often customize → must override queries.

---

## 9. 🧩 Takeaways

* Move from **in-memory → database** for real-world security.
* Use **`JdbcUserDetailsManager` + default schema** for quick setup.
* Be mindful of:

  * Password column length (BCrypt).
  * Each user must have a role.
* Default schema is optional; customization possible if needed.

---

👉 With this we'll move from **temporary, in-memory user storage** to **persistent, database-backed authentication** using Spring Security’s built-in JDBC support.

---
