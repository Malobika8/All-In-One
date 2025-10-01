## 🛠️ Java 9: **Try-With-Resources Enhancement**

In Java 7, the **try-with-resources** statement was introduced to automatically close resources like streams, readers, etc.

But in Java 7/8, there was a limitation:

---

### ❌ Before Java 9:

You **had to declare the resource inside the try(...) itself**, like:

```java
try (BufferedReader reader = new BufferedReader(new FileReader("file.txt"))) {
    // use reader
}
```

If `reader` was declared **before** the `try` block, this wouldn't compile.

---

### ✅ Java 9 Fix:

You can now use **effectively final variables** in try-with-resources:

```java
BufferedReader reader = new BufferedReader(new FileReader("file.txt"));

try (reader) {
    System.out.println(reader.readLine());
}
```

✅ **Much cleaner** and avoids re-declaration.

---

### Question

Write code that:

1. Creates a `BufferedReader` for a file named `"sample.txt"`
2. Uses the **Java 9 style** try-with-resources to read one line
3. Catches and prints any exceptions

```
BufferedReader reader = new BufferedReader(new FileReader("file.txt"));

try (reader) {
    System.out.println(reader.readLine());
} 
catch(Exception ex){
ex.printStackTrace();
}
```
### 🔍 What's right:

* Declared the `reader` **before** the `try(...)` block ✅
* Used it directly in `try(reader)` ✅
* Caught exceptions properly ✅

This feature is especially helpful when:

* You need to **reuse** the resource reference outside `try`
* You want to avoid **nested variable declarations**

### 🧠 Quick Note:

The variable used in `try(resource)` must be **effectively final**, meaning:

* You don't reassign it before the try block
* It behaves like a final variable

## FYI - What does "effectively final" mean?

A variable is **effectively final** if it is **never reassigned** after it's initialized — even if you don't explicitly use the `final` keyword.

### ✅ Valid Example (Effectively Final):

```java
BufferedReader reader = new BufferedReader(new FileReader("file.txt"));

try (reader) {
    System.out.println(reader.readLine());
}
```

* `reader` is assigned **once**, never changed ✅
* So it's **effectively final**, and allowed inside `try(reader)` ✅

---

### ❌ Invalid Example (Not Effectively Final):

```java
BufferedReader reader = new BufferedReader(new FileReader("file1.txt"));
reader = new BufferedReader(new FileReader("file2.txt")); // Reassigned ❌

try (reader) {
    System.out.println(reader.readLine());
}
```

This will cause a **compile-time error**:

```
error: resource 'reader' is not a final or effectively final variable
```

---

### ✅ Fixed Version:

```java
BufferedReader reader = new BufferedReader(new FileReader("file2.txt"));

try (reader) {
    System.out.println(reader.readLine());
}
```

Or make it explicitly final:

```java
final BufferedReader reader = new BufferedReader(new FileReader("file2.txt"));
```

---

### Summary:

| Variable Reassigned? | Effectively Final? | Try-with-resources Allowed? |
| -------------------- | ------------------ | --------------------------- |
| ❌ No                 | ✅ Yes              | ✅ Yes                       |
| ✅ Yes                | ❌ No               | ❌ No (Compile error)        |

