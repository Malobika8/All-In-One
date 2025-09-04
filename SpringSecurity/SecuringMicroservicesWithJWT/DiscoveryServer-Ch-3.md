# 🔹 Step 2 — Setup Discovery Server (Eureka)

## 1️⃣ Create a new Spring Boot project

* Name: **discovery-server**
* Dependencies:

  * **Spring Boot Starter Web**
  * **Eureka Server** (under *Spring Cloud Discovery*)

---

## 2️⃣ Add dependencies (if creating manually via Maven)

In `pom.xml`:

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
    </dependency>
</dependencies>

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>2023.0.3</version> <!-- 👈 latest stable BOM -->
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

---

## 3️⃣ Enable Eureka Server

In `DiscoveryServerApplication.java`:

```java
@SpringBootApplication
@EnableEurekaServer
public class DiscoveryServerApplication {
    public static void main(String[] args) {
        SpringApplication.run(DiscoveryServerApplication.class, args);
    }
}
```

---

## 4️⃣ Configure application.yml

Create `src/main/resources/application.yml`:

```yaml
server:
  port: 8761

spring:
  application:
    name: discovery-server

eureka:
  client:
    register-with-eureka: false   # server should not register itself
    fetch-registry: false
```

---

## 5️⃣ Run the server

Start the app → open [http://localhost:8761](http://localhost:8761).
You should see the **Eureka Dashboard** 🖥️ (with “No instances available” for now).

---

# Note:

`@EnableDiscoveryClient` is the **generic annotation** that works with *any* discovery service (Eureka, Consul, Zookeeper).

But here’s the subtle difference:

* **`@EnableEurekaServer`** → used only on the **server side** (the Discovery Server itself, e.g., `discovery-server`).
* **`@EnableDiscoveryClient`** → used on the **client side** (like `product-service`, `order-service`, etc.) so they can register with *whatever* discovery mechanism you configure.

There is also a thing people sometimes mention: **`@EnableDiscoveryServer`** — but that doesn’t actually exist in Spring Cloud. For servers, it’s always `@EnableEurekaServer`.

# Quick look

<img width="1031" height="749" alt="Screenshot 2025-09-04 at 12 29 20 PM" src="https://github.com/user-attachments/assets/23c9572d-d6e7-4ce7-a947-a129cdd14cdd" />
<img width="989" height="358" alt="Screenshot 2025-09-04 at 12 29 26 PM" src="https://github.com/user-attachments/assets/10e64da8-00a5-4e3e-a7c0-d4f4345327c9" />
<img width="907" height="309" alt="Screenshot 2025-09-04 at 12 29 31 PM" src="https://github.com/user-attachments/assets/942ed357-b6e6-4bb5-b374-b560764a7288" />

