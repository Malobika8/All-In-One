## 🌐 What is Web Layer Testing?

**Web Layer Testing** means testing:

* Your **Controllers** (REST endpoints)
* HTTP behavior (status codes, response body, path variables, etc.)
* Without needing to start a full application

You simulate real HTTP requests and validate responses.

---

## ✅ Basic Controller Example (Common for Both)

Let’s take a simple Spring controller:

```java
package com.example.controller;

import org.springframework.web.bind.annotation.*;

@RestController
@RequestMapping("/users")
public class UserController {

    @GetMapping("/{id}")
    public String getUser(@PathVariable int id) {
        return "User: Alice";
    }
}
```

---

# 🧪 Part 1: Testing in **Spring MVC (non-Spring Boot)**

### ✅ 1. Add These Dependencies in `pom.xml`

```xml
<!-- Spring Core + Web -->
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-webmvc</artifactId>
  <version>5.3.34</version>
</dependency>

<!-- Spring Test -->
<dependency>
  <groupId>org.springframework</groupId>
  <artifactId>spring-test</artifactId>
  <version>5.3.34</version>
  <scope>test</scope>
</dependency>

<!-- JUnit 5 -->
<dependency>
  <groupId>org.junit.jupiter</groupId>
  <artifactId>junit-jupiter-api</artifactId>
  <version>5.13.3</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>org.junit.jupiter</groupId>
  <artifactId>junit-jupiter-engine</artifactId>
  <version>5.13.3</version>
  <scope>test</scope>
</dependency>
```

---

### ✅ 2. Test Using `MockMvcBuilders.standaloneSetup()`

```java
package com.example.controller;

import org.junit.jupiter.api.Test;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

public class UserControllerTest {

    @Test
    public void testGetUser() throws Exception {
        MockMvc mockMvc = MockMvcBuilders
                            .standaloneSetup(new UserController())
                            .build();

        mockMvc.perform(get("/users/1"))
               .andExpect(status().isOk())
               .andExpect(content().string("User: Alice"));
    }
}
```

✅ No full app startup
✅ No Spring Boot needed
✅ Fast, isolated test

---

# 🥾 Part 2: Testing in **Spring Boot**

### ✅ 1. Add Only This Dependency in Spring Boot

If you're using Spring Boot, **just this**:

```xml
<dependency>
  <groupId>org.springframework.boot</groupId>
  <artifactId>spring-boot-starter-test</artifactId>
  <scope>test</scope>
</dependency>
```

---

### ✅ 2. Use `@WebMvcTest` and `@Autowired MockMvc`

```java
package com.example.controller;

import org.junit.jupiter.api.Test;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.test.autoconfigure.web.servlet.WebMvcTest;
import org.springframework.test.web.servlet.MockMvc;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.get;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

@WebMvcTest(UserController.class)
public class UserControllerTest {

    @Autowired
    private MockMvc mockMvc;

    @Test
    public void testGetUser() throws Exception {
        mockMvc.perform(get("/users/1"))
               .andExpect(status().isOk())
               .andExpect(content().string("User: Alice"));
    }
}
```

✅ `@WebMvcTest` loads only controller + web layer
✅ `MockMvc` autowired — no need for manual setup
✅ Test behaves like a real HTTP call, but no full server

- @WebMvcTest → loads only the web (controller) layer
- MockMvc → lets us simulate HTTP requests and validate responses, without starting a real server

---

## 📊 Spring MVC vs Spring Boot Web Layer Testing

| Feature                  | Spring MVC (No Boot)                  | Spring Boot                           |
| ------------------------ | ------------------------------------- | ------------------------------------- |
| Setup                    | Manual (`MockMvcBuilders`)            | Auto (`@WebMvcTest`)                  |
| Full App Context?        | ❌ No                                  | ❌ No (only web layer loaded)          |
| Controller Layer Testing | ✅ Yes                                 | ✅ Yes                                 |
| Dependency Simplicity    | ❌ You add JUnit, Spring Test manually | ✅ Just use `spring-boot-starter-test` |
| Speed                    | ⚡ Very fast                           | ⚡ Very fast                           |

---

