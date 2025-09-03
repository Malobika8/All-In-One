## 13) Versions & Tags in Images

* Each Docker image has **tags** → represent versions/variants.
* If no tag is specified → `latest` is used.
* Example:

  ```bash
  docker pull mysql        # pulls latest version
  docker pull mysql:8.0    # pulls version 8.0
  ```
* Images are downloaded as multiple **layers** (seen line by line during pull).
* Some layers are **common** across versions → reused instead of redownloaded.

---

## 14) Using Multiple Versions 

* We can run containers from different versions of the same image.
* Example:

  ```bash
  docker run -d mysql:latest
  docker run -d mysql:8.0
  ```
* Both containers will run different versions of MySQL.
* Very useful if multiple apps need **different dependency versions** on the same host.

---

## 15) Detached Mode 

* By default, containers run in **attached mode** (logs visible in terminal).
* To run in **background (detached mode):**

  ```bash
  docker run -d <image>
  ```

---

## 16) Environment Variables

* Some containers require environment variables at startup.
* Example: MySQL requires a **root password**.
* Use `-e` flag:

  ```bash
  docker run -d -e MYSQL_ROOT_PASSWORD=secret mysql:latest
  ```
* Environment variables can be checked inside the container with:

  ```bash
  printenv
  ```

---

## 17) Naming Containers

* Docker assigns random names by default.
* To set a **custom name:**

  ```bash
  docker run -d --name mysql-older mysql:8.0
  docker run -d --name mysql-latest mysql:latest
  ```
* Helps manage multiple containers easily.

---

## 18) Image Layers 

* Any Docker image is made up of **multiple layers**.
* **Base layer** → smallest, immutable (cannot be changed).
* **Container layer** → writable; changes are applied here.
* Example:

  * `mysql:latest` and `mysql:8.0` share some common layers.
  * When pulling the second image, Docker reuses already existing layers.
* Layers make Docker **lightweight and efficient**.

---

## 19) Port Binding 

* Each container has its own ports (isolated from host machine).
* To expose a container’s port to host:

  ```bash
  docker run -d -p <host-port>:<container-port> <image>
  ```
* Example:

  ```bash
  docker run -d -p 8080:3306 --name mysql1 -e MYSQL_ROOT_PASSWORD=secret mysql:latest
  docker run -d -p 5000:3306 --name mysql2 -e MYSQL_ROOT_PASSWORD=secret mysql:8.0
  ```
* ⚠️ Note: A host port can be bound only once. Each container must bind to a **different host port**.
* This allows multiple containers (with same internal port) to run side by side.

---

## 20) Troubleshooting Commands 

* **Check logs of a container:**

  ```bash
  docker logs <container-id-or-name>
  ```
* **Execute into a running container:**

  ```bash
  docker exec -it <container-id-or-name> bash
  ```

  * If `bash` isn’t available → use `sh`.
* Inside, we can check files, environment variables, dependencies.
* Exiting the shell does **not stop** the container.

---

# Quick Commands Recap

* `docker pull mysql:8.0` → Pull specific version
* `docker run -d <image>` → Run in detached mode
* `docker run -d -e VAR=value <image>` → Run with env variable
* `docker run -d --name myapp <image>` → Run with custom name
* `docker run -d -p 8080:3306 <image>` → Port binding
* `docker logs <id>` → Check container logs
* `docker exec -it <id> bash` → Access container shell

