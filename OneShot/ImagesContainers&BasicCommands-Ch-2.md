## 6) Pulling Images 

* To bring any Docker image from Docker Hub into local environment, use:

  ```bash
  docker pull <image-name>
  ```
* Example:

  ```bash
  docker pull hello-world
  ```
* If no tag is specified, Docker automatically uses the **`latest` tag**.
* To check available images locally:

  ```bash
  docker images
  ```
* Each image has:

  * A **name**
  * A **tag** (version/variant)
  * An **image ID** (unique)
  * A **size** (generally lightweight)

---

## 7) Creating Containers 

* Once an image is available locally, we can create a container from it:

  ```bash
  docker run <image-name>
  ```
* Example:

  ```bash
  docker run hello-world
  ```
* What happens:

  * A new container is created from the image.
  * The container executes and prints its output.
* In Docker Desktop, containers appear under the **Containers tab**.
* Containers have:

  * A **random name** (assigned by Docker if not specified)
  * A **unique ID**
  * Status (running/stopped)

---

## 8) Pull vs Run

* **`docker pull`** → Only downloads the image.
* **`docker run`** → Downloads the image (if not present) **and** creates a container from it.
* Example:

  ```bash
  docker pull ubuntu
  docker run ubuntu
  ```

---

## 9) Running in Interactive Mode

* To interact with a container’s terminal, use `-it` flag:

  ```bash
  docker run -it ubuntu
  ```
* Here:

  * `-i` = interactive (keep STDIN open)
  * `-t` = allocate a pseudo-TTY (terminal)
* This opens the **Ubuntu container’s terminal**.
* From here, we can run commands inside the container (e.g., `ls`, `mkdir`, `printenv`).
* To exit the interactive session:

  ```bash
  exit
  ```
* On exit, container automatically stops.

---

## 10) Checking Containers 

* To see running containers:

  ```bash
  docker ps
  ```
* To see **all containers** (including stopped):

  ```bash
  docker ps -a
  ```

---

## 11) Starting & Stopping Containers 

* **Start a stopped container:**

  ```bash
  docker start <container-id-or-name>
  ```
* **Stop a running container:**

  ```bash
  docker stop <container-id-or-name>
  ```
* Green dot in Docker Desktop indicates a container is running.

---

## 12) Removing Images & Containers 

* **Remove a container:**

  ```bash
  docker rm <container-id-or-name>
  ```
* **Remove an image:**

  ```bash
  docker rmi <image-id-or-name>
  ```
* ⚠️ Note: An image cannot be removed if it’s being used by an existing container.

  * First, remove the container → then remove the image.

---

# Quick Commands Recap (this part)

* `docker pull <image>` → Download image
* `docker run <image>` → Create & run container
* `docker run -it <image>` → Run in interactive mode
* `docker ps` → Show running containers
* `docker ps -a` → Show all containers
* `docker start <id>` / `docker stop <id>` → Start/Stop container
* `docker rm <id>` / `docker rmi <id>` → Remove container/image

---
