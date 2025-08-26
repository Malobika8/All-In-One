### ✅ The Dockerfile has **no extension** — it’s just named:

```
Dockerfile
```

> ✅ **Correct:** `Dockerfile`
> ❌ **Incorrect:** `Dockerfile.txt`, `Dockerfile.docker`, `Dockerfile.java`, etc.

---

### 📁 Where do you put it?

Put it in the **root directory** of your project — the same folder as your app files like `HelloWorld.class`, etc.

---

### 📦 Example folder structure:

```
my-java-app/
├── Dockerfile         ✅
├── HelloWorld.java
├── HelloWorld.class
```

---

# Basic Docker CLI Commands

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

# Summary Cheat Sheet

| Task                    | Command                         | Notes                            |
| ----------------------- | ------------------------------- | -------------------------------- |
| Build Docker image      | `docker build -t my-java-app .` | Build image from Dockerfile      |
| Run container           | `docker run my-java-app`        | Runs container, exits after run  |
| Rebuild images          | `docker compose build`          | Rebuild images manually |
| Compose up              | `docker-compose up`             | Runs all services, attached logs |
| Compose up detached     | `docker-compose up -d`          | Runs all in background           |
| View logs for a service | `docker compose logs [service]` | View logs for a service          |
| Follow logs             | `docker-compose logs -f`        | Follow container logs            |
| Stop containers         | `docker-compose down`           | Stop and remove containers       |
| List running containers | `docker ps`                     | See running containers           |
| List running containers | `docker compose ps`             | Show running containers           |
| Stop/start services     | `docker compose stop/start`     | Stop/start services without removing them |
| Run bash inside the container | `docker compose exec app bash` | Run bash inside the container           |
| Run one-off commands in service container     | `docker compose run app [command]`     | Run one-off commands in service container |

<img width="859" height="491" alt="Screenshot 2025-08-26 at 3 29 19 PM" src="https://github.com/user-attachments/assets/e98beb82-245f-41e4-ae54-889583b195d5" />
