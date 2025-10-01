## ✅ **Step 1: Create Your First Local Git Repository**

We’ll simulate a mini project to track with Git.

### 🔧 1. Open your terminal (Command Prompt, Git Bash, or Terminal)

### 📁 2. Create a new project folder

```bash
mkdir my-git-practice
cd my-git-practice
```

### 🌀 3. Initialize Git in this folder

```bash
git init
```

✅ Output should be:
`Initialized empty Git repository in ...`

This means Git is now **watching** this folder.

Set remote:

```bash
set remote add origin <git-url>
```

---

## ✅ **Step 2: Create and Track Your First File**

### 📄 1. Create a simple file

```bash
echo "Hello Git" > hello.txt
```

### 🔍 2. Check Git status

```bash
git status
```

It should say `hello.txt` is an **untracked file**.

Git sees it, but isn’t tracking it yet.

---

## ✅ **Step 3: Add File to Staging Area**

```bash
git add hello.txt
```

This tells Git:

> “Track this file and prepare it for the next commit.”

Check status again:

```bash
git status
```

Now it says: “Changes to be committed”

---

## ✅ **Step 4: Commit the Change**

```bash
git commit -m "Initial commit: added hello.txt"
```

✅ This creates a snapshot (version) of your code.

Now check history:

```bash
git log
```

You’ll see:

* A commit hash
* Author
* Date
* Commit message

---

## ✅ **Step 5: Make a Change and Commit Again**

### 📝 1. Edit the file

```bash
echo "Learning Git step by step." >> hello.txt
```

### 🔍 2. See the difference

```bash
git status
git diff
```

You’ll see the line that was added.

### 📥 3. Add and Commit

```bash
git add hello.txt
git commit -m "Added second line to hello.txt"
```

### 📜 4. Check full history

```bash
git log
```

You now have **two commits**!

### 5. Push to remote

For the first time, we need to set upstream

```bash
git push --set-upstream origin main
```
---

## 🧠 Quick Summary

| Git Command     | What it does                        |
| --------------- | ----------------------------------- |
| `git init`      | Start a Git repo in the folder      |
| `git status`    | Show tracked/untracked file changes |
| `git add`       | Stage files to be committed         |
| `git commit -m` | Save a snapshot with a message      |
| `git log`       | Show commit history                 |
| `git diff`      | See file changes before committing  |

---

