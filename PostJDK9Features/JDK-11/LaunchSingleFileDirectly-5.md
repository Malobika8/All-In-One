## ✅ Java 11 Feature: Launch Single-File Java Source Code Directly (No Compilation Step)

### 🔹 What is it?

From Java 11 onward, you can **run a `.java` file directly from the terminal**, without compiling it manually using `javac`.

---

### ✅ Example:

You can now run:

```bash
java HelloWorld.java
```

Even if the file contains:

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello from Java 11!");
    }
}
```

---

### ❗ No `javac` step needed:

Before Java 11:

```bash
javac HelloWorld.java
java HelloWorld
```

Now (Java 11+):

```bash
java HelloWorld.java  // ✅ Direct execution
```

---

### ✅ Why is this useful?

* Quick scripting or testing
* No build tools needed
* Useful for **coding interviews**, **scripts**, **demos**, etc.
* Great for students, automation, DevOps tools

---

### 🚫 Limitations:

* Works **only for one file**
* You **can’t use packages** or `import` other project files easily
* Not meant for large projects — just quick utilities or experiments

---

### ✅ Bonus: You can pass arguments too!

```bash
java HelloWorld.java arg1 arg2
```

And read them via `args[]` in your `main()` method.

---

