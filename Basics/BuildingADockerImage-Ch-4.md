## 🧱 Dockerfile & Building Your First Image

Let’s create a simple Java app, package it with a Dockerfile, and build our own image from scratch.

---

### ✅ 1. Create a Simple Java App

Let’s keep it dead simple:

#### 📄 `HelloWorld.java`

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("🚀 Hello from inside Docker!");
    }
}
```

---

### ✅ 2. Compile the Java file

Compile it on your machine (assuming you have JDK installed):

```bash
javac HelloWorld.java
```

This will create a `HelloWorld.class` file.

> ❗️ If you don't have Java installed on your system, no worries — I’ll show how to compile it *inside Docker* too.

---

### ✅ 3. Create the Dockerfile

This tells Docker **how to build your image**.

#### 📄 `Dockerfile`

```Dockerfile
# Use official OpenJDK base image
FROM openjdk:11-jdk

# Set working directory inside the container
WORKDIR /app

# Copy the compiled .class file into the image
COPY HelloWorld.class .

# Set the default command to run your app
CMD ["java", "HelloWorld"]
```
---

##### ✅ A. `FROM openjdk:11-jdk` — **This is the base image name**

Yes! This line means:

> “Start with the official Docker image that has Java 11 JDK pre-installed.”

* `openjdk` → Image name
* `11-jdk` → Image **tag** (version with full JDK tools)
* Docker pulls this image from Docker Hub: [https://hub.docker.com/\_/openjdk](https://hub.docker.com/_/openjdk)

🧠 Think of this as your **starting point**. You’re adding your code on top of this ready-made Java environment.

---

##### ✅ B. `WORKDIR /app` — **We can name this anything**

* This sets the **working directory inside the container**.
* `/app` is just a convention (like `C:\Project` or `~/myapp`).
* You can call it `/myapp`, `/hello`, `/code`, etc.

📦 Any future `COPY`, `RUN`, or `CMD` instructions **will happen inside this folder**.

---

##### ✅ C. `COPY HelloWorld.class .` — **We're copying into `/app`**

Here’s what happens:

* `HelloWorld.class` — This is the file **on your local system**
* `.` — Refers to the current `WORKDIR` inside the image (`/app`)

So this command copies the file from your local machine into `/app` inside the image.

> 🧠 If you said `COPY HelloWorld.class /app/HelloWorld.class`, it would mean the same thing in this context.

---

##### ✅ D. `CMD ["java", "HelloWorld"]` — **Tells Docker what to run**

* `CMD` sets the **default command** that will run when the container starts.
* In this case, it runs:

  ```bash
  java HelloWorld
  ```

  inside the `/app` directory (which has the `.class` file).

⚙️ Docker converts this line into a shell command inside the container when it runs.

> ❗️Note: You do **not** include `.class` or `.java` in the name — just `HelloWorld`, because `java` runs the class by its name.

✅ CMD stands for "Command"
- In Docker, CMD specifies the default command to run when a container starts from the image.

📝 Additional Notes:
- You can override this command at runtime:
  ```
  docker run my-java-app java AnotherClass
  ```
- There can only be one CMD in a Dockerfile. If you define multiple, only the last one is used.
- 
---

### 🧠 TL;DR Summary

| Dockerfile Line | Meaning                                             |
| --------------- | --------------------------------------------------- |
| `FROM`          | Start with a Java environment                       |
| `WORKDIR`       | Create a working folder inside the container        |
| `COPY`          | Put your app’s compiled class file into that folder |
| `CMD`           | Run your app when the container starts              |

---

### ✅ 4. Build Your Docker Image

Run this in the folder where your `Dockerfile` and `.class` file exist:

```bash
docker build -t my-java-app .
```

* `-t my-java-app` gives your image a name
* `.` means use the current directory (where your Dockerfile is)

✅ What does -t mean in docker build?
* -t stands for tag.

It allows you to name your Docker image (and optionally version it) when building it.

---

### ✅ 5. Run the Container

Now run it:

```bash
docker run my-java-app
```

It should print:

```
🚀 Hello from inside Docker!
```

🎉 Boom! You’ve packaged and containerized your first Java app!

---

### ❓What Just Happened?

| Step      | What You Did                                |
| --------- | ------------------------------------------- |
| `FROM`    | Based the image on Java                     |
| `WORKDIR` | Set the working dir inside the image        |
| `COPY`    | Added your `.class` file to the image       |
| `CMD`     | Set the command to run inside the container |
| `build`   | Created your own Docker image               |
| `run`     | Started a container from your image         |

---
