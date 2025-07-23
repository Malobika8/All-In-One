# Example:

Consider the controller:

```
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestParam;

@Controller
public class MomController {

    @GetMapping("/order")
    public String order(){
        System.out.println("entered");
        return "order";
    }

    @PostMapping("/submitOrder")
    public String submitOrder(@RequestParam("order") String order, Model model){
        System.out.println("Request param: " + order);
        model.addAttribute("order", order);
        return "food";
    }
}
```

* `@Controller` (not `@RestController`)
* Returns **view names** (`"order"` and `"food"`)
* Uses `Model` to pass data to JSP/Thymeleaf/etc.
* Handles both `GET` and `POST` endpoints

This is a classic **Spring MVC (non-REST)** setup, and we’ll test it accordingly.

## ✅ Goal

Write a unit test using `MockMvc` to:

* Test `/order` returns view `"order"`
* Test `/submitOrder` accepts a form param and returns view `"food"`

### ✅ 1. Make sure you’re using:

* `spring-webmvc:6.2.8`
* `spring-test:6.2.8`
* `jakarta.servlet-api:6.0.0` ✅ (not 4.0.4)

---

### ✅ 2. Test Class for `MomController`

```java
package com.random.controller;

import org.junit.jupiter.api.Test;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;

import static org.springframework.test.web.servlet.request.MockMvcRequestBuilders.*;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.*;

public class MomControllerTest {

    @Test
    public void testOrderPage() throws Exception {
        MockMvc mockMvc = MockMvcBuilders.standaloneSetup(new MomController()).build();

        mockMvc.perform(get("/order"))
               .andExpect(status().isOk())
               .andExpect(view().name("order")); // ✅ matches return "order"
    }

    @Test
    public void testSubmitOrder() throws Exception {
        MockMvc mockMvc = MockMvcBuilders.standaloneSetup(new MomController()).build();

        mockMvc.perform(post("/submitOrder")
                .param("order", "Biryani"))
               .andExpect(status().isOk())
               .andExpect(view().name("food"))
               .andExpect(model().attribute("order", "Biryani")); // ✅ model attribute check
    }
}
```

---

## 🧠 Key Concepts:

| Line                                                   | Meaning                                                  |
| ------------------------------------------------------ | -------------------------------------------------------- |
| `MockMvcBuilders.standaloneSetup(new MomController())` | Create mock environment for the controller               |
| `view().name("food")`                                  | Checks the controller returned the correct **view name** |
| `model().attribute("order", "Biryani")`                | Checks the model has the expected data                   |

---

