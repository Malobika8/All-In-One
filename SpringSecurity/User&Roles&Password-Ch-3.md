# Spring Security: Users, Roles & Passwords

**Focus:** how users are represented, how roles/authorities work, how to create users (in‑memory), and how passwords are handled.

---

## 0) Goal & Mental Model

* Add **users** to the app.
* Protect URLs using **roles/authorities**.
* Store users **in memory** for now (good for learning/testing).
* Use a proper **password encoder** (BCrypt) and know the quick dev shortcut (`{noop}`).

**Big picture**

```
Login form / HTTP Basic
        ↓
Creates Authentication (username+password)
        ↓
AuthenticationManager → AuthenticationProvider
        ↓
UserDetailsService / UserDetailsManager → loads user
        ↓
Compare password with PasswordEncoder → success/failure
        ↓
On success: SecurityContextHolder stores Authentication (via session)
```

---

## 1) Core Concepts

### 1.1 `UserDetails`

<img width="1118" height="368" alt="Screenshot 2025-08-23 at 11 28 50 AM" src="https://github.com/user-attachments/assets/4381444f-74e5-408c-981c-40f43824f83d" />

Represents one user. Key parts:

* `getUsername()`
* `getPassword()` (encoded)
* `getAuthorities()` → a `Collection<GrantedAuthority>`
* Account flags: `isAccountNonExpired()`, `isAccountNonLocked()`, `isCredentialsNonExpired()`, `isEnabled()`

I can either **implement `UserDetails`** myself or use the built‑in **`org.springframework.security.core.userdetails.User`**.

<img width="931" height="454" alt="Screenshot 2025-08-23 at 11 32 59 AM" src="https://github.com/user-attachments/assets/94cb0090-891a-44cc-8ecb-2ce380551552" />

### 1.2 Authorities vs Roles

* **Authority**: any string like `"READ_REPORTS"`, `"ROLE_ADMIN"`.
* **Role**: a special authority that **conventionally starts with `ROLE_`**.

**Important rule:**

* `hasRole("ADMIN")` under the hood checks for authority `"ROLE_ADMIN"`.
* `hasAuthority("ROLE_ADMIN")` checks exactly that string.

So either write:

```java
httpSecurity.authorizeHttpRequests()
  .requestMatchers("/admin/**").hasRole("ADMIN")  // adds ROLE_ automatically
  .requestMatchers("/reports/**").hasAuthority("READ_REPORTS")
  .anyRequest().authenticated();
```

### 1.3 `GrantedAuthority` & `SimpleGrantedAuthority`

* One user can have many authorities.
* `SimpleGrantedAuthority("ROLE_USER")` or `new SimpleGrantedAuthority("READ_REPORTS")`.

<img width="1122" height="138" alt="Screenshot 2025-08-23 at 11 45 27 AM" src="https://github.com/user-attachments/assets/12047448-93ec-4fbb-89f8-9685c745d79b" />
<img width="923" height="474" alt="Screenshot 2025-08-23 at 11 48 44 AM" src="https://github.com/user-attachments/assets/8e95fdcf-33e2-4a38-b86f-f57747bd4ed6" />

### 1.4 `UserDetailsService` vs `UserDetailsManager`

* `UserDetailsService` → **read‑only**: `loadUserByUsername()`
* `UserDetailsManager` → read + **CRUD** (create/update/delete users)

  * **`InMemoryUserDetailsManager`** is the in‑memory implementation (perfect for today).
 
<img width="834" height="390" alt="Screenshot 2025-08-23 at 11 54 25 AM" src="https://github.com/user-attachments/assets/2f91e8db-f3d1-428e-a9f1-28286e7c2005" />
<img width="742" height="425" alt="Screenshot 2025-08-23 at 12 00 06 PM" src="https://github.com/user-attachments/assets/e06a2244-36c2-4b38-a40e-46d2291baaab" />
<img width="845" height="370" alt="Screenshot 2025-08-23 at 11 59 09 AM" src="https://github.com/user-attachments/assets/195e8403-ff6c-41bd-990d-d75313d0cfc6" />
<img width="1024" height="522" alt="Screenshot 2025-08-23 at 12 01 16 PM" src="https://github.com/user-attachments/assets/b490dfe0-2560-4030-a583-98b425d31127" />

When we try to login,

<img width="509" height="290" alt="Screenshot 2025-08-23 at 12 02 11 PM" src="https://github.com/user-attachments/assets/082545ce-b2c1-4faf-9134-ce6a9bf3debe" />
<img width="943" height="432" alt="Screenshot 2025-08-23 at 12 02 23 PM" src="https://github.com/user-attachments/assets/7965e91d-009a-4222-b684-eaafbcefa836" />

### 1.5 Password encoding

* **Never store plain text** in real apps.
* Use `BCryptPasswordEncoder` (production‑safe choice).
* For quick dev/testing: `{noop}` (or `NoOpPasswordEncoder`), but **never** for prod.

<img width="809" height="485" alt="Screenshot 2025-08-23 at 12 03 16 PM" src="https://github.com/user-attachments/assets/7276c1cd-b8d2-4409-a6e9-5cbc41e48cee" />
<img width="1105" height="561" alt="Screenshot 2025-08-23 at 12 03 50 PM" src="https://github.com/user-attachments/assets/e4d4dd04-154e-420a-9a95-d4ff5fd39761" />
<img width="556" height="339" alt="Screenshot 2025-08-23 at 12 04 00 PM" src="https://github.com/user-attachments/assets/87de1f99-8b9b-4628-af21-e2d8e9446fd7" />
<img width="1032" height="560" alt="Screenshot 2025-08-23 at 12 04 10 PM" src="https://github.com/user-attachments/assets/338e20c8-56f0-473d-8957-0372f4c380a0" />
<img width="948" height="499" alt="Screenshot 2025-08-23 at 12 04 50 PM" src="https://github.com/user-attachments/assets/16bead2a-7b1e-4c54-85cf-102ec51e7652" />

We'll try to login again,

<img width="907" height="390" alt="Screenshot 2025-08-23 at 12 05 27 PM" src="https://github.com/user-attachments/assets/ae9e0c02-9f62-4c26-8555-ea6e35cd6d1a" />
<img width="364" height="103" alt="Screenshot 2025-08-23 at 12 05 38 PM" src="https://github.com/user-attachments/assets/50032935-8283-49f7-aac6-51bf93486868" />

---

## 2) Minimal Working Setup (in‑memory users). 

**We can use builder pattern to create User.**

We’ll define:

1. a `PasswordEncoder`
2. a `UserDetailsService` / `UserDetailsManager` bean with users
3. authorization rules in `SecurityFilterChain` (optional as of now)

```java
// src/main/java/com/example/security/SecurityConfig.java
package com.example.security;

import org.springframework.context.annotation.*;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.core.userdetails.User;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.provisioning.InMemoryUserDetailsManager;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;

@Configuration
@EnableWebSecurity
public class SecurityConfig {

  // 1) Password encoder (BCrypt)
  @Bean
  public PasswordEncoder passwordEncoder() {
    return new BCryptPasswordEncoder();
  }

  // 2) Users (in-memory)
  @Bean
  public UserDetailsService userDetailsService(PasswordEncoder encoder) {
    UserDetails user = User.builder()
        .username("user")
        .password(encoder.encode("user123"))
        .roles("USER")              // becomes authority ROLE_USER
        .build();

    UserDetails admin = User.builder()
        .username("admin")
        .password(encoder.encode("admin123"))
        .roles("ADMIN", "USER")     // ROLE_ADMIN + ROLE_USER
        .authorities("READ_REPORTS") // extra fine-grained authority
        .build();

    return new InMemoryUserDetailsManager(user, admin);
  }

  // 3) Authorization rules + login
  @Bean
  public SecurityFilterChain securityFilterChain(HttpSecurity httpSecurity) throws Exception {
    httpSecurity
      .authorizeHttpRequests()
        .requestMatchers("/", "/public/**").permitAll()
        .requestMatchers("/admin/**").hasRole("ADMIN")
        .requestMatchers("/reports/**").hasAuthority("READ_REPORTS")
        .anyRequest().authenticated();
    httpSecurity.formLogin()       // default login page
    httpSecurity.httpBasic();      // enable Basic for curl/testing

    return http.build();
  }
}
```

---

## 3) Dev shortcut: `{noop}` (only for learning!)

If I don’t want to configure a real encoder yet:

```java
@Bean
public UserDetailsService userDetailsService() {
  UserDetails demo = User.withUsername("demo")
    .password("{noop}demo123")   // ← plain text for quick tests ONLY
    .roles("USER")
    .build();
  return new InMemoryUserDetailsManager(demo);
}
```

**Common error:** `There is no PasswordEncoder mapped for the id "null"` → Happens when the password **doesn’t** have a prefix like `{noop}`, `{bcrypt}`, and no encoder is configured. Fix by either:

* Using `{noop}plainPassword` **or**
* Defining a `PasswordEncoder` and using `encoder.encode("password")`.

---

## 4) URL Authorization Examples (roles vs authorities)

```java
httpSecurity.authorizeHttpRequests()
  .requestMatchers("/profile/**").hasAnyRole("USER", "ADMIN")
  .requestMatchers("/manage/**").hasAuthority("ROLE_ADMIN")  // explicit authority
  .requestMatchers("/ops/**").hasAnyAuthority("DEPLOY", "ROLLBACK")
  .anyRequest().authenticated();
```

**Cheat sheet**

* `hasRole("ADMIN")` ⇢ expects authority `ROLE_ADMIN`.
* `hasAuthority("ROLE_ADMIN")` ⇢ checks the exact string.
* Prefer roles for broad access, authorities for finer permissions.

---

## 5) What happens after login (session basics)

After success, Spring Security stores the `Authentication` in the **session** so we don’t re‑login for each request.

```mermaid
sequenceDiagram
  participant U as User
  participant F as Security Filter Chain
  participant A as Auth Manager/Provider
  participant S as Session (JSESSIONID)

  U->>F: POST /login (username, password)
  F->>A: Authenticate(token)
  A-->>F: Success (Authentication)
  F->>S: Save SecurityContext
  F-->>U: 302 Redirect to originally requested URL
  U->>F: GET protected page (with JSESSIONID cookie)
  F-->>U: 200 OK (controller runs)
```

> In modern Spring Security, the `SecurityContext` is associated with the HTTP session by default. Logging out invalidates it.

---

## 6) Troubleshooting (typical)

* **`There is no PasswordEncoder mapped for the id "null"`** → use `{noop}` for quick tests or configure a `PasswordEncoder` and encode passwords.
* **Can’t access admin URL even as admin** → check that you used `hasRole("ADMIN")` (not `hasAuthority("ADMIN")`), or ensure your user actually has `ROLE_ADMIN`.
* **Login always fails** → verify the username, encoded password, and that the same encoder is used both to store and to match.

---

## 7) Recap

* `UserDetails` models the user; `GrantedAuthority` models permissions.
* Roles are just authorities with `ROLE_` prefix; `hasRole("X")` ⇒ checks `ROLE_X`.
* Use `InMemoryUserDetailsManager` for quick starts.
* Prefer `BCryptPasswordEncoder` for real encoding; `{noop}` only for learning.
* After login, the session holds the `SecurityContext` so we stay authenticated.
