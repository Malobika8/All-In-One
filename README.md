## ✅ Phase 1: Foundation Setup (Goal: Be ready to test)

Start with:

1. **JUnit Basics** 🧪
2. **Mockito Basics** 🎭
3. Setting up a **Spring Boot project for testing**

## ✅ Phase 2: Types of Testing (One by One)

1. **Unit Testing** – Isolated, fast (e.g. Service layer)
2. **Web Layer Testing** – With `@WebMvcTest` + `MockMvc`
3. **Repository Testing** – Using `@DataJpaTest`
4. **Integration Testing** – With `@SpringBootTest`
5. **End-to-End Testing** – Full app test with `TestRestTemplate`
6. **Behavior Testing (Optional)** – Cucumber, Gherkin (if time allows)

## ✅ Phase 3: Real-World Coverage

* Validation errors
* Exception testing
* Mocking dependencies
* Test coverage & best practices
* Interview-level case studies

---

## ✅ What is JUnit Jupiter?

`JUnit Jupiter` is the **new programming and extension model** introduced in **JUnit 5**. JUnit 5 is split into multiple modules (unlike JUnit 4 which was just one JAR).

Here’s a breakdown:

| Component                   | Description                                                                             |
| --------------------------- | --------------------------------------------------------------------------------------- |
| 🧪 **junit-jupiter-api**    | Contains the **annotations and assertion methods** — like `@Test`, `assertEquals`, etc. |
| ⚙️ **junit-jupiter-engine** | The **runtime engine** that actually **runs the tests** written with the Jupiter API.   |

So:

* `junit-jupiter-api` lets you **write** tests.
* `junit-jupiter-engine` is what the IDE or build tool (like Maven) uses to **run** those tests.

Without the engine, tests won’t be discovered/executed even though they compile fine.

Add both dependencies to your `pom.xml`:

```xml
<dependencies>
  <!-- JUnit Jupiter API: lets you write tests -->
  <dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-api</artifactId>
    <version>5.13.3</version>
    <scope>test</scope>
  </dependency>

  <!-- JUnit Jupiter Engine: lets Maven or your IDE run the tests -->
  <dependency>
    <groupId>org.junit.jupiter</groupId>
    <artifactId>junit-jupiter-engine</artifactId>
    <version>5.13.3</version>
    <scope>test</scope>
  </dependency>
</dependencies>
```

Also, make sure you’re using the **`@Test`** annotation from JUnit 5 and not JUnit 4:

```java
import org.junit.jupiter.api.Test; // ✅ Not junit.framework
import static org.junit.jupiter.api.Assertions.assertEquals;
```

### 🧪 Once You Add This:

You should be able to:

* Use `@Test`
* Use `assertEquals`
* See the tests run from your IDE or via `mvn test`

---
