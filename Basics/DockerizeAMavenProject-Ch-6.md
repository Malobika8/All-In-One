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

## ✅ Do you need to **remember** Dockerfile commands?

**No, you don’t need to memorize them.**
But you should understand **what each line does**, so you can reuse and tweak them as needed.

Think of it like **Java syntax**: you don’t remember everything, but you remember patterns like:

```java
public static void main(String[] args)
```

Similarly, Dockerfiles follow a pattern. Let’s break it down line by line.

---

## 🧱 Dockerfile Line-by-Line (explained for beginners)

```dockerfile
# 1. Use Maven and JDK to build the app
FROM maven:3.8.5-openjdk-17 AS build
```

👉 Pulls a Docker image with Maven and Java 17 preinstalled.
`AS build` gives this stage a name — “build”.

---

```dockerfile
WORKDIR /app
```

👉 Inside the container, it sets the working directory to `/app`.
Like doing `cd /app`.

---

```dockerfile
COPY pom.xml .
COPY src ./src
```

👉 Copies your Maven files from your computer to the container.

* `.` here means “copy to current WORKDIR (which is `/app`)”.
* First line copies `pom.xml`
* Second line copies your `src` directory

---

```dockerfile
RUN mvn package -DskipTests
```

👉 Runs the Maven command **inside the container** to build your project.

* It produces a `.jar` file inside `/app/target/`.

---

```dockerfile
# 2. Use JDK only to run the app (cleaner image)
FROM openjdk:17-jdk-slim
```

👉 This is a second stage! A cleaner final image with just Java (no Maven).

---

```dockerfile
WORKDIR /app
```

👉 Set working directory again for the final image.

---

```dockerfile
COPY --from=build /app/target/*.jar app.jar
```

👉 Copy the `.jar` we built earlier (from `build` stage) into this final image.

The `--from=build` part in:

```dockerfile
COPY --from=build /app/target/*.jar app.jar
```

is one of the **rare but important** places in Docker where `--` is used — and it's **not like a shell flag**, but part of Docker’s **multi-stage build syntax**.

Let me explain clearly:

---

## 🧠 What does `--from=build` mean?

### 🧱 In multi-stage Docker builds:

You define multiple stages like this:

```dockerfile
FROM maven:3.8.5-openjdk-17 AS build
# (build stuff)

FROM openjdk:17-jdk-slim
# (run stuff)
```

You give the first stage a name: `AS build`.

Then later, in the second stage, you copy something **from that earlier stage**:

```dockerfile
COPY --from=build /app/target/*.jar app.jar
```

This says:

> "Copy the `.jar` file from the previous image stage called `build` (not from your local machine)."

---

### 🔍 Why the `--`?

`COPY` normally only accepts two arguments:

```dockerfile
COPY <src> <dest>
```

But when you add `--from=...`, you're using a **flag** (like a CLI flag).
This is a special syntax **only available in multi-stage builds**.

So:

* `--from=build` → copy from the **build stage**
* Without it, Docker tries to copy from your **local system**, which will fail inside a multi-stage setup

---

## 📌 Summary

| Syntax                  | Meaning                                       |
| ----------------------- | --------------------------------------------- |
| `COPY file.txt .`       | Copy `file.txt` from local context into image |
| `COPY --from=build ...` | Copy from an earlier Docker image stage       |

So you're not writing `--` by itself — it’s part of `--from=build`, which is a required flag.

---

```dockerfile
ENTRYPOINT ["java", "-jar", "app.jar"]
```

👉 When you run the container, this is the command it will run.

---

## 🟨 Confused about `"."`? Let’s simplify:

When you do:

```bash
docker build -t my-image-name .
```

The `.` here means:

> "Build the Docker image using the Dockerfile in the **current directory** and copy content **from here** into the image."

So inside the Dockerfile, if you write:

```dockerfile
COPY pom.xml .
```

This means:

> “Copy `pom.xml` from current host directory (where you’re running `docker build`) **into** the current working directory inside the container.”

---

## 🔁 Summary

* You don’t need to memorize Dockerfile lines — just reuse and tweak based on needs.
* Understand that Dockerfile has 2 goals: **build your app**, and **prepare an image to run it**.
* `"."` means “current directory” — context matters:

  * In terminal: “build from current directory”
  * In Dockerfile: “copy to current directory in container”

---
