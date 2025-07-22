## ✅ **`.gitignore` – Ignore Unwanted Files**

Sometimes, you don’t want to track all files — like:

* `.class`, `.log`, `.env`, `node_modules`, etc.
* Sensitive data or temporary files

### 🔧 1. Create a file to ignore

```bash
echo "temp.txt" > temp.txt
echo "Don't track this" >> temp.txt
```

Now check:

```bash
git status
```

You’ll see `temp.txt` is untracked.

---

### 🚫 2. Tell Git to ignore it using `.gitignore`

```bash
echo "temp.txt" > .gitignore
git add .gitignore
git commit -m "Add .gitignore to ignore temp.txt"
```

Now run `git status`.
You'll see: **`temp.txt` is no longer shown**. Git will **ignore it forever** (until removed from `.gitignore`).

✅ This is how you prevent Git from tracking certain files.

---

## ✅ **Deleting and Restoring Files**

Let’s delete a file and see what happens.

### 🗑️ 1. Delete a tracked file

```bash
rm hello.txt
git status
```

Git will show: `deleted: hello.txt`

### ✅ 2. Stage and commit the deletion

```bash
git add hello.txt
git commit -m "Deleted hello.txt"
```

> Now Git has recorded the deletion.

---

### ♻️ 3. What if you deleted by mistake?

Let’s try again and **restore without committing**.

```bash
echo "Test content" > sample.txt
git add sample.txt
git commit -m "Added sample.txt"
rm sample.txt
git status
```

You’ll see it's deleted.

To restore it before committing:

```bash
git restore sample.txt
```

Now it comes back. 🎉

---

## ✅ **View and Undo Changes (Before Commit)**

### 📝 Modify a file

```bash
echo "Another line" >> sample.txt
```

Now run:

```bash
git diff
```

You'll see the changes.

To undo the changes before staging:

```bash
git restore sample.txt
```

---

## ✅ Summary So Far

| Task                        | Git Command                   |
| --------------------------- | ----------------------------- |
| Ignore a file               | `.gitignore` + `git add`      |
| Delete file from Git        | `rm`, `git add`, `git commit` |
| Restore deleted file        | `git restore <file>`          |
| View uncommitted changes    | `git diff`                    |
| Discard uncommitted changes | `git restore <file>`          |

---


