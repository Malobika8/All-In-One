We’ll create **two services**:

* `product-service`
* `order-service`
  and make both **register with Eureka**.

---

# 🔹 Step 3 — Create Product Service & Register with Eureka

## 1️⃣ Create Spring Boot project: **product-service**

Dependencies:

* Spring Boot Starter Web
* Spring Boot Starter Actuator (optional, good for monitoring)
* Spring Cloud Starter Netflix Eureka Client

👉 If you’re using Spring Initializr, pick **Eureka Discovery Client**.

---

## 2️⃣ `pom.xml` (product-service)

```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <dependency>
        <groupId>org.springframework.cloud</groupId>
        <artifactId>spring-cloud-starter-netflix-eureka-client</artifactId>
    </dependency>
</dependencies>

<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-dependencies</artifactId>
            <version>2023.0.3</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

---

## 3️⃣ Application class

```java
@SpringBootApplication
@EnableDiscoveryClient   // optional, Boot auto-configures this
public class ProductServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(ProductServiceApplication.class, args);
    }
}
```

---

## 4️⃣ application.yml (product-service)

```yaml
server:
  port: 8081

spring:
  application:
    name: product-service

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

---

## 5️⃣ Sample REST Controller

```java
@RestController
@RequestMapping("/products")
public class ProductController {

    @GetMapping
    public List<String> getProducts() {
        return List.of("Laptop", "Phone", "Headphones");
    }
}
```

---

# 🔹 Step 4 — Create Order Service & Register with Eureka

## 1️⃣ Create Spring Boot project: **order-service**

Dependencies:

* Spring Boot Starter Web
* Eureka Discovery Client

---

## 2️⃣ application.yml (order-service)

```yaml
server:
  port: 8082

spring:
  application:
    name: order-service

eureka:
  client:
    service-url:
      defaultZone: http://localhost:8761/eureka/
```

---

## 3️⃣ Sample REST Controller

```java
@RestController
@RequestMapping("/orders")
public class OrderController {

    @GetMapping
    public List<String> getOrders() {
        return List.of("Order1", "Order2", "Order3");
    }
}
```

---

# 🔹 Step 5 — Run All Together

1. Start **Config Server** (port `8888`)
2. Start **Discovery Server** (port `8761`)
3. Start **product-service** (port `8081`)
4. Start **order-service** (port `8082`)

👉 Go to [http://localhost:8761](http://localhost:8761) → you should see both services registered 🎉


