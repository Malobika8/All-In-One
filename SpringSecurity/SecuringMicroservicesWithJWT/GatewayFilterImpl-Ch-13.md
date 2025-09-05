## 🔑 Plan

1. **JWT Validation** (already done)

   * Extract `username` and `roles`.
   * Ensure signature & expiry are valid.

2. **Role Mapping per Route**

   * `/product/**` → allow only `ADMIN`.
   * `/order/**` → allow only `USER`.
   * (You can make this configurable later via `application.yml`).

3. **Enforce Role Checks in the Filter**

   * If user’s roles don’t match → block with `403 Forbidden`.
   * Otherwise → forward request with `X-Auth-Username`, `X-Auth-Roles`.

---

## 📝 Updated `AuthenticationFilter.java`

```java
package com.security.gateway.service.gateway_service.filter;

import com.security.gateway.service.gateway_service.util.JwtUtil;
import jakarta.ws.rs.core.HttpHeaders;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.cloud.gateway.filter.GatewayFilter;
import org.springframework.cloud.gateway.filter.factory.AbstractGatewayFilterFactory;
import org.springframework.http.HttpStatus;
import org.springframework.stereotype.Component;
import org.springframework.web.server.ServerWebExchange;
import reactor.core.publisher.Mono;

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
            String path = exchange.getRequest().getURI().getPath();

            //Allow /auth/** without token
            if(path.contains("/auth")){
                return chain.filter(exchange);
            }

            // Get token
            String authHeader = exchange.getRequest().getHeaders().getFirst(HttpHeaders.AUTHORIZATION);
            if (authHeader == null || !authHeader.startsWith("Bearer ")) {
                return onError(exchange, "Missing or invalid Authorization header", HttpStatus.UNAUTHORIZED);
            }

            String token = authHeader.substring(7);
            if (!jwtUtil.validateToken(token)) {
                return onError(exchange, "Invalid or expired JWT token", HttpStatus.UNAUTHORIZED);
            }

            // Extract username and roles
            String username = jwtUtil.getClaims(token).getSubject();
            String role = (String) jwtUtil.getClaims(token).get("role");

            // Role-based checks
            if (path.startsWith("/products") && !role.contains("ROLE_admin")) {
                return onError(exchange, "Access denied: Admin role required", HttpStatus.FORBIDDEN);
            }
            if (path.startsWith("/orders") && !role.contains("ROLE_user")) {
                return onError(exchange, "Access denied: User role required", HttpStatus.FORBIDDEN);
            }

            // Forward username & roles to downstream services
            exchange = exchange.mutate().request(r -> r.headers(h -> {
                h.add("X-Auth-Username", username);
                h.add("X-Auth-Roles", String.join(",", role));
            })).build();

            return chain.filter(exchange);
        };
    }

    private Mono<Void> onError(ServerWebExchange exchange, String err, HttpStatus httpStatus) {
        exchange.getResponse().setStatusCode(httpStatus);
        return exchange.getResponse().setComplete();
    }

    public static class Config {}
}
```

---

## 🔧 `application.yml` (Gateway routes)

```yaml
server:
  port: 8080

spring:
  application:
    name: GATEWAY-SERVICE
  cloud:
    gateway:
      server:
        webflux:
          routes:
            - id: AUTH-SERVICE
              uri: lb://AUTH-SERVICE
              predicates:
                - Path=/auth/**
            - id: ORDER-SERVICE
              uri: lb://ORDER-SERVICE
              predicates:
                - Path=/orders/**
              filters:
                - AuthenticationFilter
            - id: PRODUCT-SERVICE
              uri: lb://PRODUCT-SERVICE
              predicates:
                - Path=/products/**
              filters:
                - AuthenticationFilter

jwt:
  secret: fuHlGVqd2MRQsGUMoupHbF1VQYMeba0LsC6QaFs5Rbs=   # your HS256 secret key

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka

logging:
  level:
    org.springframework.cloud.gateway: DEBUG

```

---

## ✅ What Happens Now

1. Request → `POST /auth/register`, `POST /auth/login`  → ✅ allowed (no JWT needed).
2. Request → `POST /products` with `Authorization: Bearer <token>`

   * If token has `ROLE_ADMIN` → allowed.
   * Otherwise → `403 Forbidden`.
3. Request → `GET /orders` with `Authorization: Bearer <token>`

   * If token has `ROLE_USER` → allowed.
   * Otherwise → `403 Forbidden`.

---

⚡ With this, the **Gateway itself enforces role-based access** before hitting downstream services.
Services can still double-check if needed, but they don’t have to.

---

