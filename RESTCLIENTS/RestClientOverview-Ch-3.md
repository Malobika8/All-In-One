

## 🚀 What Is a REST Client?

A **REST client** is something that **makes HTTP requests** to a RESTful web service and reads the responses.  
REST (REpresentational State Transfer) uses **standard HTTP methods** like:

- `GET` – Read data  
- `POST` – Create something  
- `PUT` – Update something  
- `DELETE` – Remove something  

A REST client is like saying:  
> “Hey server, give me this resource,” or “Here’s some data I want you to store.”

In Java, you write code (or use tools) to perform those HTTP operations.

---

## 🔢 3 Ways to Be a REST Client

### ✅ 1. **Java Code (Libraries and APIs)**
Use libraries like:
- `HttpClient` (Java 11+)
- Apache HttpClient
- OkHttp
- Spring RestTemplate / WebClient
- Feign, Retrofit, Unirest, etc.

### ✅ 2. **Command-Line Tools**
- `curl`, `httpie`

### ✅ 3. **GUI Tools**
- Postman, Insomnia, VS Code extensions

We’re focusing on **Java code clients**.

---

## 🧰 Java REST Clients – Full List with Purpose

Here’s a complete chart of major REST clients used in Java projects:

| REST Client               | Description                                               | Best For                         |
|---------------------------|-----------------------------------------------------------|----------------------------------|
| **HttpURLConnection**     | Very old, low-level, verbose                              | Tiny, no-dependency apps         |
| **HttpClient (Java 11+)** | Modern standard, async/sync support, part of JDK          | Most recommended if on Java 11+  |
| **Apache HttpClient**     | Powerful, connection pooling, mature                      | Enterprise and older projects    |
| **OkHttp**                | Lightweight, super fast                                   | Android / modern REST clients    |
| **Retrofit**              | Built on OkHttp, declarative                              | Clean API definitions (Android)  |
| **Spring RestTemplate**   | Blocking, simple, but deprecated                          | Legacy Spring apps               |
| **Spring WebClient**      | Reactive, non-blocking, async                             | Modern Spring apps (WebFlux)     |
| **JAX-RS Client (Jersey, RESTEasy)** | Java EE standard REST client              | Jakarta EE / enterprise stacks   |
| **Feign (Spring Cloud)**  | Declarative, interface-based, pluggable                   | Microservices (Spring Cloud)     |
| **Unirest**               | Lightweight, simple syntax                                | Quick dev/test scripts           |
| **RestAssured**           | DSL-style testing client                                  | Writing API tests in Java        |
| **Vert.x WebClient**      | Non-blocking, event-driven                                | Reactive systems (Vert.x)        |
| **Micronaut HTTP Client** | Ultra-fast, ahead-of-time compiled                        | Micronaut microservices          |

---

## 🧪 HTTPClient (Java 11+) – The Official Standard

```java
// Java 11+
HttpClient client = HttpClient.newHttpClient();
HttpRequest request = HttpRequest.newBuilder()
    .uri(URI.create("https://jsonplaceholder.typicode.com/posts/1"))
    .build();

// Synchronous call
HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());
System.out.println(response.body());

// Asynchronous call
client.sendAsync(request, HttpResponse.BodyHandlers.ofString())
    .thenApply(HttpResponse::body)
    .thenAccept(System.out::println);
```

✅ Modern, built-in, and uses **CompletableFuture** for async.

---

## 📦 Apache HttpClient – Enterprise Classic

```java
CloseableHttpClient client = HttpClients.createDefault();
HttpGet request = new HttpGet("https://jsonplaceholder.typicode.com/posts/1");

CloseableHttpResponse response = client.execute(request);
String responseBody = EntityUtils.toString(response.getEntity());
System.out.println(responseBody);
```

✅ Great when you need full control and legacy compatibility.

---

## 🟩 OkHttp – Lightweight and Fast

```java
OkHttpClient client = new OkHttpClient();
Request request = new Request.Builder()
    .url("https://jsonplaceholder.typicode.com/posts/1")
    .build();

Response response = client.newCall(request).execute();
System.out.println(response.body().string());
```

✅ Great for Android and minimalistic apps.

---

## 🟦 Retrofit – Built on OkHttp, declarative

```java
public interface PostService {
    @GET("posts/{id}")
    Call<Post> getPost(@Path("id") int id);
}

Retrofit retrofit = new Retrofit.Builder()
    .baseUrl("https://jsonplaceholder.typicode.com/")
    .addConverterFactory(GsonConverterFactory.create())
    .build();

PostService service = retrofit.create(PostService.class);
Call<Post> call = service.getPost(1);
```

✅ Just define an interface — Retrofit handles everything else.

---

## 🌱 Spring RestTemplate (Legacy)

```java
RestTemplate restTemplate = new RestTemplate();
String result = restTemplate.getForObject("https://jsonplaceholder.typicode.com/posts/1", String.class);
System.out.println(result);
```

✅ Easy and readable, but being replaced.

---

## 🌊 Spring WebClient – Reactive, async

```java
WebClient client = WebClient.create("https://jsonplaceholder.typicode.com");
String body = client.get()
    .uri("/posts/1")
    .retrieve()
    .bodyToMono(String.class)
    .block();  // .subscribe() for async

System.out.println(body);
```

✅ Powerful and non-blocking. Part of **Spring WebFlux**.

---

## 📡 Feign – Declarative Client for Spring Cloud

```java
@FeignClient(name = "postsClient", url = "https://jsonplaceholder.typicode.com")
public interface PostClient {
    @GetMapping("/posts/{id}")
    Post getPost(@PathVariable("id") int id);
}
```

✅ You just call methods — no boilerplate HTTP code!

---

## 💡 Which One Should *You* Learn First?

| Your Project Type         | Start With                |
|---------------------------|---------------------------|
| Simple / demo app         | `HttpClient (Java 11+)`   |
| Spring app (blocking)     | `RestTemplate` (legacy)   |
| Spring app (modern)       | `WebClient`               |
| Android                   | `Retrofit + OkHttp`       |
| Writing tests             | `RestAssured`             |
| You hate boilerplate      | `Feign` or `Retrofit`     |

---
