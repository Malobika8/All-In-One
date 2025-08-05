## ✅ `HttpClient` API – Basics

Java 11 introduced a **new HTTP Client API** under the package `java.net.http`.

It supports:

* Synchronous and asynchronous requests
* HTTP/1.1 and HTTP/2
* Easy handling of headers, methods, response bodies

---

### 🔹 Step 1: Create a Simple GET Request

Let’s begin with the **simplest** case — a **synchronous GET request** to a public API.

### ✅ Example: Basic GET

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class HttpClientExample {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newHttpClient();

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://jsonplaceholder.typicode.com/posts/1"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println("Status Code: " + response.statusCode());
        System.out.println("Response Body:\n" + response.body());
    }
}
```

---

### 🔍 What is happening?

* `HttpClient.newHttpClient()` → creates a new HTTP client instance.
* `HttpRequest.newBuilder()` → creates a request.
* `.uri(...)` → sets the target URL.
* `client.send(request, handler)` → sends the request synchronously.
* `BodyHandlers.ofString()` → tells the client to convert the response body to a `String`.

---

## 🕰️ **Before Java 11: What was used instead of HttpClient?**

Prior to Java 11, developers used:

### 🔸 1. `HttpURLConnection` (Since Java 1.1)

```java
URL url = new URL("https://example.com");
HttpURLConnection con = (HttpURLConnection) url.openConnection();
con.setRequestMethod("GET");
int status = con.getResponseCode();
BufferedReader in = new BufferedReader(new InputStreamReader(con.getInputStream()));
// ...read response manually
```

### 🔹 Problems:

* Verbose and boilerplate-heavy
* Poor support for modern features (e.g., HTTP/2, async)
* Manually handle streams and encoding

---

### 🔸 2. Third-party libraries were popular:

* **Apache HttpClient**
* **OkHttp**
* **Spring’s RestTemplate or WebClient**

These libraries offered:

* Better usability
* Async support
* Retry mechanisms
* JSON parsing integration

---

## ✅ Java 11 Introduced the Modern HTTP API:

The following **new classes** were introduced in the `java.net.http` package:

| Class                        | Description                                          |
| ---------------------------- | ---------------------------------------------------- |
| `HttpClient`                 | Used to send requests and receive responses          |
| `HttpRequest`                | Represents the HTTP request                          |
| `HttpResponse<T>`            | Represents the HTTP response (with body of type `T`) |
| `HttpRequest.BodyPublishers` | For sending data in requests (e.g., JSON body)       |
| `HttpResponse.BodyHandlers`  | For handling responses (e.g., string, file)          |

---

### ✅ Advantages of Java 11 `HttpClient`:

* Supports **HTTP/1.1 and HTTP/2**
* Supports both **sync and async** requests
* Cleaner API with **Streams** and **Lambdas**
* Supports **timeout**, **redirects**, **headers**, etc.
* No external dependencies

---

## ✅ Is Apache HttpClient different from Java 11 `HttpClient`?

**Yes, 100% different.**

### 🔸 Apache HttpClient

* A **third-party library** provided by the Apache Software Foundation
* Package: `org.apache.http.client.*`
* Must be added manually via Maven/Gradle
* Used widely in enterprise apps before Java 11

### 🔸 Java 11 `HttpClient`

* A **standard JDK feature**
* Package: `java.net.http.*`
* No external dependency needed
* Introduced in **Java 9 (incubating)** → **final in Java 11**

---

## 🤔 If Apache HttpClient existed, why did Java need a new one?

### ✅ 1. **Standardization in the JDK**

* Prior to Java 11, the JDK’s own `HttpURLConnection` was **old, clunky, and low-level**
* Developers **had no modern, built-in alternative**
* Java needed a **clean, modern, and standard** HTTP client as part of the language itself

---

### ✅ 2. **Better Design**

Java 11’s `HttpClient`:

* Uses a **builder pattern** → clean, readable code
* Supports **HTTP/2 natively**
* Provides both **sync and async** support out-of-the-box
* Uses **non-blocking I/O** under the hood (`CompletableFuture`)

Apache’s one is powerful but:

* Verbose in configuration
* Not standardized
* Requires dependency management

---

### ✅ 3. **No External Dependency**

Projects that want to **avoid third-party dependencies** (e.g., in banks, secure environments) now have a native solution.

---

## ✅ Summary Table:

| Feature                    | Apache HttpClient       | Java 11 `HttpClient`          |
| -------------------------- | ----------------------- | ----------------------------- |
| Source                     | Third-party library     | Built into JDK                |
| Package                    | `org.apache.http.*`     | `java.net.http.*`             |
| HTTP/2 Support             | With config             | Native                        |
| Async Support              | Yes                     | Yes (via `CompletableFuture`) |
| Stream-based Body Handling | Limited                 | Native                        |
| Dependency                 | External (Maven/Gradle) | None (JDK only)               |

---

Perfect — here's a **clear side-by-side comparison** between **Apache HttpClient** and **Java 11 HttpClient**, both conceptually and with real code examples.

---

## ✅ 1. **Basic Comparison Table**

| Feature / Aspect             | Java 11 `HttpClient`                  | Apache HttpClient (`org.apache.http`)   |
| ---------------------------- | ------------------------------------- | --------------------------------------- |
| **Availability**             | Built-in since Java 11                | Third-party library                     |
| **Package**                  | `java.net.http`                       | `org.apache.http.client`                |
| **Requires Maven/Gradle?**   | ❌ No                                  | ✅ Yes                                   |
| **HTTP/2 support**           | ✅ Native support                      | ⚠️ Limited (extra setup or not native)  |
| **Async support**            | ✅ Yes (`CompletableFuture`)           | ✅ Yes (with `HttpAsyncClient`)          |
| **Timeout, Redirects, etc.** | ✅ Built-in configuration              | ✅ Rich features                         |
| **Streaming body**           | ✅ Built-in                            | ⚠️ Possible but more verbose            |
| **JSON integration**         | ❌ Use with Jackson or Gson separately | ❌ Same                                  |
| **Learning Curve**           | ✅ Simple, clean, modern               | ⚠️ Verbose, config-heavy                |
| **Industry usage**           | ✅ Growing (modern apps)               | ✅ Widely used in legacy/enterprise apps |

---

## ✅ 2. Code Comparison – Synchronous GET Request

---

### ✅ Java 11 HttpClient:

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;

public class JavaHttpClientExample {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClient.newHttpClient();
        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://jsonplaceholder.typicode.com/posts/1"))
                .build();

        HttpResponse<String> response = client.send(request, HttpResponse.BodyHandlers.ofString());

        System.out.println("Status code: " + response.statusCode());
        System.out.println("Body:\n" + response.body());
    }
}
```

---

### ✅ Apache HttpClient (5.x or 4.x):

**Maven Dependency** (if not present):

```xml
<dependency>
    <groupId>org.apache.httpcomponents.client5</groupId>
    <artifactId>httpclient5</artifactId>
    <version>5.2</version>
</dependency>
```

**Java Code:**

```java
import org.apache.hc.client5.http.classic.methods.HttpGet;
import org.apache.hc.client5.http.classic.HttpClient;
import org.apache.hc.client5.http.impl.classic.HttpClients;
import org.apache.hc.core5.http.io.entity.EntityUtils;
import org.apache.hc.core5.http.ClassicHttpResponse;

public class ApacheHttpClientExample {
    public static void main(String[] args) throws Exception {
        HttpClient client = HttpClients.createDefault();
        HttpGet request = new HttpGet("https://jsonplaceholder.typicode.com/posts/1");

        try (ClassicHttpResponse response = client.executeOpen(null, request, null)) {
            System.out.println("Status code: " + response.getCode());
            System.out.println("Body:\n" + EntityUtils.toString(response.getEntity()));
        }
    }
}
```

---

## ✅ Which one should I use?

| Scenario                                       | Recommendation                   |
| ---------------------------------------------- | -------------------------------- |
| Modern Java (Java 11+)                         | ✅ Use `java.net.http.HttpClient` |
| Java 8 or older projects                       | ❌ Java HttpClient not available  |
| Enterprise app using Apache stack already      | ✅ Stick to Apache HttpClient     |
| Want minimal dependencies                      | ✅ Use Java 11 HttpClient         |
| Need features like connection pooling, retries | ✅ Apache HttpClient is richer    |

---

Java 11’s `HttpClient` has **first-class support for asynchronous requests** using `CompletableFuture`.

## ✅ Java 11 HttpClient — Asynchronous Requests

### 🔹 Use `sendAsync()` instead of `send()`

* `send()` → blocks and waits for the response (synchronous)
* `sendAsync()` → **non-blocking**, returns a `CompletableFuture<HttpResponse<T>>`

---

## ✅ Example: Asynchronous GET request

```java
import java.net.URI;
import java.net.http.HttpClient;
import java.net.http.HttpRequest;
import java.net.http.HttpResponse;
import java.util.concurrent.CompletableFuture;

public class AsyncHttpExample {
    public static void main(String[] args) {
        HttpClient client = HttpClient.newHttpClient();

        HttpRequest request = HttpRequest.newBuilder()
                .uri(URI.create("https://jsonplaceholder.typicode.com/posts/1"))
                .build();

        CompletableFuture<HttpResponse<String>> future = client.sendAsync(
                request, HttpResponse.BodyHandlers.ofString()
        );

        future.thenApply(HttpResponse::body)
              .thenAccept(body -> System.out.println("Response:\n" + body))
              .join(); // Wait for it to finish (only for demo)

        System.out.println("Request sent! (non-blocking)");
    }
}
```

---

### 🔍 Explanation:

* `sendAsync(...)` → Immediately returns a `CompletableFuture`
* `.thenApply()` → Transforms the response (`HttpResponse → body`)
* `.thenAccept()` → Consumes the body
* `.join()` → Blocks the main thread just for demonstration (not needed in real apps like web servers)

---

### ✅ Advantages of `sendAsync()`:

* Non-blocking I/O
* Easily combine with other `CompletableFuture`s
* Great for web servers, GUI apps, parallel requests, etc.

---
