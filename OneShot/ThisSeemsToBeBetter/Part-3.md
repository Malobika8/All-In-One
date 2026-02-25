Alright. I’ve read **Part 3** carefully end-to-end.
Below are **pure handwritten-style notes**, in **English**, written **exactly in the same chronological order**, with **no compression, no optimization, no skipping**, and **no instructor references** — as if *you yourself wrote them while watching the video*.

I am intentionally keeping the **flow, repetitions, transitions, and gradual buildup**, because that’s what helps recall during revision.

---

# 🧠 PART 3 — Mongo Express UI → Docker Compose → Dockerfile → Image Layering → Publishing to Docker Hub

---

## Accessing Mongo Express on Browser

When we open **localhost:8081** in the browser and we see the **sign-in screen**, it means **Mongo Express is working successfully**.

This confirms that:

* Mongo Express container is running
* Port `8081` is correctly exposed
* Browser can access the container

---

## Mongo Express Login Credentials

The **username and password here are different** from the MongoDB username/password we set earlier.

For Mongo Express:

* **Username:** `admin`
* **Password:** `pass`

These are **standard default credentials**.

After entering `admin / pass` and signing in, we can see the **Mongo Express dashboard**.

This screen represents the **default setup of MongoDB**.

---

## Understanding MongoDB vs Mongo Express

At this point it becomes very clear:

* **MongoDB** is the actual **database**
* MongoDB is running **inside the Mongo container**
* **Mongo Express** is just a **Graphical User Interface (GUI)**

Mongo Express allows us to:

* View databases
* View collections
* Insert documents
* Modify data
* Do everything visually

This UI is very different from working via terminal commands.

---

## Default Databases in Mongo Express

By default, **three databases are already present**.

If we want to create our own database, we can do it directly from this UI.

---

## Creating Custom Database (college-db)

In the Node.js application code, the database name was already decided as **`college-db`**.

So we create the **same database here**.

Steps:

* Enter database name: `college-db`
* Click **Create Database**

Now the new database appears.

---

## Creating Collection (users)

Inside `college-db`, we create a new collection.

* Collection name: `users`
* Click **Create Collection**

These names are **not random** — they were already defined in the application code.

If we want something custom, we can:

* Modify the code
* Use different database / collection names

---

## Creating a Sample Document

Now we add a document inside the `users` collection.

We already know the structure:

* email
* username
* password

Sample values:

* email → `john@yahoo`
* username → `johndoe`
* password → `secret`

This document is added successfully.

Now everything that was possible via terminal is possible through this UI.

---

## Verifying Connection with Node.js Application

Now we need to check whether:

* MongoDB (inside container)
* Mongo Express
* Node.js application

are **actually connected**.

### Sending GET Request

We send a GET request to:

```
localhost:5050/getUsers
```

Output:

* A single user document is returned
* The same document we inserted via Mongo Express

This confirms:

* Node.js app is connected to MongoDB
* MongoDB is running inside a container
* No MongoDB is installed locally

---

## Conceptual Architecture Understanding

Current setup looks like this:

* Node.js application

  * Contains `server.js`
* MongoDB container

  * Actual database
* Mongo Express container

  * GUI

Node.js app:

* Fetches data from MongoDB container
* Inserts data into MongoDB container

Mongo Express:

* Shows the same data
* Because both are interacting with the **same MongoDB**

This works because:

* All containers are inside the **same Docker network**

---

## Real-World Applicability

This setup is **not limited to Node.js**.

Same approach works for:

* Python apps
* Golang apps
* .NET apps
* Any technology

If a service already has a Docker image available, we can:

* Use it directly
* Without installing it locally

---

## Testing POST Request

From the home page:

* Enter email → `johndoe@gmail.com`
* Enter username
* Enter password
* Click **Create Account**

Now:

* Refresh Mongo Express
* New user appears

Again:

```
GET /getUsers
```

Now two users are returned.

This confirms:

* GET works
* POST works
* Database connection is successful

This is the **first practical use case** of connecting an application with Docker containers.

---

# 🐳 Introduction to Docker Compose

When running **multiple containers**, Docker Compose becomes useful.

So far:

* Mongo
* Mongo Express
* Node app

All were started using **docker run commands**.

It worked, but:

* Commands were long
* Many options
* Not very maintainable

---

## Why Docker Compose?

When running containers manually, we define:

* Ports
* Container names
* Networks
* Environment variables
* Other configs

As applications grow, this becomes complex.

Docker Compose solves this by:

* Putting everything into **one YAML file**
* Running containers from that file

---

## YAML File Basics

YAML = **Yet Another Markup Language**

Benefits:

1. Commands become **structured and readable**
2. Editing becomes very easy
3. No need to re-type long terminal commands

Docker Compose is a tool to:

* Define
* Run
* Manage **multi-container applications**

It makes sense only when **multiple containers exist**.

---

## Docker Compose File Structure

Inside the YAML file:

### Version

Defines Docker Compose version
(example: `3.8`)

In latest Docker versions:

* This field is **obsolete**
* Warning appears
* Can be removed

---

### Services Section

All containers are defined under:

```
services:
```

Each container = one service

---

## Indentation Rule

Indentation is **extremely important** in YAML.

Wrong spacing = broken file.

---

## Defining Mongo Service

Service name: `mongo`

Inside mongo:

* image: `mongo`
* ports:

  * `27017:27017`
* environment variables

Environment variables can be written in **two ways**:

1. Dash (`- KEY=VALUE`)
2. Colon (`KEY: VALUE`)

Both are valid.

---

## Defining Mongo Express Service

Service name: `mongo-express`

Inside:

* image: `mongo-express`
* ports:

  * `8081:8081`
* environment variables:

  * admin username
  * admin password
  * MongoDB URL

MongoDB URL can be simplified by removing extra strings and adding `/` at the end.

---

## Role of YAML File

This file defines:

* Which containers to create
* How to configure them
* How they interact

---

## Running Containers Using Docker Compose

Two important commands:

### docker compose up

* Creates containers
* Starts them
* Usually used with `-d` (detached)

### docker compose down

* Stops containers
* Deletes containers
* Deletes network

---

## Automatic Network Creation

In YAML:

* No network was defined

Docker Compose automatically:

* Creates a **default network**
* Runs all services inside it

So:

* No need to manually create networks

---

## Cleaning Old Containers

Old containers were removed because:

* Port `8081` was already used
* New container could not bind to same port

So:

* Old containers deleted
* Old images deleted
* Fresh setup created

---

## Running docker compose

Command used:

```
docker compose -f mongodb.yml up -d
```

Output shows:

* Warning about version
* Images pulled
* New network created
* Containers started

---

## Data Persistence Observation

Old database (`college-db`) was **not present**.

Reason:

* Containers were recreated
* No data persistence

Docker containers **do not persist data by default**.

To persist data, **Docker Volumes** are required (covered later).

So database and collection were recreated again.

---

## Verifying Again

* Create database
* Create users collection
* Insert user
* GET request works

This confirms:

* Docker Compose setup is correct

---

# 📦 Dockerizing Our Own Application

Now comes another major use case:
**Dockerizing our own application**

This means:

* Converting app → Docker image
* Running app inside container
* Sharing app as an image

This works for:

* Node.js
* Python
* Any application

---

## Role of Dockerfile

Dockerfile is:

* A blueprint
* Contains instructions
* Used to build images

---

## Important Dockerfile Instructions

### FROM

Defines base image
Every image is based on another image

Example:

* Node app → needs Node
* Base image = `node`

---

### Layering Concept

Images are built **layer on layer**.

Example:

* Debian → base
* Node → built on Debian
* App → built on Node

This is why when pulling images, **multiple layers** download.

---

### WORKDIR

Defines working directory inside container

---

### COPY

Copies files from host → container

---

### RUN

Executes commands during image build

Multiple RUN commands are allowed.

---

### CMD

Defines default command to run when container starts

Only **one CMD allowed**.

Example:

```
node server.js
```

---

### EXPOSE

Documents port usage

---

### ENV

Defines environment variables

---

## Creating Dockerfile

* File name: `Dockerfile`
* Capital D
* No extension

---

## Base Image Selection

Base image: `node`

This image itself:

* Is based on Debian
* Uses layered images

---

## Defining Environment Variables

Inside Dockerfile:

* MongoDB username
* MongoDB password

---

## Directory Creation

* Create `/test-app` inside container
* Copy application files into it

---

## CMD Path Correction

Inside container:

* Root folder doesn’t contain `server.js`
* `server.js` exists inside `/test-app`

So CMD becomes:

```
node /test-app/server.js
```

---

## Building Docker Image

Command:

```
docker build -t test-app:1.0 .
```

This:

* Detects Dockerfile
* Builds image layer by layer

---

## Verifying Image

Command:

```
docker images
```

New image:

* test-app:1.0

---

## Running Container from Image

```
docker run test-app:1.0
```

Output:

```
Server running on port 5050
```

---

## Interactive Mode

```
docker run -it test-app:1.0 bash
```

Now:

* Inside container
* Can run `ls`
* Can inspect file system

---

## Node Modules Discussion

If `node_modules` are excluded:

* Dockerfile must include:

```
RUN npm install
```

Whether to include `node_modules` depends on Dockerfile setup.

---

## Real-World Integration

In real projects:

* Mongo
* Mongo Express
* Node app

All are run using **Docker Compose together**.

---

# 🌍 Publishing Image to Docker Hub

To share images:

* Create Docker Hub account
* Create repository
* Push image

Repository can be:

* Public
* Private

---

## Login to Docker Hub from Terminal

Two ways:

1. `docker login`
2. Browser-based device authentication

After login → authentication successful.

---

## Pushing Image

```
docker push username/test-application
```

All image layers are pushed.

---

## Pulling Image Anywhere

Now:

* Code can be deleted locally
* Image can be pulled anytime
* Container can be run instantly

---

## Final Outcome

* Application fully dockerized
* Image published
* Can be reused
* Can be shared
* Can be deployed anywhere

---

If you want, next we can:

* Convert **all three containers into one docker-compose.yml**
* Or create **revision cheat sheets**
* Or do **interview Q&A mapping from this video**

Just tell me how you want to proceed.
