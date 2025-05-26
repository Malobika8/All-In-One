
## ✅ Goal

We will write a `Dockerfile` that:

1. Uses a Java image
2. Copies the Java source file (`.java`)
3. Compiles it inside the container
4. Runs it

---

## 🛠️ Step-by-Step: Dockerfile That Compiles & Runs Java

Assume you have this Java file in the current folder:

```java
// HelloWorld.java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("✅ Hello from inside Docker!");
    }
}
```

Now create a `Dockerfile`:

```dockerfile
# Use a Java image with JDK
FROM openjdk:21

# Set working directory
WORKDIR /app

# Copy Java source file into the container
COPY HelloWorld.java .

# Compile the Java file
RUN javac HelloWorld.java

# Run the compiled Java class
CMD ["java", "HelloWorld"]
```

---

## 🧱 Folder Structure

```
JavaFiles/
├── Dockerfile
└── HelloWorld.java
```

---

## 🚀 Build and Run

### Build the image:

```bash
docker build -t java-compile-run .
```

### Run the container:

```bash
docker run java-compile-run
```

✅ Output:

```
✅ Hello from inside Docker!
```

---

### 🔄 What’s the benefit?

* You don’t need Java installed on your host machine.
* The container handles both compiling and running.

---
