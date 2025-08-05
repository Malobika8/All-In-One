# ✅ JDK 15 – Most Important & Finalized Features

Here’s a quick overview of what was finalized in JDK 15:

| Feature                            | Finalized?                | Relevance to Developers       |
| ---------------------------------- | ------------------------- | ----------------------------- |
| ✅ Text Blocks                      | ✅ Final                   | ✅ Yes — for multiline strings |
| ❌ Sealed Classes                   | ❌ Preview                 | ❌ Skip for now                |
| ❌ Records                          | ❌ Still preview in JDK 15 | ❌ Skipped                     |
| ✅ Hidden Classes (JVM-level)       | ✅ Final                   | ❌ Low relevance               |
| ✅ Shenandoah GC (production-ready) | ✅ Final                   | ⚠️ Optional (for GC tuning)   |

---

## ✅ Java 15 Feature: **Text Blocks** — Finalized in JDK 15

---

### 🔹 What is a Text Block?

A **multi-line string literal** — much easier and cleaner than old multi-line strings.

#### 🔸 Old way (before Java 15):

```java
String json = "{\n" +
              "  \"name\": \"John\",\n" +
              "  \"age\": 30\n" +
              "}";
```

### ✅ New way (Java 15 — text block):

```java
String json = """
    {
      "name": "John",
      "age": 30
    }
    """;
```

* Uses triple quotes: `"""`
* Preserves formatting and indentation
* Automatically handles line breaks

---

### ✅ Works great for:

* JSON
* SQL queries
* HTML templates
* Logs or help text

---

### 🔍 Bonus: You can still use `.trim()` or `String.format()` if needed.

---

**Realistic examples** of how **Text Blocks** in Java 15+ make **SQL queries** and **logs** much cleaner and more readable.

## ✅ 1. SQL Query with Text Block

### 🔸 Before Java 15 (😩 hard to read):

```java
String sql = "SELECT id, name, salary FROM employees " +
             "WHERE department = 'Engineering' " +
             "AND salary > 100000 " +
             "ORDER BY salary DESC";
```

---

### ✅ Java 15+ using Text Block:

```java
String sql = """
    SELECT id, name, salary
    FROM employees
    WHERE department = 'Engineering'
      AND salary > 100000
    ORDER BY salary DESC
    """;
```

### ✅ Benefits:

* No more `+` and `\n`
* Readable formatting like actual SQL
* Can copy-paste from a DB client directly

---

## ✅ 2. Multi-line Logs with Text Block

### 🔸 Before Java 15 (Messy string building):

```java
String log = "ERROR: Could not process request\n" +
             "Reason: Timeout while calling external API\n" +
             "Request ID: " + requestId + "\n" +
             "User: " + user.getName();
```

---

### ✅ Java 15+ using Text Block:

```java
String log = """
    ERROR: Could not process request
    Reason: Timeout while calling external API
    Request ID: %s
    User: %s
    """.formatted(requestId, user.getName());
```

* Uses `.formatted()` for substitution (like `String.format`)
* Cleaner structure and formatting
* Easier to scan logs

---

## ✅ Bonus Tips

| Use Case  | How Text Blocks Help               |
| --------- | ---------------------------------- |
| SQL       | Keeps query readable and indented  |
| JSON      | Copy-paste from real API responses |
| Logs      | Log full request/response bodies   |
| Docs/Help | Embed help messages in CLI tools   |

---


Would you like to try a small hands-on with text blocks (e.g., build a multiline SQL or JSON string)?
Or shall we move to **JDK 16**, where **Records are finalized** (very important)?
