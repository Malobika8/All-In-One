# Spring Security

> Goal: Understand the *core pieces* only — enable security, filters (mental model), user representation, roles/authorities, creating users, password encoding, and in‑memory storage. **No custom authorization rules or custom login yet.**

---

## 1) What does Spring Security turn on?

* A **Security Filter Chain** is registered in the Servlet container. Every HTTP request passes through this chain before reaching your controllers.
* Out of the box (with Spring Boot):

  * **All endpoints require authentication** by default.
  * **Default login & logout pages** are provided.
  * **CSRF protection** and common security headers are enabled.
  * You don’t have to list every filter; Spring Security wires the chain for you.

### Mental model of the filter chain

1. Request enters the container and hits the **DelegatingFilterProxy**.
2. It delegates to Spring Security’s **FilterChainProxy**.
3. A series of filters run (context setup, auth attempt, session management, CSRF, etc.).
4. If authentication succeeds, the request proceeds to your controller; otherwise it’s redirected to the login page or challenged.

> You don’t need to memorize filter names yet—just know there’s an ordered pipeline that guards requests.

---

## 2) How users are represented

* **`UserDetails`**: contract that describes a user — username, password, **authorities**, and account flags (enabled, locked, expired, credentialsExpired).
* **`User`**: a built‑in implementation of `UserDetails` that you can use directly for simple cases.
* **`GrantedAuthority`**: represents a single permission/authority string.

### Roles vs Authorities (quick, practical)

* A **role** is a convention for a set of authorities. In code we usually assign roles like `ADMIN`, `USER`.
* Internally, roles are stored as authorities prefixed with `ROLE_` (e.g., role `ADMIN` → authority `ROLE_ADMIN`).
* When you later write authorization rules (not in this step), `hasRole("ADMIN")` is just sugar for `hasAuthority("ROLE_ADMIN")`.

---

## 3) Creating users with the Builder

You can create `UserDetails` instances using the fluent **builder**. Two common patterns:

**A. Quick demo (plain text password — only for learning!)**

```java
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;

UserDetails admin = User.withUsername("admin")
        .password("{noop}admin123")   // {noop} = no encoding (demo only)
        .roles("ADMIN")                // becomes authority ROLE_ADMIN
        .build();
```

**B. Proper encoding with BCrypt (recommended)**

```java
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;

var encoder = new BCryptPasswordEncoder();

UserDetails user = User.builder()
        .username("alice")
        .passwordEncoder(encoder::encode) // applies BCrypt to the next password
        .password("alice123")
        .roles("USER")
        .build();
```

> Tip: The builder sets sensible defaults (enabled = true, not locked/expired) unless you change them.

---

## 4) In‑memory user store (for practice/testing only)

* **`InMemoryUserDetailsManager`** keeps users in a `Map` in memory. Fast to start, but **not persistent** (users disappear on restart).

```java
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.core.userdetails.UserDetailsService;

UserDetailsService users = new InMemoryUserDetailsManager(admin, user);
```

> Suitable for demos and local dev. For real apps you’ll switch to JDBC/LDAP/custom stores later.

---

## 5) Password encoding — the essential idea

* **Never store raw passwords.** Hash them.
* Use a `PasswordEncoder` implementation like **`BCryptPasswordEncoder`**.
* Matching is done by `passwordEncoder.matches(raw, encoded)` during login.

```java
import org.springframework.context.annotation.Bean;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;

@Bean
PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
}
```

> `{noop}` is OK only while learning. Prefer BCrypt for anything you keep longer than a demo.

---

## 6) Minimal Spring Boot setup (keeping defaults)

> We **won’t** add any authorization rules or custom login here.

Create a configuration class that **only** defines users and a password encoder. Don’t define your own `SecurityFilterChain` bean yet — let Spring Boot keep its secure defaults (auth required for all endpoints + default login page).

```java
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;

@Configuration
class SecurityUsersConfig {

    @Bean
    PasswordEncoder passwordEncoder() { return new org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder(); }

    @Bean
    UserDetailsService userDetailsService(PasswordEncoder encoder) {
        UserDetails admin = User.builder()
                .username("admin")
                .passwordEncoder(encoder::encode)
                .password("admin123")
                .roles("ADMIN")
                .build();

        UserDetails user = User.builder()
                .username("alice")
                .passwordEncoder(encoder::encode)
                .password("alice123")
                .roles("USER")
                .build();

        return new InMemoryUserDetailsManager(admin, user);
    }
}
```

**What you’ll observe now**

* App starts with Spring Security active.
* Visiting any endpoint redirects you to the **default login page**.
* You can log in with `admin/admin123` or `alice/alice123`.

---

## 7) Quick authentication flow (just enough detail)

1. Username/password submitted to the login endpoint.
2. Spring loads the `UserDetails` via your `UserDetailsService`.
3. Raw password is checked against the encoded password using `PasswordEncoder.matches(...)`.
4. On success, the **SecurityContext** holds the authenticated principal for the rest of the request.

---

## 8) When *not* to use in‑memory users

* Any environment where restarts can happen (you’ll lose users).
* If you need to create/update users dynamically.
* If you must comply with password policies, audits, or integrations.

> Next steps (later videos): JDBC/LDAP stores, adding **authorization rules**, method security, and token‑based flows (JWT/OAuth2).

---

## Self‑check (keep it short)

* What’s the difference between a **role** and an **authority**?
* Where are in‑memory users kept and what happens on restart?
* Why use **BCrypt** instead of `{noop}`?
* At this stage, who provides the **login page**?

---

### Tiny troubleshooting

* **Login fails even with correct password** → ensure you encoded the stored password with the same `PasswordEncoder` you configured.
* **No login page shown** → if you created your own `SecurityFilterChain` and removed defaults, you must explicitly enable `formLogin()` (save for later step). For now, avoid defining a custom chain.

---


