## 🔹 Why Do We Need Encoding Systems Like ASCII or Unicode?

Computers store everything as **binary (0s and 1s)** — whether it's text, images, or videos.

But humans deal with **characters** like `A`, `B`, `1`, `@`, `♥`, `你`, etc.

So, there must be a **standardized way to map characters to numbers (binary)** so computers can understand and store them.

That’s where **character encodings** like **ASCII** and **Unicode** come in.

---

## 🔸 What is ASCII?

**ASCII** = *American Standard Code for Information Interchange*

* It was created in the 1960s.
* It only supports **English characters**.

### 🔤 What it includes:

* Uppercase letters: `A` to `Z`
* Lowercase letters: `a` to `z`
* Digits: `0` to `9`
* Common symbols: `@`, `#`, `$`, `+`, etc.
* Control characters: newline, tab, etc.

### ✅ Example:

| Character | ASCII Decimal | Binary   |
| --------- | ------------- | -------- |
| A         | 65            | 01000001 |
| a         | 97            | 01100001 |
| 0         | 48            | 00110000 |

### 🚫 Limitations:

* Only 128 characters (7 bits) — can’t handle characters like `é`, `ß`, `€`, `你`, `😊`.

---

## 🔸 What is Unicode?

**Unicode** is a **universal** character encoding system meant to include **all characters** in all languages (and symbols, emojis, etc.).

* Started in the 1990s.
* Can represent **over 1 million characters**.
* It’s the **modern standard**.

### 📦 Unicode is not just one thing:

It comes in **different encodings**, such as:

| Encoding | Description                                             |
| -------- | ------------------------------------------------------- |
| UTF-8    | Most common on the web, uses 1 to 4 bytes per character |
| UTF-16   | Uses 2 or 4 bytes per character                         |
| UTF-32   | Uses exactly 4 bytes per character                      |

---

## 🔁 ASCII vs Unicode

| Feature          | ASCII                           | Unicode                              |
| ---------------- | ------------------------------- | ------------------------------------ |
| Year created     | 1960s                           | 1990s                                |
| Size             | 7 bits (128 characters)         | Variable (UTF-8: 1–4 bytes)          |
| Language support | English only                    | All human languages, emojis, symbols |
| Compatibility    | Included in Unicode (first 128) | Superset of ASCII                    |

➡️ So, **Unicode includes ASCII**. The first 128 characters of Unicode are the same as ASCII.

---

## 🔍 Why do multiple encodings (like UTF-8, UTF-16) exist?

They are different **ways of storing** Unicode characters in memory or files:

* **UTF-8** is space-efficient for English text (same as ASCII) but can grow for other languages.
* **UTF-16** is better for languages like Chinese, Japanese, but less efficient for plain English.
* **UTF-32** is fixed-size but wastes space.

---

## 🔚 Final Analogy:

Think of characters like **people from different countries**.

* **ASCII** is like a guest list with only Americans.
* **Unicode** is like a guest list for the **entire world** — with **translation** systems (UTF-8, UTF-16, etc.) deciding how to fit each person’s name tag in memory.

---

## ✅ Can we write entire programs in **Hindi** or **other languages**?

### 🔸Answer: **Partially — yes**, but with **limitations**.

---

### ✅ 1. **What can be written in any language?**

* **Comments**: ✅ Yes
* **Variable names**: ✅ Yes
* **Function names**: ✅ Yes
* **String literals**: ✅ Yes

✅ These parts are fully under your control and can be in **any Unicode-supported language** like Hindi, Chinese, Arabic, etc.

```java
// यह एक उदाहरण है
String नाम = "मालोबिका";
System.out.println("नमस्ते दुनिया");
```

### ❌ 2. **What **cannot** be translated?**

* **Language Keywords** like:

  * `if`, `else`, `while`, `switch`, `for`, `class`, `public`, `return`, etc.

🧠 These are **part of the programming language specification**, and they are **fixed** — like grammar rules.

---

## ❓ Why are keywords not available in Hindi or other languages?

1. ✅ Programming languages were originally designed **in English-speaking countries**.
2. ✅ To ensure **global standardization**, the keywords were defined **in English**.
3. ❌ Most languages do **not support custom language localization** of keywords.

For example:

```java
// ❌ You CANNOT write this in Java
अगर (x > 0) {
    वापिस करें x;
} अन्यथा {
    वापिस करें 0;
}
```

This will give a **syntax error**, because Java doesn’t recognize `अगर` (`if`), `वापिस करें` (`return`), or `अन्यथा` (`else`).

---

## 🔸 Are there any programming languages that support **native language keywords**?

### ✅ Yes — but they're rare or experimental.

Some examples:

| Language                        | Features                                                |
| ------------------------------- | ------------------------------------------------------- |
| **LOLCODE**                     | Uses humorous English phrases like `HAI`, `KTHXBYE`     |
| **Bharat Programming Language** | A new project trying to bring Hindi-style keywords      |
| **Scratch (block-based)**       | Allows interface translation into Hindi or any language |
| **Catrobat / Blockly**          | Block languages with keyword localization support       |

But **mainstream languages like Java, C++, Python, etc. do not support keyword localization**.

---

## ✅ Summary

| Feature            | Can be Hindi/Any Language? | Example                |
| ------------------ | -------------------------- | ---------------------- |
| Variable Names     | ✅ Yes                      | `int उम्र = 25;`       |
| Function Names     | ✅ Yes                      | `void दिखाओ()`         |
| Comments           | ✅ Yes                      | `// यह एक टिप्पणी है`  |
| String Literals    | ✅ Yes                      | `"नमस्ते"`             |
| Keywords (if, for) | ❌ No                       | Must remain in English |

---

## 🧠 TL;DR:

You **usually don’t manually specify** ASCII or Unicode in your source code, but the **editor/compiler/file encoding setting** tells the system how to interpret the characters.

Let’s go step-by-step.

---

## ✅ 1. **How does the computer know which encoding is used in a program?**

### 🔹 The **text editor or IDE** you use (like VS Code, IntelliJ, Notepad++, etc.) **saves the file using a certain encoding** — most commonly **UTF-8**.

* You can check/set this in your editor.
* For example, in VS Code you’ll see something like:

  ```
  UTF-8  🔽  (in the bottom-right corner)
  ```

### 🔹 When you compile or run your program, the compiler or runtime:

* Reads the file as per the encoding.
* If encoding doesn't match actual file content: ❌ You get strange characters or errors.

---

## ✅ 2. **What is the default encoding?**

| Context             | Default Encoding                                                    |
| ------------------- | ------------------------------------------------------------------- |
| Most modern editors | **UTF-8**                                                           |
| Java source files   | UTF-8 (since Java 18 officially)                                    |
| HTML/Web            | UTF-8 is the standard                                               |
| Linux terminals     | UTF-8                                                               |
| Windows             | Often used to be Windows-1252, but now also UTF-8 in newer versions |

---

## 🔸 3. **Where can you specify the encoding (if needed)?**

### 💻 In Java:

```bash
javac -encoding UTF-8 Hello.java
```

This tells the compiler to interpret the source file using UTF-8.

### 📄 In HTML:

```html
<meta charset="UTF-8">
```

Tells the browser to interpret the HTML file as UTF-8 encoded.

---

## 🔹 4. **ASCII vs Unicode in real-world files**

* If your program only contains English characters, it looks **identical in ASCII and UTF-8**.
* But if you write `नमस्ते` or `😊`, **ASCII can’t store that** — only Unicode (UTF-8/UTF-16/etc.) can.

---

## ❗ Important:

> Text encoding is **not part of the programming language syntax** — it’s a property of **how the file is saved on disk**.

---

## ✅ Summary

| Question                                  | Answer                                                                      |
| ----------------------------------------- | --------------------------------------------------------------------------- |
| Do I write `ASCII` or `UTF-8` in my code? | ❌ No, not usually. It’s handled by the editor/compiler.                     |
| How does computer know?                   | Based on how the file is saved (file encoding).                             |
| Where can I check?                        | In your code editor or by using compile/run options.                        |
| What’s usually used today?                | ✅ **UTF-8** — it supports everything and is backward-compatible with ASCII. |

---
