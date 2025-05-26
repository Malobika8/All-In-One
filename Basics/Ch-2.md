## 🧭 Step-by-Step Docker Learning Plan

---

### ✅ Step 1: Core Concepts

Let’s lock in these basic terms:

| Term              | Meaning                                                                 |
| ----------------- | ----------------------------------------------------------------------- |
| **Image**         | A blueprint or snapshot of your application + environment.              |
| **Container**     | A running instance of an image. Lightweight, isolated, portable.        |
| **Dockerfile**    | A file that defines how to build an image (instructions).               |
| **Docker Engine** | The tool that builds and runs containers on your machine.               |
| **Docker Hub**    | A public place to find or push images (like GitHub but for containers). |

---

### ✅ Step 2: Install Docker

You might already have it — if not, install Docker Desktop:

* [https://www.docker.com/get-started](https://www.docker.com/get-started)
* After installation:

  ```bash
  docker --version
  docker info
  ```

---

### ✅ Step 3: Your First Container (Hands-on)

Let’s run a test container:

```bash
docker run hello-world
```

This:

* Pulls a test image from Docker Hub
* Creates a container from it
* Runs it (prints a message and exits)

---

### ✅ Step 4: Basic Docker CLI Commands

Practice these regularly:

| Command               | Purpose                            |
| --------------------- | ---------------------------------- |
| `docker pull <image>` | Download an image                  |
| `docker images`       | Show downloaded images             |
| `docker run <image>`  | Create & start a container         |
| `docker ps`           | Show running containers            |
| `docker ps -a`        | Show all containers (even stopped) |
| `docker stop <id>`    | Stop a running container           |
| `docker rm <id>`      | Remove a container                 |
| `docker rmi <id>`     | Remove an image                    |

---

## ✅ Step-by-Step: Try a Java Image (with Hints)

### 🪝 Step 1: Pull the official Java image

Use the following command to download the OpenJDK 11 image:

```bash
docker pull openjdk:11-jdk
```

* This fetches the **OpenJDK 11 image with JDK tools** (not just JRE).
* Docker will download it from **Docker Hub**.
* Only needs to be done once (unless you want a newer version later).

---

### 🪝 Step 2: Run a container with that image interactively

```bash
docker run -it openjdk:11-jdk bash
```

Let's break that down:

* `docker run` — Start a new container
* `-it` — Make it **interactive**, with a **terminal**
* `openjdk:11-jdk` — Use the image you just pulled
* `bash` — Run `bash` shell inside the container

---

### 🪝 Step 3: You are now inside the container!

You’ll now see a terminal prompt like:

```
root@abc123:/#
```

You’re inside the running container. Try this:

```bash
java -version
```

It should print Java 11 info — proving that the JDK is inside the container, **even if your local system doesn’t have Java installed.**

---

### 🪝 Step 4: Exit the container

To return to your normal terminal:

```bash
exit
```

This will stop the container unless you run it in the background (we’ll explore that later).

---

### 🔜 Next: Build Your Own Docker Image

Once you're comfortable with basic commands, we’ll write a Dockerfile for a simple Java program and build a custom image.

---

