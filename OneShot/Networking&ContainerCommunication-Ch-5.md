## 26) Docker Networking Basics

* Each container gets its **own isolated network environment**.
* By default, Docker provides these network types:

  * **bridge** (default) → containers communicate via virtual bridge
  * **host** → container shares host machine’s network stack
  * **none** → no network access
* Default mode = **bridge**.
* Each container in bridge network gets its own **IP address**.

---

## 27) Checking Networks 

* List all networks:

  ```bash
  docker network ls
  ```
* Inspect details of a network:

  ```bash
  docker network inspect <network-name>
  ```

---

## 28) Creating Custom Networks

* Create a custom bridge network:

  ```bash
  docker network create mynetwork
  ```
* Run containers inside this network:

  ```bash
  docker run -d --name app1 --network mynetwork nginx
  docker run -d --name app2 --network mynetwork alpine ping app1
  ```
* Containers in the same custom network can communicate by **container name**.
* Advantage: avoids manual IP usage.

---

## 29) Connecting Containers to Multiple Networks 

* By default, a container is attached to one network.
* To connect an existing container to another network:

  ```bash
  docker network connect <network-name> <container-name>
  ```
* To disconnect:

  ```bash
  docker network disconnect <network-name> <container-name>
  ```

---

## 30) Networking with Docker Compose

* Docker Compose automatically creates a **default network** for all services.
* All services can talk to each other by **service name**.
* Example (`docker-compose.yml`):

  ```yaml
  version: '3'
  services:
    web:
      image: nginx
    db:
      image: mysql
      environment:
        - MYSQL_ROOT_PASSWORD=secret
  ```
* Here, `web` can reach database using hostname `db`.

---

## 31) Practical Example

* Running **Node.js + MongoDB** with custom network:

  ```bash
  docker network create app-network

  docker run -d --name mongo --network app-network mongo:4.2

  docker run -d --name nodeapp --network app-network -p 3000:3000 mynodeapp:1.0
  ```
* In Node.js code, DB hostname = `mongo` (container name).

---

# Quick Commands Recap

* `docker network ls` → list networks
* `docker network create mynetwork` → create network
* `docker run --network mynetwork <image>` → attach container to network
* `docker network connect/disconnect` → manage container networks
* Compose: services auto-connect to a shared network

