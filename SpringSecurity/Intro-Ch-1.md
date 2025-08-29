## Prerequisites

- Spring Core
- Spring MVC
- Spring MVC Intermediate
- Spring JDBC
  
# Spring Security

Spring Security is a comprehensive security framework for Java-based web applications built on the Spring Framework. It provides robust authentication and authorization capabilities, 
allowing developers to secure their applications with ease. Spring Security offers a wide range of features, including user authentication, role-based access control, password 
encryption, and more. It also integrates seamlessly with other Spring-based frameworks, making it a popular choice for building secure web applications. By using Spring Security, 
developers can focus on building their application's core functionality while ensuring the security and integrity of their data.  

<img width="1126" alt="Screenshot 2024-06-26 at 11 37 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/48519af9-9610-4daf-86c4-e074bdf1b168">
<img width="1136" alt="Screenshot 2024-06-26 at 11 38 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a2e39188-2946-4941-a72c-0433bbbb5b0d">
<img width="1130" alt="Screenshot 2024-06-26 at 11 39 41 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/578ed415-fc42-45bb-9844-f543e5a5e548">
<img width="1129" alt="Screenshot 2024-06-26 at 11 42 05 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c454e640-1792-4452-9991-27b59f894e02">

# Let's configure Spring Security with SpringMVC

1. *Create a simple SpringMVC App.*
   
   - **pom.xml**
  
     Dependencies required:

     <!-- https://mvnrepository.com/artifact/org.springframework/spring-webmvc -->
          <dependency>
              <groupId>org.springframework</groupId>
              <artifactId>spring-webmvc</artifactId>
              <version>${spring.version}</version>
           </dependency>
     <!-- https://mvnrepository.com/artifact/jakarta.servlet/jakarta.servlet-api -->
          <dependency>
              <groupId>jakarta.servlet</groupId>
              <artifactId>jakarta.servlet-api</artifactId>
              <version>6.1.0</version>
              <scope>provided</scope>
          </dependency>

      Spring Security dependencies:
   
      <!-- https://mvnrepository.com/artifact/org.springframework.security/spring-security-config -->
          <dependency>
              <groupId>org.springframework.security</groupId>
              <artifactId>spring-security-config</artifactId>
              <version>${spring-security.version}</version>
          </dependency>
      <!-- https://mvnrepository.com/artifact/org.springframework.security/spring-security-web -->
         <dependency>
              <groupId>org.springframework.security</groupId>
              <artifactId>spring-security-web</artifactId>
              <version>${spring-security.version}</version>
          </dependency>
          <dependency>
              <groupId>org.springframework.security</groupId>
              <artifactId>spring-security-core</artifactId>
              <version>${spring-security.version}</version>
          </dependency>
    
       #### Spring security versions are not in sync with other Spring dependencies. We need to check and make sure version are compatible.

       <img width="1025" alt="Screenshot 2024-06-26 at 1 02 47 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/608f2845-f393-40f2-b028-5890966147a6">

   - **MyAppConfig**

     <img width="988" alt="Screenshot 2024-06-26 at 11 31 35 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/93463557-fd46-4f7c-bfee-bb0b31cdf422">

   - **HelloWorldController**

     <img width="1047" alt="Screenshot 2024-06-26 at 11 35 19 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/9eb340b0-e903-4ad1-bbd0-2dfee87b214c">

   - **WebAppInitializer**
  
     <img width="1000" alt="Screenshot 2024-06-26 at 11 32 16 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/25e8d86e-5fbe-49bd-99cc-ca6bd835aebb">

   - **hello-world.jsp**

     <img width="772" alt="Screenshot 2024-06-26 at 11 33 03 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ee39fc76-2d09-42d5-bbf9-c88d299ba24a">

   - **Run the Application**
  
     <img width="1347" alt="Screenshot 2024-06-26 at 11 33 12 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/eafb947a-3f67-453b-9d24-d784d765ac41">
     <img width="1213" alt="Screenshot 2024-06-26 at 11 33 19 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/8ec79d2c-f8bf-4aa3-be9b-29329c045258">

1. *Let's try to secure these url's by designing Spring Security filter (This internally uses Servlet Filter).*
   
   <img width="645" alt="Screenshot 2024-06-26 at 11 35 42 AM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ee7c8dfd-3b48-4dd3-9d00-2a6e9c5cfa11">

   - #### Create Spring Security config file

     <img width="1134" alt="Screenshot 2024-06-26 at 12 04 22 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2f7c402f-5cd7-4231-9073-a770bed02e5d">
   
     ##### *@EnableWebSecurity* creates Spring security filter chain

     <img width="911" alt="Screenshot 2024-06-26 at 12 52 09 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/55e6b982-8029-4ada-9d33-1b591aeadec8">
     <img width="1045" alt="Screenshot 2024-06-26 at 12 52 47 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/91011f1a-b100-4e24-8935-26fd90073ba1">

     ##### Creates a bean named "springSecurityFilterSecurityChain

     <img width="1058" alt="Screenshot 2024-06-26 at 12 54 35 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/70b99aa1-1d26-4c4f-a801-cd184af26ce8">

     <img width="1126" alt="Screenshot 2024-06-26 at 12 07 35 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/b6adb9ad-a0fb-42cc-a556-cad5e7b2d529">

   - #### Register the Spring Security Filter chain to our App

     <img width="823" alt="Screenshot 2024-06-26 at 12 10 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a4702cf3-763c-49b2-9de7-56d88147c2e8">
     <img width="922" alt="Screenshot 2024-06-26 at 12 22 15 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/c8a20352-cd76-4665-847d-e6a3a6ffe3a9">
  
     Takes the *springSecurityFilterChain* bean and registers it
     
     <img width="1049" alt="Screenshot 2024-06-26 at 12 48 39 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f835b5e7-26fd-4e4d-8cae-f61ff66afd18">
     <img width="1052" alt="Screenshot 2024-06-26 at 12 49 36 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f9a36d6f-1779-4194-b45c-1375bb6db105">
   

2. *Run the Application*

   <img width="1338" alt="Screenshot 2024-06-26 at 12 24 13 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/ff3d8e80-7b0e-4875-8fca-38fea6fbaf84">

   Spring's default login page. We cannot bypass this.
   
   <img width="848" alt="Screenshot 2024-06-26 at 12 24 18 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/66b3fc31-5abe-47ea-9ce3-d28cd5bdad2b">
   <img width="810" alt="Screenshot 2024-06-26 at 12 26 54 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/e39ca8a5-0c15-4e39-b861-a044d84421b9">

## Observation

   We can see the filter that are used by enabling debug.

   <img width="664" alt="Screenshot 2024-06-26 at 12 28 53 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/2a9b8e00-c4d7-4dd8-b617-307af6ba10d0">
   <img width="639" alt="Screenshot 2024-06-26 at 12 29 45 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/f9eddcde-d135-4cb0-ba5f-5405832cb926">
   <img width="935" alt="Screenshot 2024-06-26 at 12 30 15 PM" src="https://github.com/Malobika8/All-In-One/assets/111234135/a245ba36-4441-4e22-a7d6-763e0bd54a3d">

   ### Which class executes first Springinitializer or MySpringConfig?

   - SpringInitializer

   ------------
   SpringInitializer(This boots up our Spring Security Application. It registers Spring Security filter chain) **------->** MySecurityConfig(Helps create Filter chain)
   ------------

   We can also do XML config for the same.

---

Let’s carefully unpack **what “registering the filter chain” means in Spring Security**.

### 1. The `springSecurityFilterChain` Bean

* When you add `@EnableWebSecurity`, Spring Security **creates a bean of type `FilterChainProxy`**.
* This bean is actually named `springSecurityFilterChain`.
* It’s a **Servlet `Filter`** — so it can intercept HTTP requests before they reach your controllers.

---

### 2. Registering the Filter Chain with the Servlet Container

* A plain Spring `Filter` bean is **not automatically applied** to web requests.
* To make it active, it needs to be **registered with the Servlet container** (Tomcat, Jetty, etc.).
* This is done by **`DelegatingFilterProxy`**, which is a special bridge between the Servlet container and Spring.

---

### 3. Where `SpringInitializer` Comes In

* In a Spring Boot (or `SpringInitializer` in non-Boot apps), you extend `AbstractSecurityWebApplicationInitializer`.
* This initializer registers a `DelegatingFilterProxy` in the `ServletContext`.
* That proxy is mapped to all URL patterns (`/*`).
* The proxy **looks up the bean named `springSecurityFilterChain`** in the Spring context and delegates filtering to it.

So:

* **SpringInitializer** → registers `DelegatingFilterProxy` with servlet container.
* **DelegatingFilterProxy** → delegates work to `springSecurityFilterChain` bean.
* **springSecurityFilterChain** → contains your security filter chain logic.

---

### 4. What “Registering the Filter Chain” Really Means

When we say “registering the filter chain”:

* It means **telling the Servlet container**:
  *“Before any request reaches my controllers, run it through the Spring Security filter chain.”*
* Technically:

  * A `DelegatingFilterProxy` is registered in the container.
  * That proxy points to the Spring-managed bean `springSecurityFilterChain`.
  * Now, Spring Security’s entire chain of filters (authentication, CSRF, etc.) will execute on every request.

---

✅ In short:
“Registering the filter chain” doesn’t just mean *creating the bean*. It means:

1. Create the `springSecurityFilterChain` bean (a `FilterChainProxy`).
2. Register a `DelegatingFilterProxy` with the servlet container.
3. That proxy forwards all web requests into the Spring-managed filter chain.

---

### 🔄 Request Flow Diagram

```
   [Browser]
      |
      v
[Servlet Container]  (e.g. Tomcat)
      |
      |  (DelegatingFilterProxy is registered by SpringInitializer)
      v
[DelegatingFilterProxy]  --> looks for bean named "springSecurityFilterChain"
      |
      v
[springSecurityFilterChain]  (FilterChainProxy)
      |
      |--> [Security Filters in order]
      |       - UsernamePasswordAuthenticationFilter
      |       - CsrfFilter
      |       - ExceptionTranslationFilter
      |       - SecurityContextPersistenceFilter
      |       - ... (etc, based on config)
      |
      v
[DispatcherServlet / Your Controllers]
      |
      v
   [Response]
```

---

### 🔑 Step-by-step

1. **Browser sends request** → hits Servlet container (Tomcat/Jetty/etc.).
2. **Servlet container sees a registered filter** (`DelegatingFilterProxy`) mapped to `/*`.
3. **DelegatingFilterProxy** → delegates to Spring-managed bean `springSecurityFilterChain`.
4. **springSecurityFilterChain (FilterChainProxy)** → runs a **list of security filters** (auth, csrf, session, etc.) configured in your `MySecurityConfig`.
5. If everything passes → request continues to your controller.
6. If security fails → one of the filters returns an error response (e.g., 403 Forbidden, redirect to login, etc.).

---

✅ So when we say **“registering the filter chain”**:
It means **hooking Spring Security’s `FilterChainProxy` (`springSecurityFilterChain`) into the Servlet container request flow via `DelegatingFilterProxy`**.

---

