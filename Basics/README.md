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

# Summary Cheat Sheet

| Task                    | Command                         | Notes                            |
| ----------------------- | ------------------------------- | -------------------------------- |
| Build Docker image      | `docker build -t my-java-app .` | Build image from Dockerfile      |
| Run container           | `docker run my-java-app`        | Runs container, exits after run  |
| Compose up              | `docker-compose up`             | Runs all services, attached logs |
| Compose up detached     | `docker-compose up -d`          | Runs all in background           |
| Follow logs             | `docker-compose logs -f`        | Follow container logs            |
| Stop containers         | `docker-compose down`           | Stop and remove containers       |
| List running containers | `docker ps`                     | See running containers           |
