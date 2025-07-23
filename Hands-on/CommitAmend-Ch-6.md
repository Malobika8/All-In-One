## 🛠️ What is `git commit --amend`?

### ➕ It’s used to **modify the last commit**, either:

* To **change the commit message**
* Or to **add/remove files** to the last commit

---

### ✅ Example 1: Fix a typo in the commit message

You made a commit like this:

```bash
git commit -m "Fix loginc bug"  # typo: 'loginc' instead of 'login'
```

To fix it:

```bash
git commit --amend -m "Fix login bug"
```

👉 This replaces the old commit with a corrected one.

---

### ✅ Example 2: Forgot to add a file before committing

```bash
git add file1.java
git commit -m "Add login handler"
```

But you realize you forgot `file2.java`.

```bash
git add file2.java
git commit --amend
```

It opens an editor (or uses the same message) and adds `file2.java` to the previous commit.

---

### ⚠️ Important:

`--amend` rewrites history — so **only use it before pushing**.
If the commit is already pushed, **don't amend**, or your teammates may get conflicts.

---

## 🧠 Git Amend – Scenario-Based Question

You're working locally on a Git project.

You just ran:

```bash
git add file1.txt
git commit -m "Initial content for file1"
```

Then you realize you **forgot to include `file2.txt`**, which is **also ready**.

---

### ❓What’s the **best and cleanest** way to include `file2.txt` in the same commit, **without creating a second commit**?

**A.** `git add file2.txt && git commit -m "Initial content for both files"`
**B.** `git add file2.txt && git commit --amend`
**C.** `git add file2.txt && git commit`
**D.** `git add file2.txt && git merge`


