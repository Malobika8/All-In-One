## ✅ Goal

We’ll create:

* A shared config for `user-service`
* A **dev-specific** config for `user-service` when the `dev` profile is active

---

## 🧱 Step-by-Step: Add `user-service-dev.yml`

### 📁 Inside your config repo (`~/config-repo`), create this:

```
~/config-repo/
├── user-service.yml              <-- common config for all profiles
└── user-service-dev.yml          <-- overrides when 'dev' profile is active
```

---

### 🧾 `user-service.yml`

```yaml
custom:
  message: Hello from Common Config
```

### 🧾 `user-service-dev.yml`

```yaml
custom:
  message: Hello from DEV Profile
  welcome: Welcome to Dev Environment!
```

---

## 🔧 Modify the Client App (`user-service`)

### ✅ Add active profile

Update `application.yml` of `user-service`:

```yaml
spring:
  application:
    name: user-service

  config:
    import: optional:configserver:http://localhost:8888

  profiles:
    active: dev  # 🔥 This activates the profile

server:
  port: 8081
```

---

### 🧾 Update the Controller to read both properties

```java
@RestController
public class MessageController {

    @Value("${custom.message}")
    private String message;

    @Value("${custom.welcome:Default welcome}")
    private String welcome;

    @GetMapping("/msg")
    public String getMessage() {
        return message + " | " + welcome;
    }
}
```

> `:Default welcome` is a fallback in case `custom.welcome` is not found.

---

## ▶️ Run Everything

### 1. Run `config-server`

It should serve `user-service.yml` and `user-service-dev.yml`

Test this in browser:

```
http://localhost:8888/user-service/dev
```

You should see:

```json
"custom.message": "Hello from DEV Profile",
"custom.welcome": "Welcome to Dev Environment!"
```

### 2. Run `user-service`

Then visit:

```
http://localhost:8081/msg
```

You should see:

```
Hello from DEV Profile | Welcome to Dev Environment!
```

✅ That confirms profile-specific config is working perfectly!

---

## 🧠 How This Works Internally

When profile = `dev`, the config server merges:

```
user-service.yml         ⬅️ common
+
user-service-dev.yml     ⬅️ profile-specific (active)
```

The `user-service-dev.yml` **overrides or adds** any keys.

---

## 🧪 Test Switching to `prod`

Just change this in `user-service` → `application.yml`:

```yaml
spring.profiles.active: prod
```

Create a `user-service-prod.yml` in your config repo:

```yaml
custom:
  message: Hello from PROD Profile
  welcome: Welcome to Production!
```

Then restart `user-service` and hit `/msg`. You’ll see the new message.

---

## ✅ Summary

| File Name               | Purpose                           |
| ----------------------- | --------------------------------- |
| `user-service.yml`      | Default config for all profiles   |
| `user-service-dev.yml`  | Overrides for `dev` profile only  |
| `user-service-prod.yml` | Overrides for `prod` profile only |

---
