# Architecture pieces

### 🟢 Core microservice setup we want

* **Config Server** → Centralized config for all services
* **Discovery Server** (Eureka) → Services register/discover each other
* **API Gateway** (Spring Cloud Gateway) → Entry point, routes to microservices, can also validate JWTs
* **2–3 Simple Business Services** (e.g. `product-service`, `order-service`) → Expose REST APIs, secure with JWT, role-based access
* **Resilience4j** → Circuit breaker, retry, rate limiting for inter-service calls

### 🟢 Where does **Auth** fit in?

* **Authentication service**: Validates user credentials (username/password, OAuth2 login, etc.) and issues JWT (identity).
* **Authorization**: Deciding *what you can do* → usually checked inside **resource services** (`@PreAuthorize`, path-based access, etc.).

> That’s why we often see people say “authentication service” and “authorization service” — but in practice, we don’t *need* a separate service just for authorization.
>
> * If we use **Keycloak / Okta** → they’re both authN + authZ servers.
> * If we build your own → our **Auth service** issues tokens with `roles` claim. Then each microservice enforces role-based access (authZ) itself.

---

## Step 1 — Base skeleton of microservice system

We’ll keep it very simple for learning.

### Services:

1. **config-server**
2. **discovery-server** (Eureka)
3. **api-gateway** (Spring Cloud Gateway)
4. **product-service**
5. **order-service**

Later, add:
6\. **auth-service** (login + JWT issuing)

### Flow:

```
Client → API Gateway → (token validated) → product-service / order-service
```

## Step 2 — Build order

To avoid confusion, let’s **build incrementally**:

1. Create **config-server** → externalize configs.
2. Create **discovery-server** → make services register.
3. Create **product-service** and **order-service** → expose basic REST endpoints.
4. Create **api-gateway** → route to services.
5. Add **Resilience4j** (circuit breaker between product ↔ order).
6. Add **auth-service** → login, JWT.
7. Secure gateway + services with JWT → add RBAC.

## Step 3 — Quick word on **Authorization service**

We don’t need a separate one **unless**:

* We want **centralized policy management** (ABAC, fine-grained rules, dynamic policies).
* We want to decouple role checks from microservices. Example: OPA (Open Policy Agent) or Keycloak with policies.

But for **our learning goal**, let's keep it simple:

* **Auth service** = Authentication + Token issuing (with roles inside).
* **Authorization** = enforced inside each microservice with Spring Security.

---
