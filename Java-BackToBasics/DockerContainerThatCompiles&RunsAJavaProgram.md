
## ✅ **Goal:**

Create a Docker container that compiles and runs a Java program — just like LeetCode does!

---

### **Step 1: Install Docker (if not already)**

* [Download Docker](https://www.docker.com/products/docker-desktop/) for Windows/Mac/Linux.
* Run `docker --version` in terminal to confirm it's installed.

---

### **Step 2: Create a Simple Java Program**

Let’s say you have this file named `Main.java`:

```java
public class Main {
    public static void main(String[] args) {
        System.out.println("Hello from inside Docker!");
    }
}
```

---

### **Step 3: Create a Dockerfile**

This Dockerfile tells Docker to set up an environment with JDK.

Create a file named `Dockerfile` (no extension):

```Dockerfile
# Use official OpenJDK image from DockerHub
FROM openjdk:17

# Set working directory inside container
WORKDIR /app

# Copy current folder files to /app in container
COPY . .

# Compile the Java program
RUN javac Main.java

# Command to run when the container starts
CMD ["java", "Main"]
```

This mimics what LeetCode does:

* It uses a **JDK image** (step 1).
* Copies your code into the container (step 2).
* Compiles it using `javac` (step 3).
* Runs it using `java` (step 4).

---

### **Step 4: Build the Docker Image**

Run this in the folder where your `Dockerfile` and `Main.java` are located:

```bash
docker build -t my-java-runner .
```

This builds your custom Java execution environment!

---

### **Step 5: Run the Container**

Now, execute your Java code inside the container:

```bash
docker run --rm my-java-runner
```

✅ You should see:

```
Hello from inside Docker!
```

You just created your own code-runner like LeetCode does — isolated and containerized.

---

### 🔥 **(Optional Bonus)**

If you want to make it dynamic (like LeetCode: accepts user code and runs), you can modify it to:

* Copy user-submitted code.
* Compile and run inside the container.
  This is exactly how online judges and coding platforms work at scale.

---

## FYI

Good question — let’s clear that up simply.

When you ran this command:

```bash
docker build -t my-java-runner .
```

Here’s what’s happening:

* `-t my-java-runner` → This gives a **name** (or **tag**) to the Docker image you’re building.
* `my-java-runner` is just a custom name I picked for this image.
* So now you have a Docker image called **`my-java-runner`**, which contains:

  * The **OpenJDK 17**
  * Your **compiled Java program**
  * The environment set up to run `java Main`

Later, when you run this:

```bash
docker run --rm my-java-runner
```

* Docker starts a **container** using the `my-java-runner` image.
* The container executes the **CMD** (`java Main`), which runs your Java code.

### Think of it like this:

| Command Part                       | Meaning                                            |
| ---------------------------------- | -------------------------------------------------- |
| `docker build -t my-java-runner .` | Build an image named **my-java-runner**            |
| `docker run --rm my-java-runner`   | Run a container using the **my-java-runner** image |

---

So, **`my-java-runner`** = your custom Java code runner image!

It’s like your personal "mini-LeetCode engine" in Docker form 😄

---

