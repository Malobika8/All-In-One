
# 🚀 **Complete Guide to Java REST Clients**

This guide will walk you through the **best REST clients** in Java, from built-in to third-party libraries, their features, and examples of how to use them.

---

## 🧰 **1. Java 11+ `HttpClient`**

### **Overview**
Introduced in **Java 11**, `HttpClient` is a modern, built-in class in the JDK for making HTTP requests. It supports **sync** and **async** operations, uses **HTTP/2** by default, and supports **non-blocking** I/O with **`CompletableFuture`**.

### **Advantages**
- **No dependencies** — part of the standard JDK.
- Supports **synchronous** and **asynchronous** calls.
- Built-in **HTTP/2** support.
- Built on the **non-blocking IO** model with `CompletableFuture`.

### **Usage Example**

#### 1. **Synchronous HTTP GET Request**

```java
// Create an HttpClient
HttpClient client = HttpClient.newHttpClient();

// Build a request
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://jsonplaceholder.typicode.com/posts/1"))
    .build();

// Send request and get response synchronously
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());
```

#### 2. **Asynchronous HTTP GET Request**

```java
// Asynchronous call using CompletableFuture
client.sendAsync(request, HttpResponse.BodyHandlers.ofString())
    .thenApply(HttpResponse::body)
    .thenAccept(System.out::println);
```

### **When to Use**
- When you are on **Java 11+** and need modern, efficient HTTP support.
- When you need **non-blocking I/O** or want **asynchronous** calls.

---

## 🧰 **2. Apache HttpClient**

### **Overview**
Apache HttpClient is a **powerful, mature, and customizable** HTTP client for Java. It is popular for **enterprise-level** applications due to its support for **connection pooling**, **cookie management**, and **HTTP/2**.

### **Advantages**
- **Connection pooling** for reusing connections, improving performance.
- **Customizable**: Allows you to configure timeouts, retries, and other advanced options.
- **Mature** and widely used in legacy enterprise applications.

### **Usage Example**

```java
CloseableHttpClient client = HttpClients.createDefault();  // Create client
HttpGet request = new HttpGet("https://jsonplaceholder.typicode.com/posts/1");

CloseableHttpResponse response = client.execute(request);  // Send the request
String responseBody = EntityUtils.toString(response.getEntity());  // Get response
System.out.println(responseBody);
```

### **When to Use**
- When you need **advanced features** like **connection pooling**, **custom timeouts**, or more control over the HTTP requests.
- For **legacy systems** or **enterprise applications** that need robust, full-featured HTTP support.

---

## 🧰 **3. OkHttp**

### **Overview**
OkHttp is a **lightweight** and **efficient** HTTP client for Java, widely used for mobile applications (especially **Android**). It supports features like **HTTP/2**, **connection pooling**, and **web socket** support.

### **Advantages**
- **Lightweight** and fast.
- Supports **HTTP/2** and **connection pooling**.
- **Good integration** with Android.
- **Simple API** for making requests.

### **Usage Example**

```java
OkHttpClient client = new OkHttpClient();  // Create client

Request request = new Request.Builder()
    .url("https://jsonplaceholder.typicode.com/posts/1")
    .build();

Response response = client.newCall(request).execute();  // Send request
System.out.println(response.body().string());  // Print response
```

### **When to Use**
- Ideal for **mobile apps** or **Android** development.
- When you need **lightweight** and **efficient** HTTP handling with **HTTP/2**.

---

## 🧰 **4. Retrofit**

### **Overview**
Retrofit is a **declarative** HTTP client built on top of **OkHttp**. It simplifies API consumption by allowing you to define **interfaces** for your endpoints, and it handles all the **networking** internally.

### **Advantages**
- **Declarative** approach using interfaces.
- **Integration with Gson** or other converters.
- Supports **synchronous** and **asynchronous** calls.
- Built on **OkHttp**, so it inherits all OkHttp’s advantages.

### **Usage Example**

```java
// Define your interface
public interface PostService {
    @GET("posts/{id}")
    Call<Post> getPost(@Path("id") int id);
}

// Create Retrofit instance
Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("https://jsonplaceholder.typicode.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .build();

// Create service instance
PostService service = retrofit.create(PostService.class);
Call<Post> call = service.getPost(1);  // Request

Response<Post> response = call.execute();  // Synchronous call
System.out.println(response.body());
```

### **When to Use**
- When you want a **clean, declarative** API that simplifies network calls.
- When you need **integration with converters** like Gson or Moshi for easy data binding.

---

## 🧰 **5. Spring RestTemplate** (Deprecated)

### **Overview**
RestTemplate is a simple **blocking** HTTP client in the Spring Framework, providing convenience methods for HTTP requests. It has been **deprecated** in favor of **Spring WebClient** (which supports reactive programming).

### **Advantages**
- Easy to use and integrate within Spring apps.
- Provides a wide range of methods for all HTTP operations (`GET`, `POST`, `PUT`, etc.).
- Simpler than other libraries for **basic REST calls**.

### **Usage Example**

```java
RestTemplate restTemplate = new RestTemplate();
String result = restTemplate.getForObject("https://jsonplaceholder.typicode.com/posts/1", String.class);
System.out.println(result);
```

### **When to Use**
- For **legacy** Spring applications where **non-blocking** operations are not required.

---

## 🧰 **6. Spring WebClient** (Modern Alternative to RestTemplate)

### **Overview**
WebClient is part of **Spring WebFlux** and provides a **reactive, non-blocking** HTTP client. It supports **synchronous** and **asynchronous** operations, and is designed for **highly scalable, non-blocking applications**.

### **Advantages**
- Supports **asynchronous** and **reactive** programming.
- Fully integrated into **Spring WebFlux**.
- Works with **Mono** and **Flux** for handling streams of data.

### **Usage Example**

```java
WebClient client = WebClient.create("https://jsonplaceholder.typicode.com");
String response = client.get()
    .uri("/posts/1")
    .retrieve()
    .bodyToMono(String.class)
    .block();  // Blocking call (use subscribe() for non-blocking)
System.out.println(response);
```

### **When to Use**
- For **reactive, non-blocking** applications in Spring WebFlux.
- When you need full **asynchronous** support.

---

## 🧰 **7. Feign (Spring Cloud)**

### **Overview**
Feign is a **declarative** HTTP client built for **microservices** using **Spring Cloud**. It allows you to declare REST endpoints via **interfaces**, and it abstracts away the HTTP calls for you.

### **Advantages**
- Simplifies **microservice communication**.
- Supports **client-side load balancing**, making it great for **distributed systems**.
- Easily integrates with **Spring Cloud**.

### **Usage Example**

```java
@FeignClient(name = "postsClient", url = "https://jsonplaceholder.typicode.com")
public interface PostClient {
    @GetMapping("/posts/{id}")
    Post getPost(@PathVariable("id") int id);
}

// Auto-wired into Spring services
```

### **When to Use**
- In **Spring Cloud** based microservices, especially for **declarative** HTTP calls.
- When you need **client-side load balancing** or integration with **Eureka**, **Ribbon**, etc.

---

## 🧰 **8. RestAssured**

### **Overview**
RestAssured is a **DSL (Domain-Specific Language)** for **testing** REST APIs in Java. It simplifies writing tests for REST services, making it easier to validate API responses and assertions.

### **Advantages**
- Excellent for **testing** REST APIs.
- Clean, **fluent syntax** for assertions.
- Integrates easily with **JUnit** or other testing frameworks.

### **Usage Example**

```java
given()
    .when()
    .get("https://jsonplaceholder.typicode.com/posts/1")
    .then()
    .statusCode(200)
    .body("id", equalTo(1));  // Assert the response
```

### **When to Use**
- When you are writing **tests** for REST APIs.
- For **behavior-driven testing** in CI/CD pipelines.

---

## 🧰 **9. Unirest**

### **Overview**
Unirest is a **lightweight**, easy-to-use HTTP client for **quick development**. It supports **JSON**, **XML**, and **Form data**, and it is great for **rapid prototyping**.

### **Advantages**
- **Simple, minimalistic API**.
- Supports **JSON**, **XML**, and **Form data**.
- **Non-blocking** if needed (via `Async` methods).

### **Usage Example**

```java
HttpResponse<JsonNode> response = Unirest.get("https://jsonplaceholder.typicode.com/posts/1")
    .asJson();

System.out.println(response.getBody().getObject().getString("title"));
```

### **When to Use**
- When you need **quick development** without much boilerplate code.
- Great for **small projects** or testing.

---

### 🧪 **Summary: Which One to Use?**

| Use Case                    | Recommended Client          |
|-----------------------------|-----------------------------|
| Simple app                  | **HttpClient (Java 11+)**   |
| Legacy Spring app           | **RestTemplate** (deprecated) |
| Reactive Spring app         | **Spring WebClient**        |
| Android                     | **Retrofit** + **OkHttp**   |
| Microservices with Spring   | **Feign**                   |
| API testing                 | **RestAssured**             |
| Quick HTTP calls            | **Unirest**                 |

---

