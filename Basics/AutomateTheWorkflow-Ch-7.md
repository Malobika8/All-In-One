Automating your Docker workflow with a **shell script** or **Makefile** will save time and reduce errors. Let’s start with a **shell script** that:

1. Cleans and builds your Maven project
2. Runs your app inside a Docker container using volume mount

---

## 🧾 Step-by-Step: Create a Shell Script to Automate Your Workflow

### ✅ Step 1: Create the script

Create a file in your project root:

```bash
touch run.sh
chmod +x run.sh
```

### ✅ Step 2: Add the following content to `run.sh`

```bash
#!/bin/bash

# Step 1: Build the app
echo "🔨 Building project..."
mvn clean package

# Step 2: Run the app in Docker with volume mount
echo "🐳 Running app in Docker..."
docker run --rm -v "$(pwd):/app" -w /app openjdk:17-jdk-slim java -jar target/DockerVolPractice-1.0-SNAPSHOT.jar
```

> 🔁 Adjust the `.jar` name if yours is different.

---

### ✅ Step 3: Run your script

```bash
./run.sh
```

You should see:

```
🔨 Building project...
<output from Maven build>

🐳 Running app in Docker...
Hello world!
```

Boom 💥— one command, everything happens.

---

## 🧪 Want to Make It Smarter?

You can add options or checks like:

```bash
#!/bin/bash

set -e  # Stop script on first error

JAR_NAME="target/DockerVolPractice-1.0-SNAPSHOT.jar"

echo "🔨 Building Maven project..."
mvn clean package

if [ ! -f "$JAR_NAME" ]; then
  echo "❌ Build failed: $JAR_NAME not found!"
  exit 1
fi

echo "🐳 Running app in Docker..."
docker run --rm \
  -v "$(pwd):/app" \
  -w /app \
  openjdk:17-jdk-slim \
  java -jar "$JAR_NAME"
```

---

