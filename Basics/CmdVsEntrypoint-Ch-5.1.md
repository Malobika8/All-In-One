
# Docker CMD vs ENTRYPOINT and Overriding Commands

### 1. **CMD**

* Specifies the **default command** and arguments to run when the container starts.
* You can **override CMD completely** by passing a different command when running the container.

**Example Dockerfile:**

```dockerfile
CMD ["java", "-jar", "app.jar"]
```

**Usage:**

* Default run:

  ```bash
  docker run my-image
  ```

  Runs:

  ```bash
  java -jar app.jar
  ```

* Override CMD with a new command:

  ```bash
  docker run my-image java -version
  ```

  Runs:

  ```bash
  java -version
  ```

---

### 2. **ENTRYPOINT**

* Specifies the **fixed command** that always runs.
* Commands passed via `docker run` become **arguments** to the ENTRYPOINT.

**Example Dockerfile:**

```dockerfile
ENTRYPOINT ["java", "-jar", "app.jar"]
```

**Usage:**

* Default run:

  ```bash
  docker run my-image
  ```

  Runs:

  ```bash
  java -jar app.jar
  ```

* Passing extra args:

  ```bash
  docker run my-image --someArg
  ```

  Runs:

  ```bash
  java -jar app.jar --someArg
  ```

* If you try to override command:

  ```bash
  docker run my-image java -version
  ```

  It runs:

  ```bash
  java -jar app.jar java -version
  ```

  (which is usually not what you want)

---

### 3. **ENTRYPOINT + CMD together (best practice)**

You can combine both to set fixed command with default arguments, but still allow overriding arguments:

```dockerfile
ENTRYPOINT ["java", "-jar", "app.jar"]
CMD []
```

* Default run:

  ```bash
  docker run my-image
  ```

  Runs:

  ```bash
  java -jar app.jar
  ```

* Run with extra args:

  ```bash
  docker run my-image --someArg
  ```

  Runs:

  ```bash
  java -jar app.jar --someArg
  ```

---

### 4. **How to override ENTRYPOINT?**

* Use the `--entrypoint` flag in `docker run` to override ENTRYPOINT:

```bash
docker run --entrypoint java my-image -version
```

This runs:

```bash
java -version
```

---

### Summary Table

| Dockerfile Setup                              | `docker run` command                             | Runs                                            |
| --------------------------------------------- | ------------------------------------------------ | ----------------------------------------------- |
| `CMD ["java", "-jar", "app.jar"]` only        | `docker run my-image`                            | `java -jar app.jar`                             |
|                                               | `docker run my-image java -version`              | `java -version` (CMD replaced)                  |
| `ENTRYPOINT ["java", "-jar", "app.jar"]` only | `docker run my-image`                            | `java -jar app.jar`                             |
|                                               | `docker run my-image --arg`                      | `java -jar app.jar --arg`                       |
|                                               | `docker run my-image java -version`              | `java -jar app.jar java -version` (args passed) |
| `ENTRYPOINT + CMD`                            | `docker run my-image`                            | `java -jar app.jar`                             |
|                                               | `docker run my-image --arg`                      | `java -jar app.jar --arg`                       |
| Override ENTRYPOINT                           | `docker run --entrypoint java my-image -version` | `java -version`                                 |

---
