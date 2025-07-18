# What is Spring Boot, and how is it different from Spring Framework? Explain its key features and benefits in real-world projects.

### Sol:

**Spring Boot is an opinionated extension of the Spring Framework** that simplifies application development by eliminating boilerplate configurations.

#### Key Features:

1. **Auto-Configuration**
   * Automatically configures beans (like `EntityManagerFactory`, `DataSource`, etc.) based on classpath and properties

2. **Starter Dependencies**
   * Example: `spring-boot-starter-web` brings Spring MVC + Jackson + Tomcat
   * Ensures version compatibility using `spring-boot-starter-parent`

3. **Embedded Servers**
   * Comes with embedded Tomcat, Jetty, or Undertow — no need to deploy WAR files

4. **Production-Ready Features**
  * Includes Actuator for monitoring, health checks, metrics

5. **Minimal Configuration**
  * Convention over configuration — sensible defaults unless overridden

6. **Executable JARs**
  * You can run a Spring Boot app using `java -jar`

> “Spring Boot makes Spring application development faster and easier by using auto-configuration, starter dependencies, and embedded servers. It removes the need for boilerplate XML or Java config, and enables rapid development of stand-alone, production-ready apps.”

---

# What does `@SpringBootApplication` do? Also, write a minimal Spring Boot app that prints `"App Started!"` on startup.

### Sol:


