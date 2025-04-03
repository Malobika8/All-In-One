### **📌 About REST Clients & How to Use Them in Java**  

A **REST Client** is a tool or library that allows applications to **send HTTP requests (GET, POST, PUT, DELETE, etc.)** to RESTful APIs and process responses.  

If you're **completely new** to REST clients, this guide will explain:  
✔ What a REST client is 🔍  
✔ Different types of REST clients available in Java  
✔ How to use each with **code examples**  

---

# **🔹 1. What is a REST Client?**  
A **REST client** is responsible for **sending HTTP requests** and **receiving responses** from a RESTful API.  

✅ **Common REST Client Features**:  
- Send **GET, POST, PUT, DELETE** requests  
- Handle **JSON/XML** responses  
- Set **headers, authentication, and query parameters**  
- Support **asynchronous requests** (for better performance)  

### **📌 Example of How a REST Client Works**
1️⃣ You send a request:  
   ```http
   GET https://jsonplaceholder.typicode.com/posts/1
   ```
2️⃣ The API responds with data:  
   ```json
   {
     "userId": 1,
     "id": 1,
     "title": "Hello, World!",
     "body": "This is a sample post."
   }
   ```
---
# **🔹 2. Different REST Clients Available in Java**  
Java has multiple libraries to call REST APIs. Here's a breakdown:

| **REST Client** | **Description** | **Best For** |
|----------------|---------------|-------------|
| **Java's `HttpURLConnection`** | Built-in but low-level and verbose | Simple use cases |
| **Apache HttpClient** | More powerful, supports connection pooling | Enterprise apps |
| **OkHttp (by Square)** | Lightweight, efficient, good for Android | Modern apps |
| **Spring `RestTemplate`** | Simple and widely used in Spring (Deprecated) | Spring apps |
| **Spring `WebClient`** | Supports async calls, better than `RestTemplate` | Reactive APIs |
| **JAX-RS `Client` (Jersey/RESTEasy)** | Standard Java EE client | Java EE apps |

---

# **🔹 3. How to Use Each REST Client (Code Examples)**  

## **✅ Method 1: Java's Built-in `HttpURLConnection` (Basic)**
This is the most basic way to call an API **without external libraries**.  
### **📌 Example: Calling a GET API**
```java
import java.io.BufferedReader;
import java.io.InputStreamReader;
import java.net.HttpURLConnection;
import java.net.URL;

public class SimpleHttpClient {
    public static void main(String[] args) throws Exception {
        URL url = new URL("https://jsonplaceholder.typicode.com/posts/1");
        HttpURLConnection conn = (HttpURLConnection) url.openConnection();
        conn.setRequestMethod("GET");
        conn.setRequestProperty("Accept", "application/json");

        if (conn.getResponseCode() != 200) {
            throw new RuntimeException("Failed : HTTP error code : " + conn.getResponseCode());
        }

        BufferedReader br = new BufferedReader(new InputStreamReader(conn.getInputStream()));
        String output;
        while ((output = br.readLine()) != null) {
            System.out.println(output);
        }
        conn.disconnect();
    }
}
```
✔ **Pros**: Built-in, no extra dependencies  
❌ **Cons**: Verbose, lacks modern features  

---

## **✅ Method 2: Apache HttpClient (More Powerful)**
Apache HttpClient is **widely used for production apps** due to its advanced features like **connection pooling and timeout handling**.  

### **📌 Example: Calling a GET API**
📌 **Add dependency (Maven)**:
```xml
<dependency>
    <groupId>org.apache.httpcomponents.client5</groupId>
    <artifactId>httpclient5</artifactId>
    <version>5.2</version>
</dependency>
```
📌 **Java Code**:
```java
import org.apache.hc.client5.http.classic.methods.HttpGet;
import org.apache.hc.client5.http.classic.methods.CloseableHttpResponse;
import org.apache.hc.client5.http.impl.classic.CloseableHttpClient;
import org.apache.hc.client5.http.impl.classic.HttpClients;
import org.apache.hc.core5.http.io.entity.EntityUtils;

public class ApacheHttpClientExample {
    public static void main(String[] args) throws Exception {
        CloseableHttpClient client = HttpClients.createDefault();
        HttpGet request = new HttpGet("https://jsonplaceholder.typicode.com/posts/1");

        try (CloseableHttpResponse response = client.execute(request)) {
            String responseBody = EntityUtils.toString(response.getEntity());
            System.out.println(responseBody);
        }
    }
}
```
✔ **Pros**: Connection pooling, better error handling  
❌ **Cons**: Needs an external library  

---

## **✅ Method 3: OkHttp (Fast & Modern)**
**OkHttp** is a popular library for making HTTP calls **efficiently**.  
📌 **Add dependency (Maven)**:
```xml
<dependency>
    <groupId>com.squareup.okhttp3</groupId>
    <artifactId>okhttp</artifactId>
    <version>4.11.0</version>
</dependency>
```
📌 **Java Code**:
```java
import okhttp3.OkHttpClient;
import okhttp3.Request;
import okhttp3.Response;

public class OkHttpExample {
    public static void main(String[] args) throws Exception {
        OkHttpClient client = new OkHttpClient();
        Request request = new Request.Builder()
            .url("https://jsonplaceholder.typicode.com/posts/1")
            .build();

        try (Response response = client.newCall(request).execute()) {
            System.out.println(response.body().string());
        }
    }
}
```
✔ **Pros**: Lightweight, modern, Android-compatible  
❌ **Cons**: Requires dependency  

---

## **✅ Method 4: Spring `RestTemplate` (Deprecated)**
**Spring `RestTemplate` is now deprecated** in favor of `WebClient`, but still used in legacy apps.

📌 **Example**:
```java
import org.springframework.web.client.RestTemplate;
import org.springframework.http.ResponseEntity;

public class RestTemplateExample {
    public static void main(String[] args) {
        RestTemplate restTemplate = new RestTemplate();
        ResponseEntity<String> response = restTemplate.getForEntity("https://jsonplaceholder.typicode.com/posts/1", String.class);
        System.out.println(response.getBody());
    }
}
```
✔ **Pros**: Easy to use for simple APIs  
❌ **Cons**: Blocking, deprecated  

---

## **✅ Method 5: Spring `WebClient` (Recommended for Spring)**
**`WebClient`** is the **best** choice for modern Spring apps as it supports **async calls**.

📌 **Example**:
```java
import org.springframework.web.reactive.function.client.WebClient;

public class WebClientExample {
    public static void main(String[] args) {
        WebClient client = WebClient.create("https://jsonplaceholder.typicode.com");
        String response = client.get()
                .uri("/posts/1")
                .retrieve()
                .bodyToMono(String.class)
                .block();
        System.out.println(response);
    }
}
```
✔ **Pros**: Asynchronous, efficient  
❌ **Cons**: Spring dependency required  

---

# **🔹 4. Which REST Client Should You Use?**
| **Use Case** | **Recommended Client** |
|-------------|----------------|
| Simple built-in Java support | `HttpURLConnection` |
| High-performance, production apps | `Apache HttpClient` |
| Lightweight, modern, good for Android | `OkHttp` |
| Spring-based applications | `WebClient` (preferred) or `RestTemplate` (legacy) |
| Java EE / Jakarta EE | `JAX-RS Client` (Jersey/RESTEasy) |

---
