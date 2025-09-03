## 1) Session Overview

  * What Docker is and **why we use it**
  * **Images vs Containers**
  * **Essential Docker commands**
  * Docker vs **Virtual Machine**
  * **Port mapping** and **Environment variables**
  * Later: Dockerfile, Compose, Networking, Volumes, etc.

---

## 2) What is a Container?

* **Container = Single bundle / single unit** that includes the **application + all its dependencies**.
* This **single unit** is what gets shared with teammates and deployed to servers.
* Makes **environment replication** easy: take the bundle from Machine‑A to Machine‑B without manually installing/configuring dependencies.
* **OS‑agnostic**: containers run regardless of host OS differences.

---

## 3) Image vs Container

* **Image** is like an **executable file**; from **one image, multiple containers** can be created.
* Teams usually **share the image**, not the container; each dev builds their own container from the shared image.
* Resource usage analogy: Like **class vs objects** in OOP —

  * Class itself doesn’t use memory.
  * Objects consume resources.
  * Similarly, **images don’t consume system resources**, **containers do**.

---

## 4) Local Setup: Docker Desktop

* Download **Docker Desktop** from [docker.com](https://docker.com) (choose build for your OS).
* During install, accept **admin privileges/permissions**.
* After installation, **Close & Restart**; on restart, Docker Desktop launches.
* If the popup doesn’t appear, open via **Docker Desktop icon**.

---

## 5) First Run: Hello‑World Container

* Command:

  ```bash
  docker run hello-world
  ```
* What happens:

  * Docker daemon **pulls the `hello-world` image from Docker Hub** (if not available locally).
  * Creates a **new container** from that image.
  * Container **runs the executable inside the image**, which **prints a message**.

---

# Quick Commands Recap (from this part)

* `docker run hello-world`

