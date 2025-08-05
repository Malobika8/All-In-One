## 🔹 `Files.readString()` and `Files.writeString()` – Simplified File I/O

---

### ✅ What is it?

Java 11 introduced **new utility methods** in `java.nio.file.Files`:

| Method                            | Purpose                          |
| --------------------------------- | -------------------------------- |
| `Files.readString(Path)`          | Read a text file into a `String` |
| `Files.writeString(Path, String)` | Write a `String` to a file       |

---

### 🔸 Before Java 11 (old way):

```java
byte[] bytes = Files.readAllBytes(Paths.get("file.txt"));
String content = new String(bytes, StandardCharsets.UTF_8);
```

### 🔸 Java 11 (new way):

```java
String content = Files.readString(Paths.get("file.txt"));
```

And to write:

```java
Files.writeString(Paths.get("file.txt"), "Hello, world!");
```

---

### ✅ Benefits:

* Much more readable
* No need to manage `InputStream`, `BufferedReader`, `StringBuilder`, etc.
* Automatically uses UTF-8 (unless you specify otherwise)

---

### 🔍 Optional Parameters:

You can also specify:

```java
Charset charset = StandardCharsets.UTF_8;
Files.readString(path, charset);
Files.writeString(path, text, charset, StandardOpenOption.CREATE);
```

---

### Question: Create a file `hello.txt`, write `"Hello Java 11!"` to it, and then read it back.

```java
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;

public class FileExample {
    public static void main(String[] args) throws Exception {
        Path path = Paths.get("src/test/hello.txt"); // relative to project root

        // Write to file
        Files.writeString(path, "Hello Java 11!");

        // Read from file
        String str = Files.readString(path);
        System.out.println("Read: " + str);
    }
}
```

This will:

* Create/write the file at `src/test/hello.txt`
* Then read it back and print the content

---

## 🔍 Quick Notes:

* If the directories don't exist (like `src/test`), it will throw `NoSuchFileException`
* If you want to create missing directories, you'll need `Files.createDirectories(path.getParent());` before writing
* You can use `StandardOpenOption.CREATE`, `APPEND`, etc. if needed

---


