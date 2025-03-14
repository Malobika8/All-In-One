# Intro

Imagine we have a client machine and a server. In web world, client sends a request to server expecting a response. It can be a string, json, html page(static(already built) or dynamic(build at runtime)) etc. When we ask for a page at runtime and send a request to the server, since the page is not kept handy as it is supposed to build at runtime, the request goes to the helper application(also called as Web Container(tomcat, glassfish, jBoss, websphere etc)). The Web Container has servlets which are basically java files that can take request from the client on the internet and send response after processing the request.

<img width="550" alt="Screenshot 2024-05-23 at 10 51 13 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/3e14a388-2d0d-4b8c-bbc7-9ce9ecf2e3f4">
<img width="517" alt="Screenshot 2024-05-23 at 10 56 34 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/90dd086b-4fc3-4d0c-aca3-5bd925e6dcef">

Inside the container has a special file called deployment descriptor web.xml where it is mentioned for which requests which servlet should be called. All of these should be configured in a file called deployment descriptor.

<img width="560" alt="Screenshot 2024-05-23 at 11 00 22 AM" src="https://github.com/Malobika8/GitDemo/assets/111234135/47ca42d5-d04b-48fa-9fe1-0a320e77ca3c">

Servlets are normal java classes which extends HttpServlet to utilize servlet features.

We can use annotations as well instead of configuring in web.xml. Mapping can be done using annotations.

## Servlet Context

### 🌐 **What is `ServletContext`?**

`ServletContext` is a special object provided by the **Servlet API** that represents the entire web application. It acts as a **global storage** and allows different parts of your app (like servlets, JSPs, filters, and listeners) to share information.

Think of it like a **shared notepad** for your whole web app — any servlet or JSP can write to it, and everyone else can read from it.

---

### 📌 **What Can You Do with `ServletContext`?**

1. **Store Global Data:**  
   You can store objects that all servlets and JSPs can access throughout the app's lifecycle.

```java
// Store data
ServletContext context = request.getServletContext();
context.setAttribute("appName", "SaveNotesApp");

// Retrieve data
String appName = (String) context.getAttribute("appName");
```

2. **Access App-Level Configuration:**  
   You can load global config parameters from `web.xml`.

```xml
<context-param>
    <param-name>appVersion</param-name>
    <param-value>1.0</param-value>
</context-param>
```

Access it in your code:

```java
String appVersion = context.getInitParameter("appVersion");
```

3. **Get the App’s Path and Resources:**  
   - Get the **context path** (the app’s base URL):  

```java
String contextPath = context.getContextPath();  // "/SaveNotesApp"
```

   - Access files in `/WEB-INF/`:

```java
InputStream is = context.getResourceAsStream("/WEB-INF/config.properties");
```

4. **Logging:**  
   No need to set up a logger — `ServletContext` has a built-in one:

```java
context.log("User logged in: " + userId);
```

---

### ⚙️ **When to Use `ServletContext`?**

- ✅ When you need **global variables** accessible to all servlets and JSPs.  
- ✅ When you want to **share configuration values** across the app.  
- ✅ For **cross-servlet communication**.  

🚫 **Avoid it** if:
- You only need data for a single user/session (use `HttpSession` instead).
- You’re using Spring — Spring’s `ApplicationContext` is a much better option for dependency injection and app-level beans.
