# Jwt Validation

<img width="933" height="531" alt="Screenshot 2025-09-05 at 1 24 14 PM" src="https://github.com/user-attachments/assets/25ecd9fc-05f9-4424-b720-696f0b6333b6" />
<img width="938" height="66" alt="Screenshot 2025-09-05 at 1 23 59 PM" src="https://github.com/user-attachments/assets/64a3a32f-6e2c-4bee-8563-27375ba32f9f" />
<img width="1019" height="749" alt="Screenshot 2025-09-05 at 1 23 52 PM" src="https://github.com/user-attachments/assets/deff5410-9229-4d63-867e-68432381c7c7" />

# Gateway Filter

## 1️⃣ Why it looks different

* In a **service** (e.g., Product/Order), we usually have `Spring MVC` + `Servlet API`.

  * There, we intercept requests using `javax.servlet.Filter` or Spring’s `OncePerRequestFilter`.
  * These work in **Servlet blocking I/O** model.
  * Example:

    ```java
    public class JwtAuthFilter extends OncePerRequestFilter {
        @Override
        protected void doFilterInternal(HttpServletRequest request,
                                        HttpServletResponse response,
                                        FilterChain filterChain) {
            // validate JWT
            filterChain.doFilter(request, response);
        }
    }
    ```
* In the **Gateway**, we don’t have the Servlet API at all.

  * Gateway is built on **Spring WebFlux** (reactive, non-blocking).
  * No `HttpServletRequest`, no `FilterChain`.
  * Instead we work with `ServerWebExchange` (request/response container) and **reactive filters**.

---

## 2️⃣ Filters in Spring Cloud Gateway

Gateway has two main types of filters:

### **Global Filters**

* Apply to every request.
* Implement `GlobalFilter` + `Ordered`.
* Example: Logging all requests.

```java
@Component
public class LoggingFilter implements GlobalFilter, Ordered {
    @Override
    public Mono<Void> filter(ServerWebExchange exchange, GatewayFilterChain chain) {
        System.out.println("Incoming request: " + exchange.getRequest().getURI());
        return chain.filter(exchange);
    }

    @Override
    public int getOrder() {
        return -1; // higher priority
    }
}
```

### **Route Filters**

* Apply to specific routes only.
* Usually extend `AbstractGatewayFilterFactory`.
* This is what we used for JWT authentication.

```java
@Component
public class AuthenticationFilter extends AbstractGatewayFilterFactory<AuthenticationFilter.Config> {
    @Autowired
    private JwtUtil jwtUtil;

    public AuthenticationFilter() {
        super(Config.class);
    }

    @Override
    public GatewayFilter apply(Config config) {
        return (exchange, chain) -> {
            // check headers, validate JWT
            return chain.filter(exchange);
        };
    }

    public static class Config {}
}
```

---

## 3️⃣ Key Differences from `OncePerRequestFilter`

| Aspect              | In Service (`OncePerRequestFilter`) | In Gateway (`AbstractGatewayFilterFactory`) |
| ------------------- | ----------------------------------- | ------------------------------------------- |
| **Framework**       | Spring MVC / Servlet API            | Spring WebFlux / Reactive                   |
| **Request object**  | `HttpServletRequest`                | `ServerWebExchange`                         |
| **Filter chain**    | `FilterChain` (blocking)            | `GatewayFilterChain` (reactive `Mono`)      |
| **Execution style** | Synchronous / Blocking              | Asynchronous / Non-blocking                 |
| **Scope**           | Per application/service             | Centralized at Gateway (routes)             |
| **Typical use**     | Security per service                | Cross-cutting concerns (JWT, logging, CORS) |

---

## 4️⃣ How filtering works in Gateway

When a request comes into Gateway:

1. The **route is matched** (by path, predicates).
2. Any configured **filters for that route** run.
3. If filters approve → request forwarded to backend service.
4. If filters reject (like invalid JWT) → Gateway returns error, never calls service.

---

## 5️⃣ Example: JWT Filter Recap

We already made a route filter like this:

```java
@Override
public GatewayFilter apply(Config config) {
    return (exchange, chain) -> {
        String authHeader = exchange.getRequest().getHeaders().getFirst(HttpHeaders.AUTHORIZATION);

        if (authHeader == null || !authHeader.startsWith("Bearer ")) {
            exchange.getResponse().setStatusCode(HttpStatus.UNAUTHORIZED);
            return exchange.getResponse().setComplete();
        }

        String token = authHeader.substring(7);
        if (!jwtUtil.isTokenValid(token)) {
            exchange.getResponse().setStatusCode(HttpStatus.UNAUTHORIZED);
            return exchange.getResponse().setComplete();
        }

        return chain.filter(exchange); // forward if valid
    };
}
```

This looks different from `OncePerRequestFilter` because:

* Instead of `request/response`, we have `exchange`.
* Instead of `doFilter(request, response, chain)`, we return a **reactive `Mono<Void>`**.
* The idea is the same though: intercept, check, then either block or continue.

---

## 6️⃣ When to use which?

* **Gateway Filters** → Centralized, cross-cutting security (JWT validation, request logging, global headers).
* **Service Filters (`OncePerRequestFilter`)** → Local business security (e.g., fine-grained rules per service, method-level `@PreAuthorize`).

---

✅ So, the difference is just because **Gateway is reactive**, while services are usually servlet-based.
The pattern is the same — intercept, check, forward or block.

