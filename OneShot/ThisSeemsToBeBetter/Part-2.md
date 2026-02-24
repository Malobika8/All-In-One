Perfect.
Now I will convert **Part 2** into full detailed handwritten-style notes — strictly chronological, no compression, no skipping, no optimization, preserving every transition exactly in the order explained.

I will continue from the beginning of Part 2 and write as if these are handwritten notes while watching.

---

# 📘 PART 2 – Detailed Chronological Notes

---

## 🔹 Docker Images and Tags

Every Docker image has some associated **tags**.

These tags — what exactly they are — we will slowly understand in this lecture.

Along with every image, some **basic documentation** is provided:

* Example outputs
* Different environment variables required by the container
* Usage examples
* Additional configuration options

So every image has different things associated with it.

---

## 🔹 Pulling an Image from Docker Hub

To bring any Docker image from Docker Hub into our local environment, we need Docker commands.

The most basic command is:

```
docker pull <image-name>
```

If the image does not exist locally, Docker will pull it from Docker Hub.

Example:

```
docker pull hello-world
```

When we run this command:

* It shows **default tag: latest**
* That means it is pulling the latest version
* The image downloads successfully

---

## 🔹 Checking Available Images

To check what images exist locally:

```
docker images
```

Currently, we see only one image:

* `hello-world`

---

## 🔹 Understanding Tags

Tags are basically the **versions of an image**.

Just like Node.js has different versions,
Docker images also can have:

* Different versions
* Different variants

---

## 🔹 Viewing Images in Docker Desktop

If we go to Docker Desktop → Images section:

* We see the hello-world image
* It has a unique Image ID
* Each image has a unique ID associated with it

If we check the size:

* It is only in KBs
* Very small

That is why Docker is considered **lightweight**.

---

# 🔹 Creating a Container from an Image

We already learned:

Image → used to build containers

To create a container:

```
docker run <image-name>
```

Example:

```
docker run hello-world
```

What happened:

* A container was created
* It executed
* It printed output
* It exited

---

## 🔹 Viewing Containers in Docker Desktop

If we go to Containers:

* A new container exists
* Docker automatically gives it a random name
* It also has a unique container ID
* We can see which image it was created from

In Images section:

* A green dot appears
* That means this image has been used to create a container

---

# 🔹 What Did Hello-World Actually Do?

The output explained the internal process:

To generate that message:

1. Docker client contacted Docker daemon
2. Docker daemon pulled hello-world image from Docker Hub
3. Docker daemon created a container from that image
4. The container executed an executable
5. Output was printed

So flow:

Image → Container built → Container ran → Output printed

---

# 🔹 Running Another Image – Ubuntu

We are suggested to run Ubuntu image.

We can also search Ubuntu on Docker Hub.

If we run:

```
docker pull ubuntu
```

It only pulls the image.

If we run:

```
docker run ubuntu
```

It:

* Pulls image (if not present)
* Creates container
* Runs container

---

# 🔹 Running Container in Interactive Mode (-it)

Now before running Ubuntu, we use a special option:

```
-it
```

Interactive mode allows us to access container terminal.

Command:

```
docker run -it ubuntu
```

Now:

* We move from host terminal (Mac terminal)
* Into container terminal

We can see:

* Root directory
* Container ID shown

If we verify in Docker Desktop:

* That container is running
* Previous container is stopped

---

# 🔹 Inside Ubuntu Container

Now inside container:

We can run commands:

```
ls
```

Shows files and folders inside container.

We can:

```
mkdir test
```

Create new directory.

We can check:

* Environment variables
* File system

Important:

This environment is separate from host machine.

---

## 🔹 Exiting Container

If we type:

```
exit
```

Container automatically stops.

Now it goes into stopped state.

---

# 🔹 Viewing Containers

To see all containers:

```
docker ps -a
```

Shows:

* All containers
* Running + stopped
* Their IDs
* Names
* Status

To see only running containers:

```
docker ps
```

Currently none running.

---

# 🔹 docker run vs docker start

Important difference:

### docker run

* Always creates a new container from image

### docker start

* Starts an existing stopped container

Example:

```
docker start <container-id>
```

Now if we do:

```
docker ps
```

Container is running.

Green dot visible in Docker Desktop.

To stop:

```
docker stop <container-name>
```

---

# 🔹 Removing Images and Containers

Important commands:

### Remove image

```
docker rmi <image-name>
```

### Remove container

```
docker rm <container-name>
```

If we try removing image that has container:

We get error:

"Image is being used by a stopped container"

So first remove container:

```
docker rm <container-id>
```

Then remove image:

```
docker rmi hello-world
```

Now image deleted.

---

# 🔹 Understanding Versions in Docker Images

Now pulling MySQL image.

If we run:

```
docker pull mysql
```

It pulls latest version.

If we want specific version:

```
docker pull mysql:8.0
```

Now we have two images:

* mysql:latest
* mysql:8.0

---

# 🔹 Layers in Docker Images

While pulling image:

We saw multiple lines downloading.

These are layers.

Each image consists of multiple layers.

When pulling another version:

Some layers say:

"Already exists"

Because:

* Common layers are reused
* Only different layers are downloaded

We will understand layers more deeply when building our own images.

For now:

Every Docker image = Collection of layers

There is always:

* Base layer (immutable)
* Container layer (modifiable)

---

# 🔹 Detached Mode (-d)

When running containers:

By default → attached mode

To run in background:

```
docker run -d mysql
```

This runs container in background.

---

# 🔹 Environment Variables (-e)

Some containers require environment variables.

Example:

MySQL requires root password.

We use:

```
-e MYSQL_ROOT_PASSWORD=secret
```

Full command:

```
docker run -d -e MYSQL_ROOT_PASSWORD=secret mysql
```

Now container running.

---

# 🔹 Custom Container Name (--name)

To give custom name:

```
--name mysql-older
```

So:

```
docker run -d --name mysql-older mysql:8.0
```

Now:

Two containers running:

* One latest
* One 8.0

---

# 🔹 Port Binding

Each container has its own ports.

Example:

MySQL container port:

```
3306
```

But:

Host machine ports and container ports are separate.

If we want host port to connect to container port:

We use:

```
-p hostPort:containerPort
```

Example:

```
-p 8080:3306
```

Meaning:

Host 8080 → Container 3306

This mapping is called **Port Binding**.

Important:

Same host port cannot bind to two containers.

If 8080 already used:

Second container must use different host port like 5000.

---

# 🔹 Troubleshooting Commands

## docker logs

To check container logs:

```
docker logs <container-name>
```

Shows initialization logs.

Example:

MySQL logs show:

* Initializing database
* Starting server

---

## docker exec

To run commands inside running container:

```
docker exec -it <container-name> /bin/bash
```

Now inside container shell.

We can:

* Check files
* Check environment variables
* Check dependencies

If we exit:

Container still running.

---

# 🔹 Docker vs Virtual Machine

Host Machine:

* OS Kernel
* Application Layer

Docker:

* Virtualizes only Application Layer
* Uses host kernel
* Lightweight
* Fast
* Small size (MBs)

Virtual Machine:

* Virtualizes entire OS
* Includes own kernel
* Heavy
* Large size (GBs)

Advantage of Docker:

* Lightweight
* Faster

Disadvantage:

* Initially built for Linux
* Depends on host kernel
* Slight compatibility limitations

---

# 🔹 Starting Node.js Application Setup

We have a test Node.js app.

Folder: test-app

Inside:

* server.js
* public folder

Server.js:

* Express backend
* MongoClient used
* Two routes:

  * GET /getUsers
  * POST /addUser

Server runs on:

```
Port 5050
```

Public folder contains UI.

We are trying to connect to database:

```
apna-college-db
```

But no MongoDB installed locally.

So:

We will use Docker to run MongoDB.

---

# 🔹 Images We Will Use

1. mongo → MongoDB database
2. mongo-express → Admin UI

We will pull these images and build containers.

---

# 🔹 Docker Network Concept

Until now:

Containers need ports to interact.

But:

We want Mongo and Mongo Express containers to interact directly.

Solution:

Create Docker Network.

Docker network allows:

Containers inside same network

To communicate directly

Without port binding

---

## Checking Networks

```
docker network ls
```

Shows:

* Network IDs
* Names
* Scope

---

## Creating Network

```
docker network create mongo-network
```

Now new network created.

---

# 🔹 Setting Up Mongo Container

Go to Docker Hub → Official Mongo Image

Instead of pulling image separately:

We directly run container.

If image not present:

Docker pulls automatically.

Mongo default port:

```
27017
```

We bind:

```
-p 27017:27017
```

We want:

* Detached mode
* Custom name
* Custom network
* Environment variables

Required env variables:

```
MONGO_INITDB_ROOT_USERNAME=admin
MONGO_INITDB_ROOT_PASSWORD=admin
```

Important:

Remember credentials.

Command structure:

```
docker run -d \
-p 27017:27017 \
--name mongo \
--network mongo-network \
-e MONGO_INITDB_ROOT_USERNAME=admin \
-e MONGO_INITDB_ROOT_PASSWORD=admin \
mongo
```

When run:

* Image layers download
* Container starts

Check:

```
docker ps
```

Mongo container running.

---

Next step:

Set up mongo-express container.

(Continuation would follow exactly in next part.)

---

This completes the structured, full chronological conversion of Part 2 up to this point — preserving all explanations, order, transitions, and details exactly as discussed.
