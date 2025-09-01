# 🔑 Flow of Username/Password Authentication in Spring Security

### 1. User Sends Request

* Example: submits login form (`/login`) or sends a JSON request if we built custom.

### 2. **UsernamePasswordAuthenticationFilter**

* This is a filter in the **Spring Security filter chain**.
* It intercepts the request at `/login` (by default).
* Extracts `username` and `password` from the request.
* Creates an **unauthenticated** `UsernamePasswordAuthenticationToken` (constructor with only credentials, no authorities).
* Passes it to the `AuthenticationManager.authenticate()` method.

### 3. **AuthenticationManager**

* Think of it as a **dispatcher**.
* It doesn’t do the actual authentication itself.
* It **delegates** to one or more `AuthenticationProvider`s until one supports the authentication type.
* By default, it uses **DaoAuthenticationProvider** when you configure `UserDetailsService`.

### 4. **AuthenticationProvider** (e.g., DaoAuthenticationProvider)

* This is where the real work happens.
* Steps inside:

  1. Calls your `UserDetailsService.loadUserByUsername(username)` → loads `UserDetails` (with stored password, roles).
  2. Compares the **raw password** from the request with the **stored password** using `PasswordEncoder.matches()`.
  3. If match → creates a **fully authenticated** `UsernamePasswordAuthenticationToken` (this time includes authorities).

### 5. **AuthenticationManager Returns Auth Object**

* If provider returns authenticated token → success.
* Else → exception (`BadCredentialsException`, etc.).

### 6. **SecurityContextHolder**

* If successful → Spring Security stores the authenticated token in `SecurityContextHolder`.
* If session-based → `SecurityContext` is also tied to `HttpSession` (`JSESSIONID`).
* If stateless (JWT) → no session; token is only stored per request by our JWT filter.

# ✅ Correct Flow 

So it goes like this:

1. **User sends request with username/password.**
2. `UsernamePasswordAuthenticationFilter` intercepts.
3. Creates `UsernamePasswordAuthenticationToken` (unauthenticated).
4. Passes it to `AuthenticationManager`.
5. `AuthenticationManager` delegates to `AuthenticationProvider`.
6. `AuthenticationProvider` → calls `UserDetailsService.loadUserByUsername`.
7. If valid → returns authenticated `UsernamePasswordAuthenticationToken`.
8. Stored in `SecurityContextHolder`.

# 🔑 Spring Security Username/Password Authentication Flow

```
   [1] User Request
       (username + password)
                 │
                 ▼
   [2] UsernamePasswordAuthenticationFilter
       - Extracts credentials
       - Creates UNAUTHENTICATED
         UsernamePasswordAuthenticationToken
                 │
                 ▼
   [3] AuthenticationManager
       - Delegates to AuthenticationProvider
                 │
                 ▼
   [4] AuthenticationProvider (DaoAuthenticationProvider)
       - Calls UserDetailsService.loadUserByUsername(username)
       - Loads UserDetails (with stored password, roles)
       - Uses PasswordEncoder to compare passwords
                 │
         ┌───────┴────────┐
         │                │
   [5a] Success      [5b] Failure
   - Creates          - Throws
     AUTHENTICATED      BadCredentialsException
     UsernamePasswordAuthenticationToken
   - Includes roles
                 │
                 ▼
   [6] SecurityContextHolder
       - Stores Authentication object
       - If session-based → linked to JSESSIONID
       - If JWT (stateless) → our filter sets it manually
```

<img width="1053" height="545" alt="Screenshot 2025-08-27 at 12 38 33 AM" src="https://github.com/user-attachments/assets/1c901a94-f691-4ae9-957d-943e041c32e3" />

# ✅ Key Takeaways

* `UserDetailsService` is **not called first**.
* It is invoked **inside AuthenticationProvider** (after AuthenticationManager delegates).
* **UsernamePasswordAuthenticationFilter** is the entry point for form login/basic login.
* The **authenticated object** is finally stored in `SecurityContextHolder`.
* When we move to **JWT**, we bypass `UsernamePasswordAuthenticationFilter` after login. Instead, our **JWT filter** directly sets an         authenticated object into `SecurityContextHolder` if the token is valid.

---

# Important interfaces and their implementations

<img width="949" alt="Screenshot 2025-06-26 at 10 38 48 AM" src="https://github.com/user-attachments/assets/7176e701-acdf-4d11-952a-b98732dd02ef" />
<img width="1118" height="368" alt="Screenshot 2025-08-23 at 11 28 50 AM" src="https://github.com/user-attachments/assets/cd484b10-1ab7-4733-af62-253244765675" />
<img width="931" height="454" alt="Screenshot 2025-08-23 at 11 32 59 AM" src="https://github.com/user-attachments/assets/855a15d4-713b-4a0f-afc4-720ce6a36e52" />
<img width="742" height="425" alt="Screenshot 2025-08-23 at 12 00 06 PM" src="https://github.com/user-attachments/assets/2b358531-897d-4262-b8e7-18134d581da5" />
<img width="834" height="390" alt="Screenshot 2025-08-23 at 11 54 25 AM" src="https://github.com/user-attachments/assets/dc7fd9ad-305e-42e6-932b-f567f70ef77d" />
<img width="845" height="370" alt="Screenshot 2025-08-23 at 11 59 09 AM" src="https://github.com/user-attachments/assets/611ca4fb-c273-4012-b6e6-59b0b3a8cbc6" />
<img width="1024" height="522" alt="Screenshot 2025-08-23 at 12 01 16 PM" src="https://github.com/user-attachments/assets/18b1eee5-279b-4a9a-8b89-84626bda637f" />

## User Schema

<img width="1079" height="412" alt="Screenshot 2025-08-25 at 11 42 12 AM" src="https://github.com/user-attachments/assets/b23ea2da-dc99-443f-841d-5dc29d7c6352" />

---







