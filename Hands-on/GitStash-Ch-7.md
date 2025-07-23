# 🧺 `git stash` — Save Your Work Without Committing

## ✅ Why we use it:

You're in the middle of some changes but suddenly need to:

* Switch branches
* Pull latest code
* Work on a bugfix
* Without committing unfinished work

**→ Use `git stash` to save your changes temporarily.**

---

## 🔧 Basic Usage:

### 1️⃣ Save current changes:

```bash
git stash
```

* Moves your **uncommitted** changes (tracked files) to a stash stack
* Cleans your working directory

> 📝 Optional: `git stash save "message"` (older syntax)

---

### 2️⃣ See what you’ve stashed:

```bash
git stash list
```

```
stash@{0}: WIP on main: 123abcd Added login feature
stash@{1}: WIP on main: 456defg Fixed layout bug
```

---

### 3️⃣ Bring back (apply) the stash:

```bash
git stash apply
```

* Applies **latest stash**, keeps it in stash stack

```bash
git stash pop
```

* Applies and **removes** stash from stack

---

### 4️⃣ Drop a stash manually:

```bash
git stash drop stash@{0}
```

---

### 5️⃣ Clear all stashes:

```bash
git stash clear
```

⚠️ Irreversible — deletes all stashed items.

---

## 🧪 Example Scenario:

```bash
# make some edits
git status → shows modified files

git stash         # saves them
git switch bugfix # move to another branch

# later...
git switch main
git stash pop     # brings back your saved edits
```

---

## 🔥 Bonus: Stash Untracked and Ignored Files

```bash
git stash -u   # also stashes untracked files
git stash -a   # stashes ignored files too
```

---

## 🧠 Scenario-Based Git Stash Question

You are working on the `main` branch and made some local changes:

* Edited `HomeController.java`
* Edited `application.properties`

You suddenly get a message:

> "Urgent bug fix required on `hotfix/login-bug` branch!"

But you **don’t want to commit your incomplete changes** yet.

### ❓What’s the best sequence of Git commands to follow?

**A.**

```bash
git commit -am "temp"
git switch hotfix/login-bug
```

**B.**

```bash
git add .
git reset
git switch hotfix/login-bug
```

**C.**

```bash
git stash
git switch hotfix/login-bug
```

**D.**

```bash
git clean -fd
git switch hotfix/login-bug
```

