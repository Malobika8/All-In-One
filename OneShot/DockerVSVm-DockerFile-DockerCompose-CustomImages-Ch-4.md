## 21) Docker vs Virtual Machines 

* **Virtual Machine (VM):**

  * Virtualizes **entire OS (kernel + application layer)**.
  * Heavyweight, large in size (GBs).
  * Slower to boot/start.
* **Docker:**

  * Virtualizes **only the application layer**.
  * Shares host OS kernel.
  * Lightweight, small in size (MBs).
  * Faster startup and less resource usage.
* **Key point:** Docker = lightweight alternative to VMs for running applications.

---

# 22) Introduction to Dockerfile 

* **Dockerfile = Blueprint** to create custom images.
* Contains a set of **instructions** to build an image.
* Common instructions:

  * `FROM <base-image>` → starting point
  * `COPY` → copy files from host to image
  * `RUN` → run shell commands during image build
  * `CMD` → default command when container runs
* Example (Node.js app):

  ```
  FROM openjdk:26-trixie

  WORKDIR /testapp

  COPY /target/SpringBootApp-1.0-SNAPSHOT.jar .

  CMD ["java", "-jar", "SpringBootApp-1.0-SNAPSHOT.jar"]
  ```
### Package your Spring Boot app

First, build your jar locally:

```bash
mvn clean package -DskipTests
```

This creates something like:

```
target/myapp-0.0.1-SNAPSHOT.jar
```

### Create a minimal Dockerfile

In the root of your project, create `Dockerfile`:

```dockerfile
# 1. Use an official JDK base image
FROM openjdk:17-jdk-slim

# 2. Set working directory inside container
WORKDIR /app

# 3. Copy jar from local machine to container
COPY target/myapp-0.0.1-SNAPSHOT.jar app.jar

# 4. Run the jar
CMD ["java", "-jar", "app.jar"]
```

### Build the image

Run this from your project root:

```bash
docker build -t my-springboot-app .
```

### Run the container

```bash
docker run -p 8080:8080 my-springboot-app
```

* Maps port 8080 of container → 8080 on your host.
* Now visit [http://localhost:8080](http://localhost:8080).

### Verify

Check logs:

```bash
docker logs <container_id>
```

Check running containers:

```bash
docker ps
```

✅ That’s the cleanest “hello-world” style Dockerization for Spring Boot.

We **can** build the JAR inside the container itself — that’s where a **multi-stage Docker build** comes in.

This way we don’t need Maven/Gradle installed locally; Docker takes care of both building and running our Spring Boot app.

# Example: Multi-stage Dockerfile

```dockerfile
# Stage 1 : Build
FROM maven:sapmachine AS build

WORKDIR /testapp

COPY pom.xml .

RUN mvn dependency:go-offline

COPY src ./src

RUN mvn clean package -DskipTests

# Stage 2 :  Run

FROM openjdk:17-jdk-slim

WORKDIR /testapp

COPY --from=build /testapp/target/*.jar springbootapp.jar

CMD ["java", "-jar", "springbootapp.jar"]
```

### How it works

- First stage (`maven:sapmachine`):

   * Has Maven & JDK
   * Builds your Spring Boot jar inside the container.

- Second stage (`openjdk:17-jdk-slim`):

   * Lighter base image with just JDK.
   * Copies the built jar from stage 1.
   * Runs it.

So your final image is small, clean, and doesn’t include Maven.

### Build & Run

```bash
docker build -t my-springboot-app .
docker run -p 8080:8080 my-springboot-app
```

✅ This is the **most common production-ready approach**: build inside Docker, then run on a minimal base image.

## Note:

### How Docker caching works

#### Case 1: With `mvn dependency:go-offline`

```dockerfile
COPY pom.xml .
RUN mvn dependency:go-offline   # <-- dependencies downloaded & cached here
COPY src ./src
RUN mvn clean package -DskipTests
```

* On **first build**:

  * Docker sees new `pom.xml`, runs `mvn dependency:go-offline`, downloads dependencies.
  * Then builds our jar.

* On **subsequent builds (only src changed)**:

  * `pom.xml` hasn’t changed → Docker reuses cached dependencies layer.
  * Only `src` step runs again → rebuilds jar quickly.

⚡ So dependencies don’t get downloaded again unless `pom.xml` changes.

#### Case 2: Without `mvn dependency:go-offline`

```dockerfile
COPY . .
RUN mvn clean package -DskipTests
```

* On **every build**:

  * Any change in source invalidates the cache for the `COPY . .` layer.
  * That means Maven dependencies are **always redownloaded**, even if unchanged.
  * Slower builds.

Docker caches the **dependency download step** (`mvn dependency:go-offline`).

* If `pom.xml` didn’t change → cache is reused → no re-download.
* If `pom.xml` changed (new dependency/version) → cache invalidated → Maven downloads again.

The `mvn clean package` step still runs every time (to recompile our code), but it **reuses cached dependencies**.

---

## 23) Building Custom Images 

* Build an image from Dockerfile:

  ```bash
  docker build -t <image-name>:<tag> .
  ```
* Example:

  ```bash
  docker build -t mynodeapp:1.0 .
  ```
* Verify image:

  ```bash
  docker images
  ```
* Run container from custom image:

  ```bash
  docker run -d -p 3000:3000 mynodeapp:1.0
  ```

---

# 24) Introduction to Docker Compose

* **Problem:** Running multiple containers manually with `docker run` is complex.
* **Solution:** Docker Compose → manages multi-container apps with a single YAML file.
* File name: `docker-compose.yml`
* Example:

  ```yaml
  version: '3'
  services:
    app:
      build: .
      ports:
        - "3000:3000"
    db:
      image: mongo:4.2
      ports:
        - "27017:27017"
  ```
* Commands:

  ```bash
  docker-compose up      # start all services
  docker-compose down    # stop all services
  ```
  
## Dockerfile for Spring Boot app

Assume you already have a Spring Boot jar built (`target/myapp.jar`):

```dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/myapp.jar app.jar
CMD ["java", "-jar", "app.jar"]
```

Build the image:

```bash
docker build -t springbootapp .
```

### `docker-compose.yml`

Create a file named `docker-compose.yml` in project root:

```yaml
services:
  app:
    image: springbootapp:1.0
    build: .
    ports:
      - 8080:8080
    depends_on:
      - db

  db:
    image: mysql:8.3.0
    restart: always
    environment:
      MYSQL_ROOT_PASSWORD: password
      MYSQL_DATABASE: security
    ports:
      - 3333:3306
```

### How it works

* **MySQL service (`db`)**

  * Runs official `mysql:8.0` image.
  * Creates a database `mydb`.
  * Root user password is `root`.
  * What does build: . mean?
    - build tells Docker Compose: build an image from a Dockerfile.
    - The . means current directory. So Compose will look in the same folder (where docker-compose.yml is) for a Dockerfile.
    - It’s basically the same as running: docker build -t springbootapp .

* **Spring Boot service (`app`)**

  * Built from your Dockerfile.
  * Exposes `8080`.
  * Connects to MySQL using environment variables.
  * Uses `db` as hostname (because Docker Compose creates a network, and service names resolve as hostnames).

* `depends_on` ensures MySQL starts before Spring Boot (but note: it doesn’t wait for DB to be *ready*, just started — we can handle readiness with retries if needed).

### Start everything

```bash
docker-compose up --build
```

* Access Spring Boot: [http://localhost:8080](http://localhost:8080)
* MySQL is available on port `3333`

✅ This is the cleanest, minimal setup. Later, we can add:

* **Volumes** to persist MySQL data
* **Custom networks**
* **Healthchecks**

## docker-compose up VS docker-compose up --build

### 🔹 `docker-compose up`

* Just **starts the services** defined in `docker-compose.yml`.
* If the image already exists locally, it will use it.
* If the image doesn’t exist, it will **build it once** (if a `build:` section is present).
* If the image exists but your source code changed → it **won’t rebuild automatically**.

### 🔹 `docker-compose up --build`

* Does everything that `docker-compose up` does, **plus** forces a **rebuild** of the images, even if they already exist.
* Useful when you’ve made changes to your app code, Dockerfile, or dependencies.

### Typical workflow

* First time (or after code changes):

  ```bash
  docker-compose up --build
  ```
* Next runs (no code changes, just want to start everything):

  ```bash
  docker-compose up
  ```

✅ **Shortcut**: We can also rebuild separately with:

```bash
docker-compose build
docker-compose up
```

---

## 25) Volumes (Intro)

* **Problem:** Data inside containers is lost when container stops/deletes.
* **Solution:** Volumes = external storage for containers.
* Example:

  ```bash
  docker run -d -v myvolume:/var/lib/mysql mysql:latest
  ```
* This keeps MySQL data safe even if the container is deleted.

---

# Quick Commands Recap 

* Dockerfile basics: `FROM`, `COPY`, `RUN`, `CMD`
* `docker build -t myapp:1.0 .` → build image
* `docker run -d -p 3000:3000 myapp:1.0` → run custom image
* Docker Compose:

  * `docker-compose up`
  * `docker-compose down`
* Volumes: `-v volume-name:/container/path`

---
