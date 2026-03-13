# Requirement:

* **Custom `UserDetails`**
* **Custom `UserDetailsManager`**
* Employees should **register**
* You want to override **all CRUD methods**

  * `createUser`
  * `updateUser`
  * `deleteUser`
  * `changePassword`
  * `userExists`
  * `loadUserByUsername`

This is exactly what **`JdbcUserDetailsManager` does internally**, but since we want **custom schema (employeeId)** we implement our **own version**.

Below is a **clean production-style implementation**.

---

# 1️⃣ Database Schema

### employee table

```sql
CREATE TABLE employee (
    employee_id VARCHAR(50) PRIMARY KEY,
    password VARCHAR(255),
    enabled BOOLEAN
);
```

### employee_role table

```sql
CREATE TABLE employee_role (
    employee_id VARCHAR(50),
    role VARCHAR(50)
);
```

Example:

```
employee
----------------------------
EMP001 | bcrypt_hash | true

employee_role
----------------------------
EMP001 | ROLE_USER
```

---

# 2️⃣ Custom UserDetails (EmployeeUser)

```java
package com.company.security.entity;

import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;

import java.util.Collection;

public class EmployeeUser implements UserDetails {

    private String employeeId;
    private String password;
    private boolean enabled;
    private Collection<? extends GrantedAuthority> authorities;

    public EmployeeUser(String employeeId,
                        String password,
                        boolean enabled,
                        Collection<? extends GrantedAuthority> authorities) {

        this.employeeId = employeeId;
        this.password = password;
        this.enabled = enabled;
        this.authorities = authorities;
    }

    @Override
    public Collection<? extends GrantedAuthority> getAuthorities() {
        return authorities;
    }

    @Override
    public String getPassword() {
        return password;
    }

    @Override
    public String getUsername() {
        return employeeId;
    }

    @Override
    public boolean isEnabled() {
        return enabled;
    }
}
```

---

# 3️⃣ Custom UserDetailsManager

```java
@Service
public class EmployeeUserDetailsManager implements UserDetailsManager {

    private final JdbcTemplate jdbcTemplate;
    private final PasswordEncoder passwordEncoder;

    public EmployeeUserDetailsManager(JdbcTemplate jdbcTemplate,
                                      PasswordEncoder passwordEncoder) {
        this.jdbcTemplate = jdbcTemplate;
        this.passwordEncoder = passwordEncoder;
    }

    private static final String CREATE_USER =
            "insert into employee(employee_id,password,enabled) values(?,?,?)";

    private static final String CREATE_ROLE =
            "insert into employee_role(employee_id,role) values(?,?)";

    private static final String UPDATE_USER =
            "update employee set password=? where employee_id=?";

    private static final String DELETE_ROLE =
            "delete from employee_role where employee_id=?";

    private static final String DELETE_USER =
            "delete from employee where employee_id=?";

    private static final String LOAD_USER =
            "select * from employee where employee_id=?";

    private static final String LOAD_ROLE =
            "select role from employee_role where employee_id=?";

    private static final String USER_EXISTS =
            "select count(*) from employee where employee_id=?";

```

---

# 4️⃣ createUser (Employee Registration)

```java
@Override
public void createUser(UserDetails user) {

    jdbcTemplate.update(
            CREATE_USER,
            user.getUsername(),
            passwordEncoder.encode(user.getPassword()),
            true
    );

    for (GrantedAuthority authority : user.getAuthorities()) {

        jdbcTemplate.update(
                CREATE_ROLE,
                user.getUsername(),
                authority.getAuthority()
        );
    }
}
```

This runs during **employee registration**.

---

# 5️⃣ updateUser

```java
@Override
public void updateUser(UserDetails user) {

    jdbcTemplate.update(
            UPDATE_USER,
            passwordEncoder.encode(user.getPassword()),
            user.getUsername()
    );

    jdbcTemplate.update(DELETE_ROLE, user.getUsername());

    for (GrantedAuthority authority : user.getAuthorities()) {

        jdbcTemplate.update(
                CREATE_ROLE,
                user.getUsername(),
                authority.getAuthority()
        );
    }
}
```

---

# 6️⃣ deleteUser

```java
@Override
public void deleteUser(String employeeId) {

    jdbcTemplate.update(DELETE_ROLE, employeeId);
    jdbcTemplate.update(DELETE_USER, employeeId);
}
```

Roles must be deleted first (FK safety).

---

# 7️⃣ changePassword

```java
@Override
public void changePassword(String oldPassword, String newPassword) {

    Authentication auth =
            SecurityContextHolder.getContext().getAuthentication();

    String employeeId = auth.getName();

    jdbcTemplate.update(
            UPDATE_USER,
            passwordEncoder.encode(newPassword),
            employeeId
    );
}
```

Spring Security already knows **current logged user**.

---

# 8️⃣ userExists

```java
@Override
public boolean userExists(String employeeId) {

    Integer count = jdbcTemplate.queryForObject(
            USER_EXISTS,
            Integer.class,
            employeeId
    );

    return count != null && count > 0;
}
```

---

# 9️⃣ loadUserByUsername (Authentication)

```java
@Override
public UserDetails loadUserByUsername(String employeeId)
        throws UsernameNotFoundException {

    try {

        EmployeeUser user = jdbcTemplate.queryForObject(
                LOAD_USER,
                (rs, rowNum) -> new EmployeeUser(
                        rs.getString("employee_id"),
                        rs.getString("password"),
                        rs.getBoolean("enabled"),
                        List.of()
                ),
                employeeId
        );

        List<SimpleGrantedAuthority> authorities =
                jdbcTemplate.query(
                        LOAD_ROLE,
                        (rs, rowNum) ->
                                new SimpleGrantedAuthority(rs.getString("role")),
                        employeeId
                );

        return new EmployeeUser(
                user.getUsername(),
                user.getPassword(),
                user.isEnabled(),
                authorities
        );

    } catch (Exception e) {
        throw new UsernameNotFoundException("Employee not found");
    }
}
```

This method is called during **authentication**.

---

# 🔟 Employee Registration Controller

```java
@RestController
public class EmployeeRegistrationController {

    private final UserDetailsManager userDetailsManager;

    public EmployeeRegistrationController(UserDetailsManager userDetailsManager) {
        this.userDetailsManager = userDetailsManager;
    }

    @PostMapping("/register")
    public String register(@RequestParam String employeeId,
                           @RequestParam String password) {

        UserDetails user = User.builder()
                .username(employeeId)
                .password(password)
                .roles("USER")
                .build();

        userDetailsManager.createUser(user);

        return "Employee registered";
    }
}
```

---

# 1️⃣1️⃣ Protected Resource

```java
@RestController
public class WorkController {

    @GetMapping("/pendingWork")
    public String pendingWork() {
        return "Your pending tasks";
    }
}
```

---

# 1️⃣2️⃣ Security Config

```java
@Bean
public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {

    http
        .authorizeHttpRequests(auth -> auth
                .requestMatchers("/register").permitAll()
                .requestMatchers("/pendingWork").authenticated()
        )
        .formLogin(Customizer.withDefaults());

    return http.build();
}
```

---

# 🔑 Full Flow

### 1️⃣ Employee registers

```
POST /register
```

↓

### 2️⃣ `createUser()` executes

```
employee table
employee_role table
```

↓

### 3️⃣ Employee logs in

```
/login
```

↓

### 4️⃣ Spring Security calls

```
loadUserByUsername()
```

↓

### 5️⃣ Password verified

↓

### 6️⃣ Employee accesses

```
GET /pendingWork
```

---

# ⭐ Important Insight

**"Why implement UserDetailsManager instead of UserDetailsService?"**

Answer:

> `UserDetailsService` only supports loading users for authentication. `UserDetailsManager` extends it and adds user management operations like createUser, updateUser, deleteUser, and changePassword, which allows applications to implement user registration and management features.


