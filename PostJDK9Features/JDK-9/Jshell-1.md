### 🔹 JShell (Java Shell) - Interactive Java

JShell is a **REPL** (Read-Eval-Print Loop) tool introduced in Java 9. It allows you to run Java code snippets **interactively** without writing an entire class or method.

#### 🧠 Why is this useful?

* Great for testing small code pieces quickly.
* Ideal for learning Java or trying out APIs.
* No need to set up a full project or compile a class.

---

### 🛠️ How to use JShell?

Just open a terminal and type:

```bash
jshell
```

Then you can type Java code like:

```java
int x = 10;
System.out.println(x * 2);
```

No `public static void main`, no class required!

### ✅ 1. **Can we declare methods in JShell?**

You can write methods just like you would in a normal class:

```java
int add(int a, int b) {
    return a + b;
}
```

Then you can simply call:

```java
add(2, 3);
```

---

### ✅ 2. **How do you exit JShell?**

Tthe official and most portable way is:

```bash
/exit
```

This works reliably on **all OS platforms**, including macOS and Linux.

---

### ❓ 3. **Command to list all variables and methods declared in JShell**

Here's what you can use:

| Command    | Description                 |
| ---------- | --------------------------- |
| `/vars`    | List all declared variables |
| `/methods` | List all declared methods   |
| `/list`    | Show all snippets entered   |
| `/help`    | Show help with all commands |

---

