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

## 22) Introduction to Dockerfile 

* **Dockerfile = Blueprint** to create custom images.
* Contains a set of **instructions** to build an image.
* Common instructions:

  * `FROM <base-image>` → starting point
  * `COPY` → copy files from host to image
  * `RUN` → run shell commands during image build
  * `CMD` → default command when container runs
* Example (Node.js app):

  ```dockerfile
  FROM node:16
  WORKDIR /app
  COPY . .
  RUN npm install
  CMD ["node", "app.js"]
  ```

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

## 24) Introduction to Docker Compose

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
