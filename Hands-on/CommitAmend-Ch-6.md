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

