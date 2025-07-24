### Jackson is a powerful **data-binding** library used in Spring Boot for **message conversion** — but here's the key:

---

## ✅ Jackson Core Usage

| Format   | Jackson Module                              | Purpose              |
| -------- | ------------------------------------------- | -------------------- |
| **JSON** | `jackson-databind` (default in Spring Boot) | Converts Java ↔ JSON |
| **XML**  | `jackson-dataformat-xml` (optional)         | Converts Java ↔ XML  |

---

### 🧠 By default:

Spring Boot auto-configures Jackson **for JSON** via:

```xml
<dependency>
    <groupId>com.fasterxml.jackson.core</groupId>
    <artifactId>jackson-databind</artifactId>
</dependency>
```

It wires the `MappingJackson2HttpMessageConverter`, which handles:

* `@RequestBody` → Java object from JSON
* `@ResponseBody` → JSON from Java object

---

### ✅ If you want **XML**, you need:

```xml
<dependency>
    <groupId>com.fasterxml.jackson.dataformat</groupId>
    <artifactId>jackson-dataformat-xml</artifactId>
</dependency>
```

Spring Boot will automatically detect this and use:

* `MappingJackson2XmlHttpMessageConverter`

Which handles Java ↔ XML conversion (instead of JAXB).

---

### ✅ Summary

| Use Case | Dependency Needed                      | Message Converter                        |
| -------- | -------------------------------------- | ---------------------------------------- |
| JSON     | jackson-databind (included by default) | `MappingJackson2HttpMessageConverter`    |
| XML      | jackson-dataformat-xml (optional)      | `MappingJackson2XmlHttpMessageConverter` |

---

### 📌 Bonus: If you're using JAXB instead of Jackson for XML

```xml
<dependency>
    <groupId>javax.xml.bind</groupId>
    <artifactId>jaxb-api</artifactId>
</dependency>
```

You’d use:

* `Jaxb2RootElementHttpMessageConverter`

But Spring Boot prefers **Jackson for both JSON and XML** unless configured otherwise.

---
