# Spring Security – Custom User Authentication with Custom Table & `UserDetailsService`

---

## 1. 🔄 Why Custom Authentication?

* Default Spring Security JDBC (`JdbcUserDetailsManager`) expects **`users`** and **`authorities`** tables.
* Real-world applications usually have their own user table (e.g., `student`, `customer`).
* Requirement: Authenticate users from this **custom table**.

---

## 2. 🗄️ Custom Table Example (`student`)

```sql
CREATE TABLE student (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(50),
    password VARCHAR(100),
    role VARCHAR(50),
    email VARCHAR(100)
);
```

* Fields:

  * `username` or `email` → used for login
  * `password` → must be encoded (BCrypt)
  * `role` → authorities for authorization
  * `email` → alternate identifier

---

## 3. ⚙️ Implementing Custom `UserDetailsService`

### Step 1: Create Service Class

```java
@Service
public class StudentDetailsService implements UserDetailsService {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    @Override
    public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
        String sql = "SELECT * FROM student WHERE username = ?";
        
        List<StudentDto> students = jdbcTemplate.query(
            sql, 
            new BeanPropertyRowMapper<>(StudentDto.class), 
            username
        );

        if (students.isEmpty()) {
            throw new UsernameNotFoundException("User not found with username: " + username);
        }

        StudentDto student = students.get(0);

        return User.builder()
            .username(student.getUsername())
            .password(student.getPassword())
            .roles(student.getRole())   // Spring automatically prefixes ROLE_
            .build();
    }
}
```

---

## 4. 🧩 Why Use `query` Instead of `queryForObject`?

* `queryForObject` → throws exception if no rows found → messy error handling.
* `query` → returns a list.

  * If empty → handle gracefully with `UsernameNotFoundException`.

✅ Cleaner, avoids runtime errors during authentication.

---

## 5. 🗝️ Mapping DB Rows to DTO

* Use **`BeanPropertyRowMapper`**:

  * Maps DB columns → DTO fields (if names match).

```java
public class StudentDto {
    private String username;
    private String password;
    private String role;
    private String email;
    // getters & setters
}
```

* Reduces boilerplate (no manual `ResultSet` extraction).

---

## 6. 🔑 Switching Login from Username → Email

* Change SQL query:

  ```sql
  SELECT * FROM student WHERE email = ?
  ```

* In `loadUserByUsername`, interpret the `username` parameter as **email**.

```java
String sql = "SELECT * FROM student WHERE email = ?";
```

* Use email as the principal identifier in `UserDetails`.

---

## 7. ⚠️ Common Issues & Troubleshooting

### (a) Ambiguous Beans

* If multiple `UserDetailsService` beans exist → Spring Security is confused.
* ❌ Error: *No AuthenticationProvider found*
* ✅ Fix: Ensure only one `UserDetailsService` bean is active.

---

### (b) Circular Dependencies

* Occur when two beans depend on each other.
* Solution:

  * Use `@Lazy` to defer bean creation.
  * Example:

    ```java
    @Autowired
    @Lazy
    private StudentDetailsService studentDetailsService;
    ```

---

## 8. 📊 Authentication Flow with Custom Table

```mermaid
flowchart TD
    A[Login Form Submit: email/password] --> B[Spring Security calls loadUserByUsername()]
    B --> C[JdbcTemplate executes query on student table]
    C --> D[Map result to StudentDto via BeanPropertyRowMapper]
    D --> E[Convert to UserDetails object]
    E --> F[Spring Security Authentication Manager validates password]
    F --> G[If valid → Authentication Success, else → Failure]
```

---

## 9. 🧩 Takeaways

* Default Spring Security schema works only for simple apps.
* For custom schemas → implement your own `UserDetailsService`.
* Prefer `query` over `queryForObject`.
* Use DTO + `BeanPropertyRowMapper` for cleaner code.
* Switching login from username → email is just **query + mapping change**.
* Manage beans carefully to avoid **ambiguity** and **circular dependency** issues.

---
