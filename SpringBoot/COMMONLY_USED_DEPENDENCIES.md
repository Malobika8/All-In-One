## ✅ Spring Boot Commonly Used Dependencies

### 🔹 1. **Lombok**

Reduces boilerplate code like getters, setters, constructors, etc.

```xml
<dependency>
    <groupId>org.projectlombok</groupId>
    <artifactId>lombok</artifactId>
    <version>1.18.30</version>
    <scope>provided</scope>
</dependency>
```

---

### 🔹 2. **Jackson (for JSON processing)**

📦 Core Jackson dependencies used for serializing/deserializing JSON:

#### 🔸 `jackson-databind` – Converts JSON to/from Java objects

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
</dependency>
```

#### 🔸 `jackson-core` – Core streaming JSON parser/generator

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-core</artifactId>
</dependency>
```

#### 🔸 `jackson-annotations` – Annotations like `@JsonIgnore`, `@JsonProperty`

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-annotations</artifactId>
</dependency>
```

Spring Boot starter-web already includes these **indirectly**, but you can add them explicitly if needed.

---

### 🔹 3. **Spring Boot DevTools** (for auto-restart and hot reload during dev)

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
</dependency>
```

---

### 🔹 4. **Validation (JSR-380 / Hibernate Validator)**

```xml
<dependency>
    <groupId>jakarta.validation</groupId>
    <artifactId>jakarta.validation-api</artifactId>
</dependency>
<dependency>
    <groupId>org.hibernate.validator</groupId>
    <artifactId>hibernate-validator</artifactId>
</dependency>
```

---

### 🔹 5. **Database + JPA (if using database)**

#### JDBC Driver for MySQL:

```xml
<dependency>
    <groupId>com.mysql</groupId>
    <artifactId>mysql-connector-j</artifactId>
</dependency>
```

#### Spring Boot Starter JPA:

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>
```

---

### 🔹 6. **ModelMapper** (for converting DTO ↔ Entity)

```xml
<dependency>
    <groupId>org.modelmapper</groupId>
    <artifactId>modelmapper</artifactId>
    <version>3.2.0</version>
</dependency>
```

---

### 🔹 7. **Testing Libraries**

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
</dependency>
```

---

### 🔹 5. Jakarta Annotations API – Common annotations like @PostConstruct, @PreDestroy

```xml
<dependency>
    <groupId>jakarta.annotation</groupId>
    <artifactId>jakarta.annotation-api</artifactId>
</dependency>
```

---

## 📝 Summary Table

| Purpose             | Dependency Example                                  |
| ------------------- | --------------------------------------------------- |
| Reduce boilerplate  | `lombok`                                            |
| JSON handling       | `jackson-databind`, `jackson-core`                  |
| Auto reload on save | `spring-boot-devtools`                              |
| Bean validation     | `jakarta.validation-api`, `hibernate-validator`     |
| Common annotations  | `	jakarta.annotation-api`                           |
| JPA + DB access     | `spring-boot-starter-data-jpa`, `mysql-connector-j` |
| Object mapping      | `modelmapper`                                       |
| Unit testing        | `spring-boot-starter-test`                          |

---
