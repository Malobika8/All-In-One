# Essential Docker Commands 

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
