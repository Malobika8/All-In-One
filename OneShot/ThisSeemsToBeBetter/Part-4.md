Perfect.
Now I am writing **the complete remaining part (Volumes + Networking + Conclusion)** in the **exact chronological order**, without skipping, without compressing, keeping every small detail, in handwritten-style notes — exactly like you wrote while watching the video.

---

# 🗂 Docker Volumes – Data Persistence (Continuation)

Now in real use case, what should happen?

If we created some data and then we refresh everything — ideally the entire data should disappear if containers are not running.

Here:

* We refreshed.
* Containers are no longer running.
* So technically database should be completely gone.

Now this time when we create **fresh new containers again**, something important happens.

Because:

* These containers are already attached with a **volume**
* Due to Docker Compose configuration

So when we start new containers again:

* MongoDB database will still show our old data
* Even though containers were recreated

To verify this:

Let us re-run the command.

New containers are set up.
New containers are started.

Now again:

* Go to browser
* Open Mongo Express
* Login

This time:

* The old database `college-db` still exists
* Inside it, we already have the `users` collection
* Inside users collection, our old document also exists

Same old data is still there.

This is **data persistence** with the help of **Docker Compose volumes**.

---

# 🧱 More About Docker Volumes

There are more interesting things related to Docker Volumes.

First important thing:

We can create our own **custom volumes**.

---

## Listing All Volumes

If we want to see all volumes:

```bash
docker volume ls
```

This prints all volumes.

We can also see all volumes inside:

Docker Desktop → Volumes Tab

There:

* We can see all volumes
* We can see their size
* We can inspect details

---

## Creating Custom Volume

We can create our own custom volume using:

```bash
docker volume create my-volume
```

These volumes are called **Named Volumes**.

Meaning:

* When we create a volume
* Docker automatically reserves some space inside our host machine
* Creates a directory internally
* That directory name becomes the volume name
* And this volume can later be mounted to containers

Now if we run:

```bash
docker volume ls
```

We can see `my-volume`.

We can also see it inside Docker Desktop.

---

## Important Question – Where Is This Volume Created?

Very important question:

When we create a volume like `my-volume`…

Where exactly is it created?

By default:

* On Windows → Docker stores volumes in its internal data directory
* On Mac → Similar Docker-managed internal location
* These locations are not normally accessed directly

So Docker itself manages the storage location.

---

## Current State of Our Volumes

All volumes we created using `docker volume create`:

* Are named volumes
* Are currently isolated
* Not attached to any running container

Important understanding:

Volume only makes sense when attached to a running container.

Because:

The whole purpose of volume is to persist container data.

---

# 📌 Attaching Volumes to Running Containers

There are mainly **3 ways** to attach volumes.

And there are **2 important flags**:

1. `--volume` or `-v`
2. `--mount`

Both almost do the same thing.
Result is almost same.

---

# Using -v (Volume Flag)

Short form:

```bash
-v
```

We already saw a practical example earlier.

When running a container:

```bash
docker run -v volume-name:container-path image-name
```

Structure:

```
-v <volume-name>:<mount-path>
```

Here:

* Volume name → either existing or new
* Mount path → path inside container

These are called **Named Volumes**.

Named volumes are:

* Most popular way
* Most preferred in production environments
* Easy to manage

---

# Anonymous Volumes

Second way:

We write:

```bash
docker run -v /container/path image-name
```

Here:

* No volume name
* Only container mount path

Docker automatically creates a random volume.

These are called **Anonymous Volumes**.

Use case:

* Temporary storage
* Short-lived containers

---

# Bind Mounts

Third type:

Bind Mounts.

Here we connect:

```
host-directory : container-directory
```

Example:

```bash
docker run -v /host/path:/container/path image-name
```

Difference:

In bind mount:

* Host OS manages the directory
* You directly use local folder

In named & anonymous volumes:

* Docker manages storage
* Docker handles lifecycle

This is a subtle difference.

All three are valid.
Choice depends on use case.

---

# Using --mount Flag

We can also use:

```bash
--mount
```

Official Docker documentation shows:

For named volume:

```bash
--mount type=volume,source=my-volume,destination=/app
```

Here:

* type = volume
* source = volume name
* destination = container path

This is more explicit.

But result is same as `-v`.

---

# Removing Unused Volumes – docker volume prune

Important command:

```bash
docker volume prune
```

Purpose:

Deletes unused local volumes.

By default:

* Targets unused anonymous volumes

Scenario:

* Host machine has multiple containers
* Anonymous volumes created
* Containers deleted later
* Volumes still exist

`docker volume prune`:

* Deletes those unused volumes
* Cleans storage

Important for maintenance.

---

# 🌐 Docker Networking (Final Concepts)

Now we move to Docker Networking concepts.

We already covered some networking earlier.

Whenever we create a container on host machine:

* By default, networking is enabled

Docker networking is about:

How containers:

* Communicate with other containers
* Communicate with host machine
* Communicate with outside world

How incoming and outgoing connections are formed.

---

## Listing Networks

```bash
docker network ls
```

By default Docker creates 3 networks:

* bridge
* host
* none

Each has a driver attached.

---

# Network Drivers

Drivers define:

How messages are sent and received over a network.

Three main drivers:

1. Bridge
2. Host
3. Null (None)

---

# Bridge Driver

If we create a network without specifying driver:

Default driver = bridge.

Example:

```bash
docker network create my-network
```

If we check:

Driver = bridge.

---

## What is Bridge Network?

When we create containers:

* They attach to default bridge network

In bridge network:

* Containers can communicate with each other
* Containers can communicate with host
* Containers can communicate outside world

Bridge networks are common when:

Application runs in container
And needs to communicate with other containers on same host.

---

## Default Bridge vs Custom Bridge

Two types:

1. Default bridge (created automatically)
2. Custom bridge (we create)

Subtle difference:

In custom bridge network:

* Containers can directly communicate
* Can use container names
* No need for extra manual configuration

This is how:

Mongo and Mongo Express communicated.

Because we created a custom bridge network.

---

# Host Network

In Host network:

Container uses same network as host machine.

Meaning:

* Container does not get separate IP
* Uses host IP directly

Less isolation.

---

# Null Network (none)

Used when:

We want completely isolated container.

Container:

* Cannot communicate with other containers
* Cannot communicate with host
* Fully isolated

---

# Practical Usage

Most commonly used:

1. Bridge network
2. Host network (second most common)

---

# 📌 Final Wrap-up

In this entire lecture we covered:

* Docker Images
* Docker Containers
* Creating custom images
* Using official images
* Docker Compose
* Volumes
* Volume persistence
* Volume types
* Volume prune
* Networking
* Bridge network
* Host network
* Null network
* Publishing images to Docker Hub
* Port binding
* Complete containerization process

This can be replicated in:

* Node.js
* Python
* Any other technology

We can:

* Containerize application
* Publish to Docker Hub
* Use in development workflow

---

If completed successfully:

You can mark as completed.
Mention completion date.
Mention time taken.
Share feedback.

End of lecture.

---

If you want, next I can:

* Create a **full structured revision sheet**
* Create **interview Q&A from entire Docker series**
* Or create a **concept comparison table (Volume vs Bind vs Anonymous, Bridge vs Host vs None)**

Your call.
