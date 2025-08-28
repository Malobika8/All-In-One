## 🔑 Steps for JWT Authentication in Spring Security

<img width="1024" height="1536" alt="image" src="https://github.com/user-attachments/assets/c63eb01f-e032-4cf4-b69d-cf1574716b4c" />

### **1. User login**

* User sends **username + password** to `/login`.

### **2. Authenticate credentials**

* Server uses `AuthenticationManager` → verify username & password against DB (via `UserDetailsService`).

### **3. If valid, generate JWT**

* **Step 3.1**: Create `Instant now = Instant.now();` → current time.
* **Step 3.2**: Set expiry `exp = now + 15 min (or any duration)`.
* **Step 3.3**: Add **claims** (extra data like roles, email, userId). → `setClaims(Map)`.
* **Step 3.4**: Add **subject** (username or user id). → `setSubject(user.getUsername())`.
* **Step 3.5**: Add **issuer** (your app name). → `setIssuer("myApp")`.
* **Step 3.6**: Add issue date. → `setIssuedAt(Date.from(now))`.
* **Step 3.7**: Add expiry date. → `setExpiration(Date.from(exp))`.
* **Step 3.8**: Sign with secret key and algorithm (HS256, RS256). → `signWith(key, SignatureAlgorithm.HS256)`.
* **Step 3.9**: Build final compact string. → `.compact()`.

👉 This gives you the **JWT string** to return to client.

---

### **4. Send token back**

* Return JWT in response body or `Authorization: Bearer <token>` header.

---

### **5. Client stores token**

* Usually in localStorage/sessionStorage (never in cookies if avoiding CSRF).

---

### **6. Client calls other APIs**

* Every request → attach `Authorization: Bearer <token>` header.

---

### **7. Validate token in server filter**

* Intercept request with `JwtAuthenticationFilter`.
* Extract token from header.
* Verify signature with same secret key.
* Check expiry date.
* Extract username + roles from claims.

---

### **8. Build authentication object**

* If token is valid → create `UsernamePasswordAuthenticationToken`.
* Store it in `SecurityContextHolder`.
* Now Spring Security knows the user is authenticated.

---

### **9. Controller executes**

* Secured endpoints see user info (`@AuthenticationPrincipal` or `SecurityContextHolder`).
* Request proceeds normally.

---

⚡ So the **core JWT creation steps** you saw:
`setClaims` → put extra user info
`setSubject` → main identifier (username/userId)
`setIssuer` → app/service issuing the token
`setIssuedAt` → time now
`setExpiration` → expiry limit
`signWith` → secret key + algorithm
`compact()` → build final token

---

# 🟢 JWT (JSON Web Token) Authentication – Step by Step

## 1. **User Logs In**

* The client (browser / mobile app / Postman) sends:

  ```json
  { "username": "alice", "password": "password123" }
  ```
* This request goes to `/login` or `/authenticate` API in your backend.

---

## 2. **Backend Verifies Credentials**

* Spring Security (via `AuthenticationManager`) checks:

  * Does `alice` exist in the database?
  * Does her password match (after encoding, e.g., BCrypt)?

✅ If **yes** → Authentication successful.
❌ If **no** → Throw error (401 Unauthorized).

---

## 3. **JWT is Created (Issued by Server)**

If authentication is successful, the server generates a JWT.
This JWT has **3 parts**:

1. **Header** (metadata about token):

   ```json
   {
     "alg": "HS256",   // algorithm
     "typ": "JWT"      // type of token
   }
   ```

2. **Payload (Claims)** (user details + extra info):

   ```json
   {
     "sub": "alice",       // subject (username)
     "roles": ["USER"],    // user’s roles/authorities
     "iat": 1693200000,    // issued at
     "exp": 1693203600     // expiry time
   }
   ```

3. **Signature** (security seal):

   ```
   HMACSHA256(
      base64UrlEncode(header) + "." + base64UrlEncode(payload),
      secretKey
   )
   ```

👉 This signature ensures that the token **cannot be tampered with** (if someone edits payload, signature breaks).

---

## 4. **Send JWT to Client**

* The JWT looks like this:

  ```
  eyJhbGciOiJIUzI1NiIsInR5cCI... (long string)
  ```
* Server sends it back in the response (usually JSON):

  ```json
  { "token": "eyJhbGciOi..." }
  ```

The client must **store this token** (not in cookies for APIs, but in localStorage/sessionStorage or memory).

---

## 5. **Client Sends JWT with Each Request**

For every new request (say fetching profile):

```http
GET /profile
Authorization: Bearer eyJhbGciOi...
```

* The JWT is placed in the `Authorization` header (with `Bearer` prefix).

---

## 6. **Server Validates JWT**

Each request passes through Spring Security filters (e.g., `JwtAuthenticationFilter`).
Steps:

1. Extract token from `Authorization` header.
2. Decode the token (Base64 decode header + payload).
3. Verify signature using secret key (or public key in RSA).

   * If tampered → reject.
4. Check expiry (`exp`).

   * If expired → reject.
5. Extract claims (username, roles).

---

## 7. **Set Authentication in SecurityContext**

* If token is valid, Spring Security creates an `Authentication` object with:

  * `Principal` = user (username)
  * `Authorities` = roles (like ROLE\_USER, ROLE\_ADMIN)
* It sets this into **SecurityContext**, so downstream code (controllers/services) knows **who the user is**.

---

## 8. **Authorization Happens**

* When you access `/admin`, Spring Security checks:

  * Does the `Authentication` have `ROLE_ADMIN`?
  * If yes → allow.
  * If no → 403 Forbidden.

---

## 🔄 Summary Flow (Easy to Remember)

1. **Login** → send username/password.
2. **Validate** → check credentials in DB.
3. **Create Token** → header + payload (claims) + signature.
4. **Send Token** → back to client.
5. **Use Token** → client attaches `Authorization: Bearer token`.
6. **Verify Token** → server checks signature + expiry.
7. **Set Authentication** → put user details in Spring Security context.
8. **Authorize** → allow/deny access based on roles.

---


