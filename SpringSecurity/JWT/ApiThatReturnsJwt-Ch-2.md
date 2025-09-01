# 🛠 Step 2: Login API + Generate JWT

---

## 1. Create DTOs (Request & Response)

When a user logs in, they’ll send a username and password.
We’ll return a JWT in the response.

```java
// Request
public class AuthRequest {
    private String username;
    private String password;
    // getters & setters
}

// Response
public class AuthResponse {
    private String token;

    public AuthResponse(String token) {
        this.token = token;
    }
    // getter
}
```

---

## 2. JWT Utility Class

This class handles **token creation & validation**.

```java
package com.spring.security.util;

import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.io.Decoders;
import io.jsonwebtoken.security.Keys;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.stereotype.Component;

import javax.crypto.SecretKey;
import java.security.Key;
import java.util.Date;

@Component
public class JwtUtil {

    // 256-bit Base64 secret
    private static final String secret = "3q2+796tLHg8v8GZx0m+ZkS4lYt+Ud3o3O8vbZTcRTA=";

    private long expiration = 60 * 60 * 1000; //1 hr

    public String generateNewToken(UserDetails userDetails){

        return Jwts.builder()
                .subject(userDetails.getUsername())
                .issuedAt(new Date())
                .expiration(new Date(System.currentTimeMillis() + expiration))
                .signWith(key())
                .compact();
    }

    public String extractUsername(String token){

        return Jwts.parser()
                .verifyWith((SecretKey) key())
                .build()
                .parseSignedClaims(token)
                .getPayload()
                .getSubject();
    }

    public Key key(){
        return Keys.hmacShaKeyFor(Decoders.BASE64.decode(secret));
    }

    public boolean validateToken(String token, UserDetails userDetails){
        String username = extractUsername(token);

        if(token!=null && userDetails.getUsername().equals(username) && Jwts.parser()
                    .verifyWith((SecretKey) key())
                    .build()
                    .parseSignedClaims(token)
                    .getPayload()
                    .getExpiration().after(new Date()))
            return true;

        return false;
    }
}
```

---

## 3. Authentication Controller

This controller exposes `/login`.

* Authenticate user using `AuthenticationManager`.
* If success → generate JWT → return to client.

```java
package com.spring.security.controller;

import com.spring.security.model.AuthRequest;
import com.spring.security.model.AuthResponse;
import com.spring.security.service.CustomUserDetailsManager;
import com.spring.security.util.JwtUtil;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.Authentication;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

@RestController
public class AuthController {

    @Autowired
    AuthenticationManager authenticationManager;

    @Autowired
    JwtUtil jwtUtil;

    @Autowired
    CustomUserDetailsManager customUserDetailsManager;

    @PostMapping("/login")
    public AuthResponse login(@RequestBody AuthRequest authRequest){
        Authentication authentication = authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(
                authRequest.getUsername(), authRequest.getPassword()));

        UserDetails userDetails = (UserDetails) authentication.getPrincipal();

        String jwtToken = jwtUtil.generateNewToken(userDetails);

        return new AuthResponse(jwtToken);
    }
}

```

---

## 4. Update Security Config for Login Endpoint

We must allow `/auth/login` without authentication (public), everything else still protected.

```java

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity http) throws Exception {
        return http
                .csrf(csrf -> csrf.disable())
                .authorizeHttpRequests(auth -> auth
                        .requestMatchers("/login").permitAll()
                        .anyRequest().authenticated()
                )
                .httpBasic(httpBasic -> httpBasic.disable()) // disable Basic Auth
                .build();
    }

```

---

## 5. Test Login API 🎯

Send request:

```http
POST /login
Content-Type: application/json

{
  "username": "Mona",
  "password": "Mona"
}
```

✅ Response:

```json
{
  "token": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJtYWxvYmlrYSIsImlhdCI6MTY5MzU3MjAwMCwiZXhwIjoxNjkzNTc1NjAwfQ.abc123"
}
```

<img width="884" height="689" alt="Screenshot 2025-09-01 at 8 49 33 PM" src="https://github.com/user-attachments/assets/ae439c75-d8ec-4a81-b3b2-08000e4fbeaf" />

---

👉 Now we have **login API returning JWT**.
But right now, this token is useless — we don’t yet use it to protect other APIs.

📌 Next Step → **Step 3: Create a JWT Filter to validate token on every request**.

