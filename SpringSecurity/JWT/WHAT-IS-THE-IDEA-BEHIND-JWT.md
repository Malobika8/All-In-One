### 🔑 Core Principle of JWT Security

JWTs are **not trusted just because they have claims**.
They’re trusted only if they are **digitally signed** with a **secret key (HS256)** or **private key (RS256)**.

* When **Auth Service** generates the JWT, it signs it with a **secret key**.
* **Gateway** (and other services) have the same key (in HS256) or the public key (in RS256).
* If someone “makes up” a token by hand, it will fail signature verification at Gateway because they don’t know the secret/private key.

So as long as we:

1. Use a strong, long, random signing key (not `"mysecret"` 😅).
2. Keep that key **safe and private** (don’t expose in repo, don’t log it).

👉 Nobody can forge a valid JWT.

### ✅ How Gateway Prevents Forged Tokens

When Gateway validates a JWT:

```java
Jwts.parserBuilder()
    .setSigningKey(key)   // 🔑 secret or public key
    .build()
    .parseClaimsJws(token) // throws exception if signature invalid
```

If the token was not issued by Auth Service (wrong signature), the parser throws `io.jsonwebtoken.security.SignatureException`.

So a fake token like:

```json
{
  "sub": "hacker",
  "roles": ["ADMIN"],
  "exp": 9999999999
}
```

would fail validation unless the hacker **knows the signing key**.

# 1. JWT is not “encrypted”, it is “signed”

* **Encryption** = hides data (only someone with the key can see it).
* **Signing** = proves data integrity + authenticity (anyone with the key can verify if data was tampered, but not hide it).

JWTs (with HS256/RS256) are **signed**, not encrypted.
That means:

* The **claims (payload)** are **base64-encoded, not hidden**.
* Anyone can decode the payload and read `"username"`, `"roles"`, `"exp"`.
* What protects JWTs is the **signature** at the end.

## 2. Structure of JWT

A JWT has 3 parts (Base64URL encoded):

```
header.payload.signature
```

Example:

```
eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1c2VyIiwicm9sZXMiOlsiQURNSU4iXX0.J23kUQjSgH...
```

* **Header**: `{ "alg": "HS256", "typ": "JWT" }`
* **Payload**: `{ "sub": "user", "roles": ["ADMIN"], "exp": ... }`
* **Signature**: `HMACSHA256(base64UrlEncode(header) + "." + base64UrlEncode(payload), secretKey)`

## 3. What the “signature” really is

When Auth Service issues a token:

1. It takes `header + payload`.
2. Computes an HMAC with the secret key.
3. Produces a hash (signature).

That signature is attached as the 3rd part of the JWT.

When Gateway receives the token:

1. It takes the same `header + payload`.
2. Recomputes the HMAC with its copy of the secret key.
3. Compares the result with the signature in the token.

   * If they match → token is authentic (not modified, issued by someone with the key).
   * If they don’t match → reject (`SignatureException`).

## 4. Why you can’t just “make” a valid JWT

Suppose you try this:

* You make up a payload: `{ "sub": "hacker", "roles": ["ADMIN"] }`.
* You base64-encode it.
* You attach some random string as signature.

👉 Gateway will recompute the signature with the secret key and compare.
Since you don’t know the secret key, your signature won’t match → Gateway rejects it.

The only way to forge a valid JWT is to **know the secret key**.
That’s why the secret key is so important.

## 5. Why people think it’s “decrypting”

It feels like decryption, but actually:

* The secret key isn’t used to decrypt the payload.
* It’s used to recompute and **verify the signature**.

The payload is always visible (unless you use JWE, an encrypted JWT variant, which is rare).
JWTs are about **authenticity, not confidentiality**.

✅ **Summary**

* JWT payload = readable by anyone.
* JWT signature = proof it was issued by your Auth Service.
* Gateway **does not decrypt** the JWT, it **verifies the signature**.
* If the signature check fails → reject.
* If you keep your secret key safe, attackers cannot forge tokens.

---

## 🔑 Signing Process (when Auth Service issues JWT)

1. Take **header** and **payload**.
   Example:

   ```json
   header:  {"alg": "HS256", "typ": "JWT"}
   payload: {"sub": "alice", "roles": ["USER"], "exp": 1693958400}
   ```
2. Base64URL encode them → `encodedHeader.encodedPayload`.
3. Compute HMAC-SHA256 using the **secret key**.

   ```
   signature = HMACSHA256(encodedHeader + "." + encodedPayload, secretKey)
   ```
4. Final JWT = `encodedHeader.encodedPayload.signature`.

## 🔑 Validation Process (at Gateway)

1. Split incoming token into `header.payload.signature`.
2. Recompute the HMAC-SHA256 using **its own copy** of `secretKey`.

   ```
   expectedSignature = HMACSHA256(encodedHeader + "." + encodedPayload, secretKey)
   ```
3. Compare `expectedSignature` with the signature part of token.

   * If they **match** → token was signed by someone who knows the secret key → ✅ valid.
   * If they **don’t match** → token is fake or tampered → ❌ reject.

### ⚠️ Subtle but important

* It’s not just “comparing secret key”.
* Gateway never sees the original secret from Auth Service inside the token.
* It **uses the secret key** to recompute a hash and check against the provided signature.

That’s why an attacker can’t just generate a JWT:

* They can make a header and payload easily.
* But they can’t produce a valid signature without the secret key.

👉 So JWT security = **the secrecy of that signing key**.
If the key leaks, attackers can issue their own valid tokens.
That’s why in production we often use:

* **Strong random keys (256-bit for HS256)**
* Or **asymmetric signing (RS256)** → private key signs (Auth), public key verifies (Gateway).

---

# 🔒 Extra Hardening Options

If you want to go beyond shared-secret validation:

1. **Asymmetric Signing (RS256)**

   * Auth Service signs JWT with **private key**.
   * Gateway & other services validate with **public key**.
   * Even if Gateway leaks, private key remains safe.
   * Best for production in multi-team setups.

2. **Key Rotation**

   * Use JWK (JSON Web Key Set).
   * Auth Service publishes public keys.
   * Gateway fetches keys dynamically.
   * This allows rotating keys without downtime.

3. **Audience & Issuer Validation**

   * Add claims like `"iss": "auth-service"` and `"aud": "product-service"`.
   * Gateway checks these fields to make sure the token was meant for your system.

---

✅ So the short answer:

* If someone fabricates a JWT without the Auth Service secret/private key → Gateway **rejects it**.
* As long as you use a **strong secret** (HS256) or **RSA/ECDSA keys**, your system is safe.

---
