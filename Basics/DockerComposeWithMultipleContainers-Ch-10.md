
## 🐳 Docker Compose — (Multiple Containers + Detached Mode)

---

### ✅ What Is Docker Compose?

Docker Compose is a tool that lets you **run multiple Docker containers together** using a single YAML file.

For example, you can:

* Run your **Java app** container
* Run a **MySQL** container
* Start both together with **one command**

---

### 📁 Where Does `docker-compose.yml` Go?

Put the `docker-compose.yml` file in the **root directory** of your project — where your `Dockerfile`, `pom.xml`, and `src/` are.

---

### 🧱 Example Scenario: Java App + MySQL

You have:

* A Java app that prints something or connects to a DB.
* A MySQL container already pulled (`mysql:8` image).

---

### 🧾 Sample `docker-compose.yml`

```yaml
version: "3.9"

services:
  app:
    build: .
    container_name: docker-java-app
    depends_on:
      - mysql
    command: ["java", "-jar", "app.jar"]

  mysql:
    image: mysql:8
    container_name: mysql
    environment:
      MYSQL_ROOT_PASSWORD: root
      MYSQL_DATABASE: testdb
    ports:
      - "3306:3306"
```

📌 What it does:

* `build: .` — Builds the app image using the `Dockerfile` in current directory.
* `depends_on` — Makes sure MySQL container starts before the app.
* `environment` — Sets MySQL username, password, and database.
* `ports` — Exposes MySQL's port to your local machine.

---

### ▶️ How to Run It

#### 🔹 Run All Containers Together

```bash
docker compose up --build
```

* Builds and starts both containers.
* Shows logs from both containers in real time.

#### 🔹 Run in Background (Detached Mode)

```bash
docker compose up -d
```

* Runs containers **in the background**
* Frees up your terminal
* You’ll **not see logs** directly

---

### 🛑 How to Stop Everything

```bash
docker compose down
```

* Stops all containers started with `docker-compose.yml`
* Removes the containers and network (if created)

---

### 📜 View Logs (After Running in Detached Mode)

```bash
docker compose logs
```

To see logs of only the app:

```bash
docker compose logs app
```

---

### 🔁 Restart Just the App

```bash
docker compose up -d --build app
```

---

### 📌 Key Points to Remember

* `docker-compose.yml` is used to define multiple containers (services).
* Each container (Java app, MySQL, etc.) is defined as a **service**.
* Use `docker compose up -d` to run in background.
* Use `docker compose down` to stop everything.
* Use `docker compose logs` to view logs.
* You don’t need to run `docker build` and `docker run` manually when using Compose.

---
