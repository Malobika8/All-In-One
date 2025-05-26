# What is Docker?
Docker is a tool that allows you to package your application and its environment into a lightweight, portable container. This container can run anywhere—your laptop, a server, or cloud—without worrying about setup differences.

## Why learn Docker?
- Simplifies setup and deployment
- Ensures consistency across environments (dev, test, production)
- Makes microservices and scalable systems easier
- Widely used in industry (DevOps, CI/CD pipelines, cloud deployments)

---

### 1. **"Package your application and its environment" — What environment?**

When we say **environment**, we mean everything your app needs to run correctly, including:

* **Operating System libraries and dependencies:** Like specific versions of Linux libraries, system tools, etc.
* **Runtime:** For example, Java Runtime Environment (JRE) for Java apps, Python interpreter for Python apps, Node.js runtime, etc.
* **Application dependencies:** External libraries, frameworks, binaries (like `Maven`, `nginx`, database clients).
* **Configuration files:** Environment variables, config files your app reads.
* **Settings like ports, file system structure, and more.**

---

### Why package environment?

Normally, if you move your app to another machine or server, you must ensure **all these dependencies and settings are installed/configured exactly the same**. This is hard, error-prone, and causes bugs.

With Docker, you **package the app *plus* this environment into a container** so it always runs the same everywhere.

---

### 2. **"Simplifies setup and deployment" — What deployment and to where?**

* **Deployment** means *getting your application running on a target system*—like a server, cloud platform, or even your colleague’s laptop.

* Traditionally, deploying means:

  * Installing the right OS and software versions.
  * Configuring environment variables.
  * Installing dependencies.
  * Starting the app with the correct commands.

* **With Docker, deployment is simplified because you just:**

  * Build a Docker image once.
  * Push it to a container registry (like Docker Hub).
  * Run the same container image anywhere (on any server or cloud) with the same behavior.

---

### **Where can you deploy Docker containers?**

* **Cloud providers:** AWS (ECS, EKS), Google Cloud (GKE, Cloud Run), Azure (AKS)
* **On-premises servers:** Your company’s own machines
* **Local machines:** Your laptop or developer machines
* **CI/CD pipelines:** Automated build and test systems

---

### Summary

| Concept              | Explanation                                                  |
| -------------------- | ------------------------------------------------------------ |
| Environment packaged | OS libs, runtimes, app dependencies, configs                 |
| Deployment           | Getting app running on a target machine/server               |
| Deployment locations | Cloud, on-prem servers, local developer machines, CI systems |

---

### Does Docker provide JRE?

* Docker **doesn't provide JRE by itself**, but you can use a **base image that already includes JRE**.
* For example, the official Docker image `openjdk:11` includes a full JRE (Java Runtime Environment) and JDK inside the container.

---

### What does this mean practically?

If you build your Docker image **based on `openjdk:11`**, your app’s runtime environment inside the container **already has the JRE**.

So, when you run that container on any machine (your laptop, a server, cloud), **you do NOT need to have JRE installed on the host system**.

---

### Example:

```dockerfile
FROM openjdk:11
COPY myapp.jar /app/myapp.jar
CMD ["java", "-jar", "/app/myapp.jar"]
```

* This image contains the JRE.
* When you run the container, the app runs inside this environment.
* Your host OS doesn’t need Java installed at all!

---

### Summary:

| Before Docker                                  | After Docker                              |
| ---------------------------------------------- | ----------------------------------------- |
| You must install JRE on every machine manually | JRE is bundled inside the container image |
| Setup can vary, causing bugs                   | Container runs consistently everywhere    |

---

**Docker images can include everything your app needs to run, including JRE, runtime libraries, dependencies, etc., making your life much easier.**

---
