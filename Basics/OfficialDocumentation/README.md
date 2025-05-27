Here are **concise cheat sheets** for both **Dockerfile instructions** and **Docker Compose fields** to keep handy while you work.

---

## 🐳 Dockerfile Cheat Sheet

| Instruction   | Description                                                                                |
| ------------- | ------------------------------------------------------------------------------------------ |
| `FROM`        | Base image to build upon                                                                   |
| `WORKDIR`     | Set the working directory inside the container                                             |
| `COPY`        | Copy files/folders from host to container                                                  |
| `ADD`         | Like COPY but supports remote URLs and auto-unzipping archives                             |
| `RUN`         | Run shell commands during image build                                                      |
| `CMD`         | Default command to run when container starts (can be overridden)                           |
| `ENTRYPOINT`  | Command that **always runs** (can pass args using CMD or `docker run`)                     |
| `ENV`         | Set environment variables                                                                  |
| `EXPOSE`      | Document the port container listens on (not actually publish it)                           |
| `VOLUME`      | Create mount point for external volumes                                                    |
| `ARG`         | Define build-time variables                                                                |
| `LABEL`       | Add metadata to the image                                                                  |
| `USER`        | Set the user to run the container                                                          |
| `HEALTHCHECK` | Define container health check commands                                                     |
| `ONBUILD`     | Add trigger instructions to be executed when the image is used as a base for another build |
| `SHELL`       | Define default shell used by `RUN` commands                                                |

---

## 🧱 Docker Compose Cheat Sheet (`docker-compose.yml`)

### 🔹 Top-Level Fields

| Field      | Description                                 |
| ---------- | ------------------------------------------- |
| `version`  | Compose file format version (e.g., `"3.9"`) |
| `services` | Defines your app containers                 |
| `volumes`  | Define named or external volumes            |
| `networks` | Define custom networks                      |
| `configs`  | External configs like `.conf` files         |
| `secrets`  | Store sensitive values securely             |

---

### 🔹 Inside `services:<service_name>`

| Field            | Description                                         |
| ---------------- | --------------------------------------------------- |
| `build`          | Path or config to build the image                   |
| `image`          | Image name (from Docker Hub or custom)              |
| `container_name` | Set custom container name                           |
| `ports`          | Map host\:container ports                           |
| `volumes`        | Mount host paths or named volumes                   |
| `environment`    | Set environment variables                           |
| `depends_on`     | Set container startup order                         |
| `command`        | Override default CMD                                |
| `entrypoint`     | Override ENTRYPOINT                                 |
| `restart`        | Restart policy (`no`, `always`, `on-failure`, etc.) |
| `networks`       | Attach service to custom network                    |
| `healthcheck`    | Set health check logic                              |
| `working_dir`    | Set working directory inside container              |
| `stdin_open`     | Keep stdin open (useful for interactive containers) |
| `tty`            | Allocate TTY (like `-t` in `docker run`)            |

---

## ✅ Quick Examples

### Dockerfile

```Dockerfile
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/app.jar app.jar
CMD ["java", "-jar", "app.jar"]
```

### docker-compose.yml

```yaml
version: "3.9"
services:
  app:
    build: .
    ports:
      - "8080:8080"
    volumes:
      - .:/app
    depends_on:
      - mysql

  mysql:
    image: mysql:8
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: testdb
    ports:
      - "3306:3306"
```

---
