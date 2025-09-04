# Auth Service

### 1. **Application Setup**

* Port: `9000`
* Service name: `auth-service`
* Registers with Eureka
* Configures JWT secret & expiration in `application.yml`/`application.properties`

```yaml
server:
  port: 9000

spring:
  application:
    name: auth-service

jwt:
  secret: fuHlGVqd2MRQsGUMoupHbF1VQYMeba0LsC6QaFs5Rbs=   # your HS256 secret key
  expiration: 3600000  # 1 hour in ms

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

### 2. **Security Configuration**

* Disables CSRF
* Allows `/auth/register` and `/auth/login` without authentication
* Requires authentication for everything else
* Defines:

  * `PasswordEncoder` (BCrypt)
  * `UserDetailsManager` (InMemoryUserDetailsManager)
  * `DaoAuthenticationProvider`
  * `AuthenticationManager`

```java

@Configuration
@EnableWebSecurity
public class SecurityConfig {

    @Bean
    public SecurityFilterChain securityFilterChain(HttpSecurity httpSecurity) throws Exception {

        httpSecurity.csrf(customizer -> customizer.disable());
        httpSecurity.authorizeHttpRequests(customizer -> {
            customizer.requestMatchers("/auth/register", "/auth/login").permitAll()
                    .anyRequest().authenticated();
        });

        return httpSecurity.build();
    }

    @Bean
    public PasswordEncoder passwordEncoder(){
        return new BCryptPasswordEncoder();
    }

    @Bean
    public UserDetailsManager userDetailsManager(){
        return new InMemoryUserDetailsManager();
    }

    @Bean
    public AuthenticationProvider authenticationProvider(UserDetailsManager userDetailsManager, PasswordEncoder passwordEncoder){
        DaoAuthenticationProvider authenticationProvider = new DaoAuthenticationProvider();
        authenticationProvider.setPasswordEncoder(passwordEncoder);
        authenticationProvider.setUserDetailsService(userDetailsManager);

        return authenticationProvider;
    }

    @Bean
    public AuthenticationManager authenticationManager(AuthenticationProvider authenticationProvider){
        return new ProviderManager(authenticationProvider);
    }
}

```

### 3. **JWT Utility (JwtUtil)**

* Generates JWT with:

  * `subject` → username
  * `claim` → role
  * `issuedAt` + `expiration`
* Uses Base64-decoded secret key with HS256 signing

```java

@Component
public class JwtUtil {

    @Value("${jwt.secret}")
    private String secretKey;

    @Value("${jwt.expiration}")
    private long expiration;

    public String generateToken(UserDetails userDetails, String role){
        return Jwts.builder()
                .signWith(getSecretKey(), SignatureAlgorithm.HS256)
                .claim("role", role)
                .subject(userDetails.getUsername())
                .issuedAt(new Date())
                .expiration(new Date(System.currentTimeMillis()+expiration))
                .compact();
    }

    public Key getSecretKey(){
        return Keys.hmacShaKeyFor(Decoders.BASE64.decode(secretKey));
    }
}
```

### 4. **Controller**

#### `/auth/register`

* Accepts username & password
* Encodes password
* Stores user in InMemory manager
* Assigns roles:

  * `"admin"` → `ROLE_ADMIN`
  * Others → `ROLE_USER`

#### `/auth/login`

* Calls `authenticationManager.authenticate(...)`
* Validates username + password using `DaoAuthenticationProvider`
* On success:

  * Gets authenticated `UserDetails`
  * Extracts role
  * Generates JWT and returns it

```java

@RestController
@RequestMapping("/auth")
public class AuthController {

    private JwtUtil jwtUtil;

    private PasswordEncoder passwordEncoder;

    private UserDetailsManager userDetailsManager;

    private AuthenticationManager authenticationManager;

    public AuthController(JwtUtil jwtUtil, PasswordEncoder passwordEncoder, UserDetailsManager userDetailsManager, AuthenticationManager authenticationManager) {
        this.jwtUtil = jwtUtil;
        this.passwordEncoder = passwordEncoder;
        this.userDetailsManager = userDetailsManager;
        this.authenticationManager = authenticationManager;
    }

    @PostMapping("/register")
    public ResponseEntity<AuthResponse> register(@RequestBody AuthRequest authRequest){
        UserDetails userDetails;

        if(authRequest.getUsername().equals("admin")) {
            userDetails = User.builder()
                    .username(authRequest.getUsername())
                    .password(passwordEncoder.encode(authRequest.getPassword()))
                    .roles("admin")
                    .build();
        }
        else{
            userDetails = User.builder()
                    .username(authRequest.getUsername())
                    .password(passwordEncoder.encode(authRequest.getPassword()))
                    .roles("user")
                    .build();
        }

        userDetailsManager.createUser(userDetails);

        return ResponseEntity.ok(new AuthResponse(authRequest.getUsername()));
    }

    @PostMapping("/login")
    public ResponseEntity<String> login(@RequestBody AuthRequest authRequest){
        Authentication authentication = authenticationManager.authenticate(
                new UsernamePasswordAuthenticationToken(authRequest.getUsername(), authRequest.getPassword()));

        UserDetails userDetails = (UserDetails) authentication.getPrincipal();

        String jwt = jwtUtil.generateToken(userDetails, userDetails.getAuthorities().stream()
                .findFirst()
                .map(a -> a.getAuthority())
                .orElse("ROLE_user"));

        return ResponseEntity.ok(jwt);
    }
}
```

---

# 🔹 Side Notes (Important Understanding)

## What AuthenticationManager does?

- AuthenticationManager is Spring Security’s central strategy for verifying credentials.
- When you call authenticationManager.authenticate(...), it delegates to an AuthenticationProvider (like DaoAuthenticationProvider) which:
  - Fetches the user (via UserDetailsService or in-memory/db).
  - Compares the raw password with the stored one using the configured PasswordEncoder.
  - If valid → returns an Authentication object containing UserDetails + authorities (roles).
  - If invalid → throws BadCredentialsException.

It’s the official Spring way of authenticating credentials. ✅

## When is it triggered automatically?

- If you configure HTTP Basic Auth (httpSecurity.httpBasic()), Spring calls the AuthenticationManager automatically on every request.
    ```java
  httpSecurity.httpBasic();
  ```

  → Spring calls `AuthenticationManager` on every request.
- If you configure form login (httpSecurity.formLogin()), it’s triggered when you submit credentials to /login.
  ```java
  httpSecurity.formLogin();
  ```

  → Triggered automatically on POST to `/login`.
- If you’re rolling your own login endpoint (Custom Login Endpoint) → you have to manually call authenticationManager.authenticate(...) to trigger validation.
  → You must **manually** call:

  ```java
  authenticationManager.authenticate(
      new UsernamePasswordAuthenticationToken(username, password)
  );
  ```
---

## 🔹 DaoAuthenticationProvider (DB / custom user source)

* Default provider in Spring Security.
* Uses `UserDetailsService` + `PasswordEncoder` to validate credentials.
* Example:

  ```java
  @Bean
  public AuthenticationProvider authenticationProvider(UserDetailsService userDetailsService, PasswordEncoder encoder) {
      DaoAuthenticationProvider provider = new DaoAuthenticationProvider();
      provider.setUserDetailsService(userDetailsService);
      provider.setPasswordEncoder(encoder);
      return provider;
  }
  ```

### 🔹 In-memory users

* There is **no separate provider** for in-memory users.
* Instead, we use:

  ```java
  @Bean
  public UserDetailsManager userDetailsManager() {
      return new InMemoryUserDetailsManager();
  }
  ```
* Since `InMemoryUserDetailsManager` implements `UserDetailsService`,
  `DaoAuthenticationProvider` works with it too.

👉 The chain looks like this:

```
AuthenticationManager
      ↓
DaoAuthenticationProvider
      ↓
UserDetailsService (DB, InMemory, LDAP, etc.)
```

So for **in-memory auth**, Spring still uses `DaoAuthenticationProvider`, but the backing `UserDetailsService` is `InMemoryUserDetailsManager`.

---

## Let's try to run

<img width="855" height="615" alt="Screenshot 2025-09-04 at 10 02 02 PM" src="https://github.com/user-attachments/assets/45cb0174-bffd-4388-b505-7c8c52d780ba" />
<img width="899" height="575" alt="Screenshot 2025-09-04 at 10 02 45 PM" src="https://github.com/user-attachments/assets/aa1d14ef-d540-4723-a13d-3dc778d33fd6" />
