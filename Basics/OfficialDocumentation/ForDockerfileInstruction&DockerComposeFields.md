Great question! You can find **all valid Dockerfile instructions** and **Docker Compose fields** in the official Docker documentation. Here’s exactly where and how to access them:

---

## 🐳 **1. Dockerfile Commands Reference**

### 📘 Official Docs:

🔗 [https://docs.docker.com/engine/reference/builder/](https://docs.docker.com/engine/reference/builder/)

This page covers all Dockerfile instructions like:

* `FROM`
* `RUN`
* `COPY`
* `WORKDIR`
* `CMD`
* `ENTRYPOINT`
* `ENV`
* `EXPOSE`
* And more

It also explains syntax, examples, and when to use what.

---

## 🧱 **2. Docker Compose File Reference (`docker-compose.yml`)**

### 📘 Official Docs:

🔗 [https://docs.docker.com/compose/compose-file/](https://docs.docker.com/compose/compose-file/)

Here you’ll find:

* Supported **versions** (`3`, `3.8`, `3.9`, etc.)
* Definitions of all **top-level keys** like:

  * `version`
  * `services`
  * `volumes`
  * `networks`
* Under `services`, all possible fields:

  * `build`
  * `image`
  * `container_name`
  * `ports`
  * `volumes`
  * `environment`
  * `depends_on`
  * `command`
  * `entrypoint`
  * And more

Each field is well documented with examples.

---

## 🔍 **How to Search Easily**

You can just Google:

* `dockerfile <instruction>` → e.g., `dockerfile copy`
* `docker-compose <field>` → e.g., `docker-compose depends_on`

And the **top result is almost always** from the official docs.

---
