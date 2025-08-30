## 1. What is JWT?

**JWT (JSON Web Token)** is a **compact, self-contained, stateless way of transmitting user identity and claims** between client and server.

It’s basically a **string** like this:

```
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.
eyJzdWIiOiJ1c2VyMSIsInJvbGUiOiJVU0VSIiwiaWF0IjoxNjkzMzQ5MjAwLCJleHAiOjE2OTMzNTI4MDB9.
aS3YVvFFWzVmpmbnLPwZZ8eH5Xh0v5whfyD58QKxHJQ
```

Looks weird, but it’s just **3 parts separated by `.`**:

1. **Header** (algorithm + token type) → Base64 encoded JSON
   Example:

   ```json
   {
     "alg": "HS256",
     "typ": "JWT"
   }
   ```

2. **Payload (Claims)** → Base64 encoded JSON
   Example:

   ```json
   {
     "sub": "user1",
     "role": "USER",
     "iat": 1693349200,
     "exp": 1693352800
   }
   ```

3. **Signature** → Used to verify the token hasn’t been tampered with.

   ```
   HMACSHA256(
     base64UrlEncode(header) + "." + base64UrlEncode(payload),
     secretKey
   )
   ```

---

## 2. Why JWT?

* Traditional **session-based authentication** stores login info on the server (in session).
  → Scaling is harder because each server needs session storage (sticky sessions, Redis, etc.).

* **JWT is stateless** → All required info is inside the token itself, so server doesn’t need to store sessions.
  → Any server can validate the token with the secret/public key.

---

## 3. How does JWT work in Authentication?

### Step-by-step Flow

1. **User logs in** (username + password)
   → Credentials verified with DB.

2. **Server generates a JWT** and sends it to client.
   Example payload:

   ```json
   {
     "sub": "user1",
     "role": "USER",
     "iat": 1693349200,
     "exp": 1693352800
   }
   ```

   Signed with secret (HS256) or private key (RS256).

3. **Client stores JWT** (usually in localStorage or a cookie).

4. **Client sends JWT in every request** in the HTTP header:

   ```
   Authorization: Bearer <jwt_token_here>
   ```

5. **Server verifies JWT** (using secret/public key).

   * If valid → extract claims (user, roles, expiry) → allow access.
   * If invalid/expired → return `401 Unauthorized`.

---

## 4. JWT Characteristics

* **Stateless**: No session on server. Token is self-contained.
* **Portable**: Works across domains/services (good for microservices).
* **Compact**: Just a string (around 200-300 bytes usually).
* **Tamper-proof**: Signature prevents modification.
* **Not encrypted by default**: Anyone can read payload (Base64 only). Sensitive data must not go in payload.

---

## 5. JWT in Spring Security

When integrating JWT with Spring Security:

1. **Login endpoint** → validate credentials → generate JWT.
2. **Custom filter** → intercept requests, extract JWT from `Authorization` header, validate.
3. **SecurityContext** → If JWT valid, set `Authentication` object.
4. **Controllers** → secured endpoints check roles/authorities inside JWT claims.

---

## 6. Common Claims in JWT

* `sub` → subject (username/userId)
* `iss` → issuer (who issued the token)
* `exp` → expiry time (Unix timestamp)
* `iat` → issued at
* `nbf` → not before (token valid only after this time)
* `roles` or `authorities` → user’s roles

---

## 7. Example JWT Lifecycle (Spring Security)

```text
POST /login (username, password)
   |
   V
Server validates user -> Generates JWT -> Returns token
   |
   V
Client stores token -> Uses in Authorization header
   |
   V
GET /api/users (Authorization: Bearer token)
   |
   V
JWT Filter -> Validate token -> Set SecurityContext
   |
   V
Controller executes with user identity
```

---

## 8. JWT Pros & Cons

✅ Pros:

* No session storage needed (scalable, microservice friendly)
* Works across domains/services
* Compact & portable

❌ Cons:

* Harder to revoke tokens (logout issue)
* Expired tokens still valid until expiry
* Payload is readable (must avoid sensitive info)

---


Do you want me to start with **a simple implementation flow + code snippets**?
