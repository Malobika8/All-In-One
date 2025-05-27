## 📦 What Are Docker Volumes? (Simple Explanation)

> **Volumes** let you **share files between your local machine and the container**.

This is especially useful during **development**, where you want your container to see your local code, so you don't need to rebuild the image every time.

---

## ✅ Summary: What we should do with Volumes

### Run:

```bash
docker run --rm \
  -v "/Users/malobikanandy/IdeaProjects/Docker/Docker Volumes/DockerVolPractice:/app" \
  -w /app \
  openjdk:17-jdk-slim \
  java -jar target/DockerVolPractice-1.0-SNAPSHOT.jar
```

This command:

| Part                    | Meaning                                                                     |
| ----------------------- | --------------------------------------------------------------------------- |
| `--rm`                  | Remove the container after it exits                                         |
| `-v "/local/path:/app"` | Mount your project into the container at `/app`                             |
| `-w /app`               | Set the working directory inside the container to `/app`                    |
| `openjdk:17-jdk-slim`   | Use this image to run Java                                                  |
| `java -jar ...`         | Run your app inside the container using the latest JAR you compiled locally |

---

## ✅ Why This Is Cool

* You **don’t rebuild the Docker image** when code changes.
* You **control the source code and JAR locally**, but run it **inside a container**.
* This mirrors how many dev teams work day-to-day.

---

## 🔁 Your Dev Cycle Now Looks Like This

```bash
# 1. Make code changes
# 2. Rebuild the JAR
mvn clean package

# 3. Run it inside Docker without rebuilding the image
docker run --rm -v "$(pwd):/app" -w /app openjdk:17-jdk-slim java -jar target/YourApp.jar
```

---

## 🧪 What You Should Try Next

### 🧩 1. Try Editing Your Code

* Make a small change to your Java code (`System.out.println("Updated!")`)
* Run `mvn package`
* Rerun your Docker `run` command
* ✅ Confirm that your change appears in the output (without rebuilding the Docker image!)

---

### 🔄 2. Compare with Docker Image Rebuild

* Go back to using a `Dockerfile`
* Build the image (`docker build -t myapp .`)
* Change your code
* Rebuild image again (`docker build ...`)
* You'll see that **volume mounting is faster** for dev

---

### 📦 3. Explore Named Volumes (Optional)

You can also try Docker **named volumes**, which store data **outside the container**, even if the container is removed.

For now, though, you’re focused on **bind mounts** (local file system mapped into container), which is perfect.

---

## ✅ You're All Set!

To wrap up:

* You now understand how to **build**, **run**, and **develop with volumes** in Docker
* You know how to **run code from your machine** inside a container using volume mounts
* You learned how to **make your JAR executable** using `maven-jar-plugin`

---
