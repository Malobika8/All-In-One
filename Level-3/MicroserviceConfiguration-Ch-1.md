# Microservice configuration what and why?

- Separation between code and config

<img width="728" alt="Screenshot 2025-07-09 at 11 14 47 PM" src="https://github.com/user-attachments/assets/f2176c0a-4bfa-4e49-b5c1-056c8b84cd20" />
<img width="588" alt="Screenshot 2025-07-09 at 11 22 07 PM" src="https://github.com/user-attachments/assets/e543b3ad-0713-4a85-a0e9-0197f3573bb3" />

## ✅ What is Microservice Configuration?

**Microservice configuration** refers to the **external properties and settings** that control how each microservice behaves.

Examples:

* Server port (`server.port`)
* Database URL and credentials
* API base URLs
* Feature toggles
* Logging levels
* Retry/circuit breaker settings
* Environment-specific values (dev/test/prod)

Instead of hardcoding these values in your code, you **externalize** them using:

* `.properties` or `.yml` files
* Environment variables
* Centralized config servers (like Spring Cloud Config)
* Secret managers (AWS Secrets Manager, Vault, etc.)

---

## 🔍 Why is Configuration Important in Microservices?

Microservices are **distributed, autonomous, and environment-aware**.

### Without external config:

* You’d have to rebuild and redeploy code to change a single DB password or URL.
* All your services would become tightly coupled to one environment (e.g., dev only).

---

## 💡 Why External Configuration is Essential

| Reason                                 | Explanation                                                                           |
| -------------------------------------- | ------------------------------------------------------------------------------------- |
| 🔁 **Environment-specific setup**      | You can deploy the same codebase to dev, QA, and prod with different configs          |
| 🔒 **Secure secrets handling**         | Credentials, tokens, API keys can be managed securely                                 |
| ⚙️ **Dynamic tuning**                  | You can change log levels, feature flags, or circuit breaker settings without restart |
| 🧪 **Blue/Green & Canary Deployments** | Services can behave differently based on config flags                                 |
| 🚀 **Cloud-native readiness**          | Works well with Docker/Kubernetes where configs are injected at runtime               |

---

## 🧱 Common Configuration Techniques

### 1. **Per-Service `.properties` or `.yml` Files**

```yaml
# application.yml for movie-catalog-service
server:
  port: 8080

movie:
  service:
    url: http://movie-info-service

rating:
  service:
    url: http://rating-data-service
```

---

### 2. **Spring Cloud Config Server (Centralized)**

All services fetch config from a **central config Git repo** or file system via Spring Cloud Config Server.

```text
Catalog Service → Config Server → Git Repo (application.yml)
```

✅ Good for managing:

* Centralized config updates
* Versioned config (via Git)
* Environment overrides

---

## 🛠️ Spring Boot Config Hierarchy (Important!)

When resolving config, Spring Boot follows this order (highest to lowest priority):

1. Command-line args
2. `application.yml` / `application.properties`
3. Profile-specific ymls (`application-dev.yml`)
4. Environment variables
5. Default values in code

✅ You can override values easily without touching the code!

---

## ✅ Real-World Example (Your Architecture)

### You Have:

* Movie Catalog Service
* Movie Info Service (calls slow external MovieDB)
* Rating Data Service

### You Externalize Config Like:

```yaml
# For Movie Info Service
moviedb:
  base-url: https://api.themoviedb.org
  timeout: 3000
```

So you can:

* Change the MovieDB base URL without touching the code
* Adjust timeout to make it more resilient
* Inject fallback values per environment

---

## 🔚 Summary

\| What is it?            | Externalized settings that control your microservice behavior |
\| Why it matters?        | Environment flexibility, secure secrets, easy tuning, and cloud-native readiness |
\| How to manage it?      | `application.yml`, Spring Cloud Config, Kubernetes ConfigMaps, env vars |
