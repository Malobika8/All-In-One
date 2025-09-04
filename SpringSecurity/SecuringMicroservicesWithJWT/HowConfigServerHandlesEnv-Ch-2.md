## 🔹 How Config Server handles environments

Config Server follows a naming convention:

```
<application-name>-<profile>.yml
```

* `<application-name>` = the microservice name (`product-service`, `order-service`, etc.)
* `<profile>` = the Spring profile (`dev`, `test`, `prod`)

When a service starts with `spring.profiles.active=dev`, Config Server will serve `product-service-dev.yml`.

---

## 🔹 Step 1 — Add environment-specific config files

In your Git repo (`spring-microservices-config`), create these files:

**`product-service.yml`** (common config for all environments)

```yaml
spring:
  application:
    name: product-service

app:
  message: "This is Product Service (default config)"
```

**`product-service-dev.yml`**

```yaml
server:
  port: 8081

app:
  message: "Product Service running in DEV environment"
```

**`product-service-prod.yml`**

```yaml
server:
  port: 8082

app:
  message: "Product Service running in PROD environment"
```

Commit & push:

```bash
git add .
git commit -m "Add dev and prod configs for product-service"
git push origin main
```

---

## 🔹 Step 2 — Access environment configs via Config Server

* Default profile (no profile set):

  ```
  http://localhost:8888/product-service/default
  ```
* Dev profile:

  ```
  http://localhost:8888/product-service/dev
  ```
* Prod profile:

  ```
  http://localhost:8888/product-service/prod
  ```

You’ll see JSON with the correct values.

---

## 🔹 Step 3 — Client microservice setup

In `product-service/src/main/resources/application.yml` (client app itself), configure:

```yaml
spring:
  application:
    name: product-service
  profiles:
    active: dev   # 👈 tell it which profile to use
  cloud:
    config:
      uri: http://localhost:8888
```

When you start `product-service`, it will fetch its config from Config Server under profile `dev`.

---

✅ That’s how you separate configs for multiple environments with Config Server.

---

