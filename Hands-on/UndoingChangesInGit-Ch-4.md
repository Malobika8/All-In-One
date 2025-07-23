# Undoing Changes in Git

### 1️⃣ Unstaging a file

You added a file to the staging area using `git add`, but want to remove it from staging (not delete the file).

```bash
git reset <file>
```

✅ This removes the file from **staging area**, but **keeps your changes** in the file.

---

### 2️⃣ Discarding changes in a file (restore to last commit)

```bash
git restore <file>
```

> ⚠️ This **discards all changes** in the working directory for that file.

---

### 3️⃣ Undoing a commit (but keeping changes)

```bash
git reset --soft HEAD~1
```

* Removes the **last commit**, but **keeps changes staged**.

---

### 4️⃣ Undoing a commit (unstage the changes too)

```bash
git reset --mixed HEAD~1
```

* Removes last commit and **unstages** changes (but **keeps the code**).

---

### 5️⃣ Undoing a commit and code (dangerous)

```bash
git reset --hard HEAD~1
```

* Removes the last commit **and the code changes**.
* Use carefully!

---

### ✍️ Practice Task

1. Create a new Git repo: `git init`
2. Create a file `test.txt` with content.
3. `git add` and `git commit` it.
4. Modify `test.txt` and explore:

   * `git status`
   * `git restore test.txt`
   * `git reset` after staging
   * `git reset --soft HEAD~1`
   * `git reset --hard HEAD~1` (carefully)

---

