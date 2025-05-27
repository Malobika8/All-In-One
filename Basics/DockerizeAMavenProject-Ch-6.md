Let’s containerize a **Maven-based Java project** that prints "Hello World" using Docker.

---

## 🔧 Dockerize a Maven Java Project

Let’s assume your Maven project structure looks like this:

```
your-project/
├── pom.xml
└── src/
    └── main/
        └── java/
            └── com/
                └── example/
                    └── App.java
```

Where `App.java` contains:

```java
package com.example;

public class App {
    public static void main(String[] args) {
        System.out.println("Hello World");
    }
}
```

---

### ✅ 1. Create a `Dockerfile` in your project root:

```Dockerfile
# Use Maven to build the app
FROM maven:3.8.5-openjdk-17 AS build
WORKDIR /app
COPY pom.xml .
COPY src ./src
RUN mvn package -DskipTests

# Use JDK to run the app
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY --from=build /app/target/*.jar app.jar
ENTRYPOINT ["java", "-jar", "app.jar"]
```

---

### ✅ 2. Build the Docker image:

From the root of your project (where the Dockerfile is):

```bash
docker build -t my-hello-world-app .
```

---

### ✅ 3. Run the Docker container:

```bash
docker run --rm my-hello-world-app
```

You should see:

```
Hello World
```

---

### 🧠 What we’ve learned:

* Multi-stage builds (build with Maven, run with JDK)
* Using Dockerfile to containerize a Maven project
* Running a Java JAR from a Docker container

---
