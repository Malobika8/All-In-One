## 32) Volumes in Detail 

* **Problem:** Data stored inside a container is lost if the container is stopped/removed.
* **Solution:** Use Docker Volumes → external persistent storage.

### Types of Volumes

1. **Anonymous Volume** → created automatically by Docker

   ```bash
   docker run -d -v /var/lib/mysql mysql:latest
   ```

   * Not easy to reuse across containers.

2. **Named Volume** → explicitly created, reusable

   ```bash
   docker volume create mydbdata
   docker run -d -v mydbdata:/var/lib/mysql mysql:latest
   ```

3. **Bind Mount** → map host directory into container

   ```bash
   docker run -d -v /host/path:/container/path myimage
   ```

   * Useful for development (code changes reflect immediately).

### Volume Commands

* List volumes:

  ```bash
  docker volume ls
  ```
* Inspect a volume:

  ```bash
  docker volume inspect mydbdata
  ```
* Remove a volume:

  ```bash
  docker volume rm mydbdata
  ```

---

## 33) Troubleshooting & Debugging 

* **Check logs of container:**

  ```bash
  docker logs <container-id-or-name>
  ```
* **Access container shell:**

  ```bash
  docker exec -it <container-id-or-name> bash
  ```

  or

  ```bash
  docker exec -it <container-id-or-name> sh
  ```
* **Inspect container details:**

  ```bash
  docker inspect <container-id-or-name>
  ```
* **Check resource usage (CPU, memory, etc.):**

  ```bash
  docker stats
  ```

---

## 34) Optimization Best Practices

* Use **official images** from Docker Hub where possible.
* Always set specific **tags/versions** instead of using `latest`.
* Keep Dockerfile **small & clean**:

  * Minimize layers
  * Remove unnecessary files
  * Use `.dockerignore` to exclude irrelevant files
* Use **multi-stage builds** for production-ready images.
* Regularly clean up unused containers/images/volumes:

  ```bash
  docker system prune
  ```

---

# 35) Final Recap: Essential Docker Commands 

### Image Management

* `docker pull <image>` → download image
* `docker images` → list images
* `docker rmi <image-id>` → remove image

### Container Management

* `docker run <image>` → create & run container
* `docker run -d <image>` → run in detached mode
* `docker run -it <image>` → run in interactive mode
* `docker ps` → running containers
* `docker ps -a` → all containers
* `docker start <id>` / `docker stop <id>` → start/stop container
* `docker rm <id>` → remove container
* `docker logs <id>` → view logs
* `docker exec -it <id> bash` → open shell inside container

### Networking

* `docker network ls` → list networks
* `docker network create <name>` → create network
* `docker run --network <name> <image>` → attach to network

### Volumes

* `docker volume ls` → list volumes
* `docker volume create <name>` → create volume
* `docker run -v <volume-name>:<path> <image>` → mount volume

### Compose

* `docker-compose up` → start services
* `docker-compose down` → stop services

---

## 36) Closing Notes

* Docker simplifies **development → deployment workflow**.
* Core ideas:

  * **Image vs Container**
  * **Networking & Volumes**
  * **Dockerfile & Compose**
* Once comfortable, you can explore **Kubernetes** for container orchestration.

---

