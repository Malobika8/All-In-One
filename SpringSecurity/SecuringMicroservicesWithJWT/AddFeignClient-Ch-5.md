# 🔹 Step 6 — Add Feign Client

## 1️⃣ Add dependency (order-service `pom.xml`)

```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-openfeign</artifactId>
</dependency>
```

---

## 2️⃣ Enable Feign in order-service

```java
@SpringBootApplication
@EnableDiscoveryClient
@EnableFeignClients   // 👈 enables Feign
public class OrderServiceApplication {
    public static void main(String[] args) {
        SpringApplication.run(OrderServiceApplication.class, args);
    }
}
```

---

## 3️⃣ Create Feign Client Interface

```java
@FeignClient(name = "product-service")  // 👈 matches spring.application.name of product-service
public interface ProductClient {

    @GetMapping("/products")
    List<String> getProducts();
}
```

---

## 4️⃣ Use Feign Client in Order Controller

```java
@RestController
@RequestMapping("/orders")
public class OrderController {

    private final ProductClient productClient;

    public OrderController(ProductClient productClient) {
        this.productClient = productClient;
    }

    @GetMapping
    public List<String> getOrders() {
        List<String> products = productClient.getProducts();
        return List.of("Order1 with " + products.get(0),
                       "Order2 with " + products.get(1));
    }
}
```

---

## 5️⃣ Run and Test

1. Start `discovery-server`
2. Start `product-service`
3. Start `order-service`

👉 Call:

```
http://localhost:8082/orders
```

Expected response (example):

```json
[
  "Order1 with Laptop",
  "Order2 with Phone"
]
```

---

✅ This proves **service-to-service communication** via **Feign + Eureka**.

---

# Quick look

## product-service:

<img width="948" height="424" alt="Screenshot 2025-09-04 at 12 52 05 PM" src="https://github.com/user-attachments/assets/891d8890-e590-4d77-af5b-4d60699be8a4" />
<img width="1006" height="335" alt="Screenshot 2025-09-04 at 12 52 11 PM" src="https://github.com/user-attachments/assets/976b0edf-9fac-451e-9756-a30a6f8fca27" />
<img width="957" height="320" alt="Screenshot 2025-09-04 at 12 52 15 PM" src="https://github.com/user-attachments/assets/dec46118-ea8e-40b3-a42c-9f303c8f4cc4" />
<img width="943" height="314" alt="Screenshot 2025-09-04 at 12 52 20 PM" src="https://github.com/user-attachments/assets/a6690096-f9e6-4ad1-963a-8a1d4da34859" />

## order-service:

<img width="1027" height="487" alt="Screenshot 2025-09-04 at 12 53 02 PM" src="https://github.com/user-attachments/assets/ef41c03e-d70d-4bf9-9dad-29ffe979655a" />
<img width="1020" height="350" alt="Screenshot 2025-09-04 at 12 53 06 PM" src="https://github.com/user-attachments/assets/c460cbcb-4d15-4a51-b8d5-847b4abef021" />
<img width="925" height="398" alt="Screenshot 2025-09-04 at 12 53 14 PM" src="https://github.com/user-attachments/assets/06a3c7d8-7e42-4afb-8e48-00f003b4ae9d" />
<img width="991" height="483" alt="Screenshot 2025-09-04 at 12 53 19 PM" src="https://github.com/user-attachments/assets/d0077597-7b03-4143-8f96-69477371b15d" />
<img width="869" height="344" alt="Screenshot 2025-09-04 at 12 53 24 PM" src="https://github.com/user-attachments/assets/50aeac44-967d-4c53-9f34-8ddb390e57f2" />

## Run all and check

<img width="1393" height="737" alt="Screenshot 2025-09-04 at 12 54 59 PM" src="https://github.com/user-attachments/assets/34d1cc74-013d-4e04-b55b-98fdc134809b" />
<img width="754" height="181" alt="Screenshot 2025-09-04 at 12 55 26 PM" src="https://github.com/user-attachments/assets/af39bea4-775b-4c38-b57c-8b3c051b4e8b" />
