# Spring Security – Securing Web Apps

**Agenda:** Building a plain **Spring MVC (no Spring Boot)** app first, then wiring **Spring Security**. 

---

## 0) Goal & Mental Model

* **Goal:** run a basic MVC app; then add Spring Security so every request goes through a **security filter chain** before reaching controllers.
* **Mental picture:**

```
Browser → [Servlet Filters] → DispatcherServlet → Controllers → Views
            ↑ Spring Security filter chain lives here
```

---

## 1) Project Setup (non‑Boot)

**Stack:** Spring Framework 6, Spring Security 6, Servlet 6 (Jakarta), JSP for views, Maven, JDK 17+.

**Key points (Jakarta world):**

* Package names are `jakarta.*` (not `javax.*`).
* Use Tomcat 10.1+ (or any Servlet 6 container).

**pom.xml (essentials)** – versions are examples; keep Spring 6.x / Security 6.x and JDK 17.

```xml
<properties>
  <maven.compiler.release>17</maven.compiler.release>
  <spring.version>6.1.0</spring.version>
  <spring.security.version>6.3.0</spring.security.version>
</properties>

<dependencies>
  <!-- Spring MVC -->
  <dependency>
    <groupId>org.springframework</groupId>
    <artifactId>spring-webmvc</artifactId>
    <version>${spring.version}</version>
  </dependency>

  <!-- Spring Security (web + config) -->
  <dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-web</artifactId>
    <version>${spring.security.version}</version>
  </dependency>
  <dependency>
    <groupId>org.springframework.security</groupId>
    <artifactId>spring-security-config</artifactId>
    <version>${spring.security.version}</version>
  </dependency>

  <!-- Servlet/JSP (provided by container) -->
  <dependency>
    <groupId>jakarta.servlet</groupId>
    <artifactId>jakarta.servlet-api</artifactId>
    <version>6.0.0</version>
    <scope>provided</scope>
  </dependency>
  <dependency>
    <groupId>jakarta.servlet.jsp.jstl</groupId>
    <artifactId>jakarta.servlet.jsp.jstl-api</artifactId>
    <version>3.0.0</version>
  </dependency>
  <dependency>
    <groupId>org.glassfish.web</groupId>
    <artifactId>jakarta.servlet.jsp.jstl</artifactId>
    <version>3.0.1</version>
  </dependency>
</dependencies>
```

**Maven plugin (JDK 17):**

```xml
<build>
  <plugins>
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-compiler-plugin</artifactId>
      <version>3.11.0</version>
      <configuration>
        <release>17</release>
      </configuration>
    </plugin>
  </plugins>
</build>
```

> **Gotchas:** Add JSP/JSTL libs to avoid compilation issues; keep `jakarta.servlet-api` scope as **provided**.

---

## 2) DispatcherServlet (programmatic init)

Register Spring MVC without XML using `AbstractAnnotationConfigDispatcherServletInitializer`.

```java
// src/main/java/com/example/web/AppInitializer.java
package com.example.web;

import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

public class AppInitializer extends AbstractAnnotationConfigDispatcherServletInitializer {

  @Override
  protected Class<?>[] getRootConfigClasses() {
    // Root context (services, security, data, etc.)
    return new Class<?>[] { SecurityConfig.class }; // add security here (see §5)
  }

  @Override
  protected Class<?>[] getServletConfigClasses() {
    // Web (MVC) context
    return new Class<?>[] { WebConfig.class };
  }

  @Override
  protected String[] getServletMappings() {
    return new String[] { "/" };
  }
}
```

**MVC config:**

```java
// src/main/java/com/example/web/WebConfig.java
package com.example.web;

import org.springframework.context.annotation.*;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.view.InternalResourceViewResolver;
import org.springframework.context.annotation.Bean;

@Configuration
@EnableWebMvc
@ComponentScan(basePackages = "com.example.web")
public class WebConfig {

  @Bean
  public InternalResourceViewResolver viewResolver() {
    InternalResourceViewResolver vr = new InternalResourceViewResolver();
    vr.setPrefix("/WEB-INF/views/");
    vr.setSuffix(".jsp");
    return vr;
  }
}
```

**Simple controller + views:**

```java
// src/main/java/com/example/web/HomeController.java
package com.example.web;

import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;

@Controller
public class HomeController {
  @GetMapping("/")
  public String home() {
    return "home"; // /WEB-INF/views/home.jsp
  }

  @GetMapping("/hello")
  public String hello() {
    return "hello"; // secured later
  }
}
```

```jsp
<!-- /WEB-INF/views/home.jsp -->
<!DOCTYPE html>
<html>
<body>
  <h1>Home (public)</h1>
  <p><a href="hello">Go to Hello</a></p>
</body>
</html>
```

```jsp
<!-- /WEB-INF/views/hello.jsp -->
<!DOCTYPE html>
<html>
<body>
  <h1>Hello (should require login once security is on)</h1>
</body>
</html>
```

**MVC request flow reminder:**

```
Client → DispatcherServlet → HandlerMapping → Controller → ViewResolver → JSP
```

---

## 3) Where Security Fits (concept)

Before a request reaches `DispatcherServlet`, it passes through **Servlet Filters**. Spring Security installs a **DelegatingFilterProxy** that delegates to a bean named `springSecurityFilterChain`.

```
Request → [DelegatingFilterProxy] → springSecurityFilterChain (many filters) → DispatcherServlet → Controller
```

* Each security filter checks if it applies; if not, it quickly passes the request along.
* No filter chain bean = security won’t run.

---

## 4) Add Spring Security Dependencies

(Already in pom above: `spring-security-web` and `spring-security-config`).

---

## 5) Security Bootstrapping (the two must‑haves)

**A. `AbstractSecurityWebApplicationInitializer` (auto‑register the proxy/filter)**

```java
// src/main/java/com/example/security/SecurityInitializer.java
package com.example.security;

import org.springframework.security.web.context.AbstractSecurityWebApplicationInitializer;

public class SecurityInitializer extends AbstractSecurityWebApplicationInitializer {
  // empty: this registers DelegatingFilterProxy → springSecurityFilterChain
}
```

**B. `@EnableWebSecurity`(internally creates a bean of springSecurityFilterChain) + a `SecurityFilterChain` bean**

```java
// src/main/java/com/example/web/SecurityConfig.java
package com.example.web;

import org.springframework.context.annotation.*;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;

@Configuration
@EnableWebSecurity //this internally creates a bean of springSecurityFilterChain
public class SecurityConfig {

}
```

<img width="845" height="408" alt="Screenshot 2025-08-24 at 9 12 24 PM" src="https://github.com/user-attachments/assets/5eb9467c-4ac4-44b6-8d90-dfd512f7992f" />
<img width="848" height="373" alt="Screenshot 2025-08-24 at 9 12 31 PM" src="https://github.com/user-attachments/assets/9faa7c1a-9c61-4b7d-bcaa-8ae9b986aae0" />
<img width="844" height="411" alt="Screenshot 2025-08-24 at 9 12 39 PM" src="https://github.com/user-attachments/assets/f9fd8594-33d5-484c-b075-f33449ccc4cf" />

> **Result now:** the app starts; navigating to `/hello` shows the **default login page**. Since we haven’t configured users yet, login attempts won’t succeed.

**Common error & fix:**

* Error: `No bean named 'springSecurityFilterChain' available` → We either forgot `@EnableWebSecurity` or my `SecurityConfig` isn’t in the **root context**. Ensure `AppInitializer#getRootConfigClasses()` includes `SecurityConfig`.

**Architecture sketch:**

```
[SecurityInitializer]
      ↓ registers
[DelegatingFilterProxy: "springSecurityFilterChain"]
      ↓ delegates to bean
[SecurityFilterChain] = [Filter1] → [Filter2] → … → [FilterN]
      ↓
DispatcherServlet → Controllers
```

---

## 6) Programmatic vs Spring Boot (just context)

* Here we **manually** registered DispatcherServlet + Security (good for learning and control).
* In Spring Boot, these initializers and many defaults are **auto‑configured** (less boilerplate, but the same building blocks under the hood).

---

## 7) Authentication Flow (sequence diagram)

```
User → Browser → Request /hello
      ↓
Servlet Container
      ↓
DelegatingFilterProxy (registered by SecurityInitializer)
      ↓
springSecurityFilterChain (series of filters)
      ↓ checks authentication → not authenticated
      ↓ redirect to /login (default form)

User enters creds → Login form POST
      ↓
UsernamePasswordAuthenticationFilter
      ↓ AuthenticationManager → AuthenticationProvider → UserDetailsService
      ↓ on success → SecurityContextHolder stores Authentication
      ↓ redirect back to /hello
      ↓ Controller executes
```

---

## 8) What we will do next (later episodes)

* Add **users/authentication** (in‑memory, JDBC, or custom `UserDetailsService`).
* Understand `AuthenticationManager`, providers, and the login flow end‑to‑end.
* Add CSRF form tokens (when I build POST forms).
* Explore method security and JWT/OAuth once basics are solid.

---

## 9) Quick Recap

* MVC app up and running.
* Added Security deps.
* **Registered** Spring Security via `AbstractSecurityWebApplicationInitializer`.
* **Enabled** Web Security and exposed `SecurityFilterChain` bean.
* Saw default login page on secured endpoints.
* Understood how the **auth flow** sequence works.

