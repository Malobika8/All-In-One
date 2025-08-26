### ✅ 1. **"An image when run is called a container"**

* Think of an **image** as a *frozen recipe*.
* When you run it, Docker **"unfreezes"** it to create a **live, isolated environment** = a **container**.

---

### ✅ 2. **"That image is only of JDK which has been packaged"**

* The image `openjdk:11-jdk` is **a pre-built environment** that includes:

  * A minimal Linux OS (e.g., Debian or Alpine depending on tag)
  * The JDK (Java Development Kit)
  * Any required dependencies (e.g., system libraries)

So yes — this image is just a *packaged JDK environment* with nothing else yet.

---

### ✅ 3. **"When we run the container, it will keep things ready"**

* Docker **instantiates** the image into a **ready-to-use Linux environment**.
* JDK is **pre-installed**, so you can immediately use `java`, `javac`, etc.
* It’s like booting into a tiny Linux machine that already has JDK installed — in seconds.

---

### ✅ 4. **"We can confirm with java --version"**

Inside the container, try:

```bash
java --version
```

or

```bash
java -version
```

This confirms the JDK is available and working. You can also try:

```bash
javac -version
```

To confirm the Java compiler is there.

---

### Visualizing it:

```
Docker Image:
----------------------------
| Minimal Linux OS        |
| Java JDK 11             |
----------------------------

   ↓ docker run

Docker Container:
-----------------------------------------
| A live, running environment based on  |
| the image. JDK is ready to use here.  |
-----------------------------------------

You enter container -> type java --version -> ✅
```

---

