# Spring Security

> **Focus**: Customizing HTTP Security & Filter Chains, controlling endpoint access, roles, supporting browser vs REST clients, and migrating to Spring Security 6.1’s Lambda DSL.

---

## 1) Default Security & Filter Chain Recap

* With Spring Boot + Spring Security:

  * **All endpoints are secured by default** → any request requires authentication.
  * Two key filters enabled automatically:

    * **Form Login filter** → default login page for browser users.
    * **HTTP Basic filter** → supports REST clients (e.g., Postman, cURL).
* This is all driven by the **default SecurityFilterChain** created by Spring Security.

### Important:

If you **do not** override the `SecurityFilterChain` bean, Spring Security still provides:

* Default login page (auto‑generated).
* Authorization requirement for every endpoint.
* Both **form login** and **HTTP Basic** enabled by default.

<img width="1047" height="322" alt="Screenshot 2025-08-24 at 8 56 45 PM" src="https://github.com/user-attachments/assets/ce691de8-65ce-46c5-9a7a-66bedef3d592" />

Even without writing this code, Spring Boot auto‑configures the above behavior internally.

### Diagram — Request Flow with Default Filters

```
Request → DelegatingFilterProxy → FilterChainProxy → [Security Filters]
   • UsernamePasswordAuthenticationFilter (form login)
   • BasicAuthenticationFilter (HTTP Basic)
   • … other filters (CSRF, session, etc.)
→ Controller (if authenticated)
```

---

### 1.1 What if you **don’t** define a `SecurityFilterChain` bean? (Defaults)

* Spring Boot auto-configures a **default** chain that:

  * **Requires authentication for every request** (`anyRequest().authenticated()`).
  * Exposes **default form login** (browser users) and **HTTP Basic** (REST clients).
  * Keeps standard protections (CSRF, headers, session management) enabled.

**Minimal setup (let Boot provide the defaults):**

> Define only users and a `PasswordEncoder`. **Do not** declare a `SecurityFilterChain` bean.

<img width="1111" height="411" alt="Screenshot 2025-08-24 at 8 52 12 PM" src="https://github.com/user-attachments/assets/fb38449d-8895-46f1-91ca-efb30d617be5" />

**What you’ll see:** visiting any endpoint → redirect to **default login page**; APIs accept **Basic Auth**; once logged in, requests are authorized.

**Equivalent explicit config (what the default *effectively* does):**

<img width="1047" height="322" alt="Screenshot 2025-08-24 at 8 56 45 PM" src="https://github.com/user-attachments/assets/34ef3430-e642-4e53-8a07-83a9ee88d5a5" />

**Diagram — No custom chain → Boot defaults**

```
(No SecurityFilterChain bean)
         │
         ▼
Spring Boot Auto-Config
         │
         ▼
anyRequest().authenticated()
+ formLogin() + httpBasic()
+ standard protections
```

## 2) Overriding the Default Filter Chain

* If you declare your own `SecurityFilterChain` bean, **you override the default**.
* This gives full control: you decide which endpoints are secured, what authentication methods are enabled, etc.

**Example — Custom Filter Chain (Spring Security 6.1 DSL)**

<img width="972" height="450" alt="Screenshot 2025-08-24 at 8 59 10 PM" src="https://github.com/user-attachments/assets/bde367e3-cffe-4187-9090-e8c5c2fe3727" />

### Key Methods

* `.authenticated()` → request must be from a logged-in user.
* `.permitAll()` → anyone can access, no login required.
* `.denyAll()` → blocks access entirely.

> Without `.formLogin()` or `.httpBasic()`, those auth methods are disabled.

---

## 3) Endpoint Authorization Control

* Apply different rules to different URL patterns.
* Examples:

<img width="972" height="450" alt="Screenshot 2025-08-24 at 8 59 10 PM" src="https://github.com/user-attachments/assets/d4fac4b6-4b2a-4161-b4ab-44bc1b940b2f" />

* Useful for separating **public docs**, **admin-only areas**, or **internal system endpoints**.

---

## 4) Supporting Different Clients

* **Browser Clients:** Use form login → user sees a login page.
* **REST Clients (Postman/cURL):** Use HTTP Basic → credentials sent in headers.

Activating both filters (`formLogin`, `httpBasic`) supports both flows simultaneously.

---

## 5) Version Compatibility & Migration to 6.1 DSL

* **Problem:** Old API (`http.authorizeHttpRequests().anyRequest().authenticated()`) with chained methods is **deprecated** in Spring Security 6.1.
* **Solution:** Use **Lambda DSL style** for better readability and forward-compatibility.

<img width="1038" height="486" alt="Screenshot 2025-08-24 at 8 24 49 PM" src="https://github.com/user-attachments/assets/c587d74f-7144-41ef-a273-b1dcc1c8fa6a" />
<img width="897" height="552" alt="Screenshot 2025-08-24 at 8 25 26 PM" src="https://github.com/user-attachments/assets/98cbc10c-a831-4b58-ac68-1b3a79a69872" />

### Before (pre-6.1 style)

```java
http
  .authorizeHttpRequests()
  .requestMatchers("/admin/**").hasRole("ADMIN")
  .anyRequest().authenticated()
  .and()
  .formLogin()
  .and()
  .httpBasic();
```

<img width="972" height="450" alt="Screenshot 2025-08-24 at 8 59 10 PM" src="https://github.com/user-attachments/assets/e3fb5b57-36d2-43ca-9cb6-f4a7934568e4" />

### After (6.1 Lambda DSL)

<img width="1031" height="488" alt="Screenshot 2025-08-24 at 8 27 42 PM" src="https://github.com/user-attachments/assets/0fbb6d22-8ff4-4c3c-96d2-92ee19fed03f" />
<img width="1140" height="377" alt="Screenshot 2025-08-24 at 8 27 59 PM" src="https://github.com/user-attachments/assets/e96738a2-4a67-40d8-9ef0-b6750e063026" />
<img width="1110" height="430" alt="Screenshot 2025-08-24 at 8 29 21 PM" src="https://github.com/user-attachments/assets/7755bfec-6fdc-42f4-bd96-485ab8f44242" />
<img width="848" height="552" alt="Screenshot 2025-08-24 at 8 29 39 PM" src="https://github.com/user-attachments/assets/730546fc-a5d6-4ed6-b8a9-ada687b03d2d" />
<img width="1062" height="372" alt="Screenshot 2025-08-24 at 8 30 42 PM" src="https://github.com/user-attachments/assets/4cedb307-cf94-4964-ba1c-beaa1d1f60ac" />
<img width="1115" height="433" alt="Screenshot 2025-08-24 at 8 31 05 PM" src="https://github.com/user-attachments/assets/498b1f4f-9970-4751-a370-76b256e5fd57" />
<img width="1062" height="379" alt="Screenshot 2025-08-24 at 8 31 26 PM" src="https://github.com/user-attachments/assets/2702591f-5e07-4fc4-9b5b-dc6ceeb6f4fe" />
<img width="826" height="409" alt="Screenshot 2025-08-24 at 8 31 53 PM" src="https://github.com/user-attachments/assets/b32d561d-089b-4dcc-a031-d6cf1d4c66ac" />
<img width="1123" height="644" alt="Screenshot 2025-08-24 at 8 32 17 PM" src="https://github.com/user-attachments/assets/9e2bf095-43f7-400d-8c9f-21e522cf97d8" />
<img width="1249" height="639" alt="Screenshot 2025-08-24 at 8 32 34 PM" src="https://github.com/user-attachments/assets/e3c81320-4572-4050-a297-d2e7953c2330" />
<img width="1091" height="577" alt="Screenshot 2025-08-24 at 8 32 58 PM" src="https://github.com/user-attachments/assets/03e779fd-33bb-4198-b339-a29a124d6f01" />

When you don't want to use the Spring login form,

<img width="1121" height="601" alt="Screenshot 2025-08-24 at 8 33 15 PM" src="https://github.com/user-attachments/assets/918d0f12-9a03-461f-9f09-8a4fc4873076" />

We can also write like this,

<img width="1107" height="185" alt="Screenshot 2025-08-24 at 8 36 28 PM" src="https://github.com/user-attachments/assets/1e3180b3-53ce-41a0-a01d-2289862a69e0" />
<img width="850" height="181" alt="Screenshot 2025-08-24 at 8 37 35 PM" src="https://github.com/user-attachments/assets/f0054756-bc7c-4a63-a049-86b289e4466d" />

```java
http
  .authorizeHttpRequests(auth -> auth
      .requestMatchers("/admin/**").hasRole("ADMIN")
      .anyRequest().authenticated()
  )
  .formLogin(Customizer.withDefaults())
  .httpBasic(Customizer.withDefaults());
```

### Visual Diagram — API Migration

```
Old Style (Pre-6.1)         →        New Style (6.1 Lambda DSL)
--------------------------------------------------------------
.authorizeHttpRequests()    →   .authorizeHttpRequests(auth -> { ... })
   .anyRequest().authenticated()  →   auth.anyRequest().authenticated()
.and()                      →   (removed, no longer needed)
.formLogin()                →   .formLogin(Customizer.withDefaults())
.httpBasic()                →   .httpBasic(Customizer.withDefaults())
```

**Benefits:**

* More concise.
* Removes need for `.and()`.
* Future-proof (old style will be removed in Spring Security 7).

---

### Visual map: Old → New (Lambda DSL)

```
[Old DSL]
authorizeRequests()
  .antMatchers("/admin/**").hasRole("ADMIN")
  .anyRequest().authenticated()
  .and().formLogin()
  .and().httpBasic();

        ↓  (migrate)

[New Lambda DSL]
authorizeHttpRequests(auth -> auth
  .requestMatchers("/admin/**").hasRole("ADMIN")
  .anyRequest().authenticated()
)
.formLogin(Customizer.withDefaults())
.httpBasic(Customizer.withDefaults());
```

**Cheat‑sheet mapping**

| Concept     | Pre‑6.1                           | 6.1+ Lambda DSL                         |
| ----------- | --------------------------------- | --------------------------------------- |
| Entry point | `authorizeRequests()`             | `authorizeHttpRequests(auth -> …)`      |
| Matchers    | `antMatchers()` / `mvcMatchers()` | `requestMatchers()`                     |
| Permit/deny | `.permitAll()`, `.denyAll()`      | same                                    |
| Roles       | `.hasRole("X")`                   | same (checks `ROLE_X`)                  |
| Authorities | `.hasAuthority("A")`              | same                                    |
| Chaining    | `.and()` between blocks           | **removed**; continue at top level      |
| Form login  | `.formLogin()`                    | `.formLogin(Customizer.withDefaults())` |
| Basic auth  | `.httpBasic()`                    | `.httpBasic(Customizer.withDefaults())` |

## 6) Role-Based Access Control (RBAC)

* Restrict access to endpoints based on roles.
* Example:

```java
.requestMatchers("/admin/**").hasRole("ADMIN")
```

* Reminder: Roles internally map to authorities with `ROLE_` prefix.
* Example: `hasRole("ADMIN")` → checks for authority `ROLE_ADMIN`.

---

## 7) Handling Common Issues

* **Missing beans (e.g., PasswordEncoder, UserDetailsService)** → must be defined manually if you customize beyond defaults.
* **Endpoints unprotected after override** → you replaced default chain, so explicitly configure protections.
* **Version mismatches** → ensure Spring Boot version aligns with Spring Security version.

  * Example: Spring Boot 3.1.x works with Spring Security 6.1.x.

---

## 8) Self‑check Questions

* What happens if you define your own `SecurityFilterChain`?
* Difference between `permitAll()`, `authenticated()`, `denyAll()`?
* Why activate both `.formLogin()` and `.httpBasic()`?
* How does the Lambda DSL differ from the older style?

---

## Quick Diagram — Endpoint Security Rules

```
URL Pattern        Rule
---------------------------------
/public/**         permitAll()
/admin/**          hasRole("ADMIN")
/api/**            authenticated()
/internal/**       denyAll()
```

---

