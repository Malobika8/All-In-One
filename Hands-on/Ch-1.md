## ✅ Step 1: What is Git?

Git is a **version control system**.
It helps you:

* Track changes to code or files
* Revert to older versions
* Work with teams without overwriting each other’s work

💡 Think of it like **Google Docs' version history**, but for code and files — and much more powerful.

---

## ✅ Step 2: Git vs GitHub

* **Git** = Local tool to track code changes.
* **GitHub** = Online service to host Git repositories and collaborate with others.

You can use Git **without** GitHub, but not the other way around.

---

## 🛠️ Step 3: Install Git and Set It Up

### ✅ 1. Install Git

* **Windows**: Download from [https://git-scm.com/downloads](https://git-scm.com/downloads)
* **Mac**: `brew install git` (if Homebrew is installed)
* **Linux**: `sudo apt install git` or `sudo dnf install git`

### ✅ 2. Configure Git

Once installed, open terminal or Git Bash and run:

```bash
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

You can check settings:

```bash
git config --list
```

---

## 📦 Step 4: Create Your First Repository (Practice)

### 🧪 Try this in a folder:

```bash
mkdir my-first-git
cd my-first-git
git init
```

Now you have a Git repo! Try creating a file:

```bash
echo "Hello Git" > hello.txt
git status
git add hello.txt
git commit -m "Initial commit"
```

Now you’ve made your **first commit** 🎉

---

