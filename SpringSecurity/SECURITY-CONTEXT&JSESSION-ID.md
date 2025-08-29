# How Spring Security tracks logged-in users?

---

## 🧩 What is `SecurityContext`?

* It’s a simple **holder object** that stores the current user’s `Authentication` object.
* Internally:

  ```java
  public interface SecurityContext {
      Authentication getAuthentication();
      void setAuthentication(Authentication authentication);
  }
  ```
* It lives in a **thread-local storage** during request processing (`SecurityContextHolder`).

---

## 🧩 What is inside `Authentication` after username/password login?

After successful authentication (`UsernamePasswordAuthenticationFilter` → `AuthenticationManager` → `DaoAuthenticationProvider`):

* An **`Authentication` object** is created (usually a `UsernamePasswordAuthenticationToken`).
* It typically contains:

  * **Principal** (the `UserDetails` object, holding username, password=null, and authorities).
  * **Credentials** (password, but usually set to `null` after authentication for security reasons).
  * **Authorities** (roles/permissions of the user).
  * `authenticated = true`.

Example:

```java
UsernamePasswordAuthenticationToken(
    principal = User(username="john", password="[PROTECTED]", authorities=[ROLE_USER]),
    credentials = null,
    authorities = [ROLE_USER]
)
```

---

## 🧩 What about `JSESSIONID`?

Here’s the critical part:

* After authentication succeeds, Spring Security doesn’t just keep the `SecurityContext` in memory (that would be lost between requests).
* Instead, it uses the **`HttpSession`** (backed by `JSESSIONID`) to persist the `SecurityContext`.
* The filter responsible is **`SecurityContextPersistenceFilter`**.

Flow:

1. On first successful login:

   * `SecurityContext` (with `Authentication`) is stored in the `HttpSession`.
   * Server issues a `JSESSIONID` cookie to the client.

2. On subsequent requests:

   * Client sends back `JSESSIONID` cookie.
   * `SecurityContextPersistenceFilter` loads the `SecurityContext` from the `HttpSession`.
   * Now, the user is considered authenticated without re-entering username/password.

---

## 🧩 So what gets checked on the next request?

* **NOT** username/password again.
* **YES** → Spring Security:

  * Reads `JSESSIONID` from cookie.
  * Looks up the corresponding session in the server.
  * Loads the `SecurityContext` (with the `Authentication` object) from that session.
  * Attaches it to the current thread (`SecurityContextHolder`).

So authentication is effectively **“remembered” via the session**.

---

## 🖼️ Flow Diagram

### First Login:

```
[Login request (username, password)]
   ↓
AuthenticationManager validates
   ↓
Authentication object created
   ↓
Stored in SecurityContext
   ↓
SecurityContext saved in HttpSession
   ↓
Server issues JSESSIONID to client
```

### Next Request:

```
[Request with JSESSIONID cookie]
   ↓
Server finds HttpSession
   ↓
SecurityContextPersistenceFilter loads SecurityContext
   ↓
SecurityContextHolder now has Authentication
   ↓
User treated as logged in (no need for password)
```

---

## ✅ In Short

* **SecurityContext** → holds the `Authentication` object (user details, authorities).
* **After login** → it holds principal, credentials=null, authorities.
* **JSESSIONID** → links client to server-side session.
* **Next requests** → Spring checks JSESSIONID, retrieves SecurityContext, reuses the stored Authentication (doesn’t check password again).

---

# 🧩 Multiple Sessions and SecurityContexts

* Each user who logs in gets their **own `HttpSession`** on the server.
* Inside that session, Spring Security stores the **`SecurityContext`**.
* So you can imagine it like this on the server:

```
JSESSIONID=abc123  → HttpSession{ SecurityContext{ Authentication(user=john, roles=[USER]) } }
JSESSIONID=xyz456  → HttpSession{ SecurityContext{ Authentication(user=alice, roles=[ADMIN]) } }
JSESSIONID=pqr789  → HttpSession{ SecurityContext{ Authentication(user=bob, roles=[USER, MANAGER]) } }
```

---

## 🧩 Flow on Each Request

1. Client sends `JSESSIONID` cookie with request.
2. Server looks up the `HttpSession` object corresponding to that `JSESSIONID`.
3. `SecurityContextPersistenceFilter` retrieves the `SecurityContext` from that session.
4. That `SecurityContext` is bound to the **current thread** (via `SecurityContextHolder`).
5. Controllers and Spring Security authorization checks use that `Authentication` object.

---

## 🧩 Important Notes

* If you **invalidate the session** (e.g., on logout), that `SecurityContext` is removed → user must log in again.
* By default, **one user = one session**, but you can configure concurrency control in Spring Security to allow/restrict multiple sessions per user.
* At any given time, the server may be holding **many `HttpSession`s**, each with its own `SecurityContext`.

---
