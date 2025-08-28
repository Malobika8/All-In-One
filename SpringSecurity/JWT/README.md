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

