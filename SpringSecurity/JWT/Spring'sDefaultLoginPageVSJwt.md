# 🔑 With Spring’s Default Login Page

1. **User opens `/login`** → enters username & password.
2. Spring Security takes the username/password →
   calls your `UserDetailsService.loadUserByUsername()`.
3. `UserDetailsService` returns a `UserDetails` object (with username, password, roles).
4. **AuthenticationManager** delegates to an **AuthenticationProvider** (usually `DaoAuthenticationProvider`).
5. This provider compares the entered password with the stored password (using a `PasswordEncoder`).
6. If valid → an `Authentication` object (like `UsernamePasswordAuthenticationToken`) is created and stored in `SecurityContextHolder`.
7. After that → session is created, and a `JSESSIONID` is given to the client to track the session.

So Spring gives us a **session-based login out-of-the-box**.

---

# 🔑 With JWT (Custom Flow We’re Building)

We’re **replacing session management** with **tokens**.

1. **User hits `/auth/login` (our API)** with username/password.
2. We still use `AuthenticationManager` + `UserDetailsService` to verify credentials.
   👉 Same as default login page!
3. If valid → instead of creating a session, **we create a JWT** (our own work).
4. Return JWT to the client (in JSON).
5. For every request:

   * Client sends `Authorization: Bearer <token>`.
   * Our **JWT filter** validates the token (check signature, expiration).
   * If valid → we manually build `UsernamePasswordAuthenticationToken` and set it in `SecurityContextHolder`.
   * No session, no JSESSIONID, everything is stateless.

---


