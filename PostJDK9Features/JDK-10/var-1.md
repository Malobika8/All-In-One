## **Local Variable Type Inference (`var`)**

This is the **headline feature** of Java 10.

---

### 🧠 What is it?

You can now use `var` to declare **local variables**, and Java will infer the type **automatically**.

---

### ✅ Example:

```java
var name = "Malobika";     // Inferred as String
var number = 42;           // Inferred as int
var list = new ArrayList<String>();  // Inferred as ArrayList<String>
```

* It **does not mean dynamic typing** (like JavaScript or Python)
* Type is inferred at **compile time**, and it's still strongly typed

---

### ⚠️ Rules:

| ✅ Allowed With     | ❌ Not Allowed With |
| ------------------ | ------------------ |
| Local variables    | Method parameters  |
| Loop variables     | Class fields       |
| Try-with-resources | Return types       |

So you **can** do:

```java
var str = "Hello";
```

But **not**:

```java
public var getName() { ... } // ❌ Invalid
```

---

### Question:

Write code using `var` to:

1. Declare a list of strings with `"apple"`, `"banana"`, `"cherry"`
2. Loop through it and print each fruit

```
var list = new ArrayList<>(Arrays.asList("apple", "banana", "cherry"));
for(String str: list){
  System.out.println(str);
}
```
---

### ✅ Breakdown:

```java
var list = new ArrayList<>(Arrays.asList("apple", "banana", "cherry"));
```

* `var` infers this as: `ArrayList<String>`
* Still **strongly typed** — you can't add an `Integer` to this list

```java
for (String str : list) {
    System.out.println(str);
}
```

* Classic and correct usage

---

### Twist

Use `var` **inside** the loop as well:

```java
for (var fruit : list) {
    System.out.println(fruit);
}
```

Java will infer `fruit` as `String` here too!

---

