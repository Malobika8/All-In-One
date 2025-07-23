# ⚔️ Git Merge Conflicts – Step by Step

## ✅ What is a Merge Conflict?

A **merge conflict** happens when:

* Two branches have changes to the **same part of the same file**
* Git **cannot auto-merge**, so it asks **you** to decide

---

## 🔁 When Do Merge Conflicts Happen?

Most commonly during:

* `git merge`
* `git pull` (which is fetch + merge)
* `git rebase`
* `git cherry-pick`

---

## 🎯 Example Scenario:

Let’s say you and your teammate both edit the same line in `main.java`:

### In `main` branch:

```java
System.out.println("Welcome!");
```

### In `feature` branch:

```java
System.out.println("Hello!");
```

Now if you try to merge `feature` into `main`, Git throws a conflict.

---

## 🧨 What Git Does:

It marks the conflict like this inside the file:

```java
<<<<<<< HEAD
System.out.println("Welcome!");
=======
System.out.println("Hello!");
>>>>>>> feature
```

* `<<<<<<< HEAD` → your current branch’s version
* `=======` → separator
* `>>>>>>> feature` → incoming changes

---

## 🛠️ How to Resolve:

### 1. Open the conflicted file(s)

### 2. Manually edit to choose or combine the changes:

Example:

```java
System.out.println("Welcome, Hello!");
```

### 3. Then stage it again:

```bash
git add main.java
```

### 4. Complete the merge:

```bash
git commit
```

Or if the conflict happened during a pull:

```bash
git pull --continue
```

---

# ✅ Summary & FAQ

## 🔁 1. What is `git merge`?

* Combines changes from one branch (e.g., `feature`) into another (e.g., `main`)
* Keeps the commit history of **both** branches
* Usually results in a **merge commit**, unless it's a **fast-forward**

---

## ⚙️ 2. How to Perform a Merge

```bash
git checkout main
git merge feature-branch
```

---

## 🔀 3. Merge Commit vs Fast-Forward

### ✅ Merge Commit:

Occurs when `main` has its own commits and `feature-branch` also has commits.

```
A---B---C---M     ← main (after merge)
     \     /
      D---E       ← feature-branch
```

* A new commit `M` is created to "tie" both lines together

### ✅ Fast-forward Merge:

Occurs when `main` hasn’t changed since `feature-branch` was created.

```
main:
A---B---C

feature:
A---B---C---D---E

# After merge:
main:
A---B---C---D---E
```

* No merge commit created
* `main` just "fast-forwards" to `feature-branch`’s tip

---

## ⚔️ 4. Merge Conflicts

### When?

* Two branches modify the **same lines** in a file

### What to do:

1. Git marks the conflict with `<<<<<<<`, `=======`, `>>>>>>>`
2. Manually fix the conflict
3. Stage the resolved file: `git add <file>`
4. Complete the merge: `git commit`

---

## 🧹 5. After Merge — Local vs Remote

### ❗ Important Notes:

* `git merge` only affects your **local branch**
* You must **push manually**:

  ```bash
  git push origin main
  ```

### To delete the merged branch:

* Locally:

  ```bash
  git branch -d newbranch
  ```
* Remotely:

  ```bash
  git push origin --delete newbranch
  ```

---

## 🧠 6. Why You May See Merged Code in Other Branches

### Scenario:

* You modified a file in `feature-branch` but **didn’t commit**
* Then you switched to `main`
* The change appears in `main` too 😕

### Why?

> Git keeps **uncommitted changes** in your working directory across branch switches

### Fix:

* **Commit** before switching
* Or **stash**:

  ```bash
  git stash
  git checkout main
  git stash pop
  ```

---

## 🧪 7. Check Which Branches are Merged

```bash
git branch --merged main
```

---

## 🧼 8. Clean Up Local/Remote Branches After Merge

* Remove remote-tracking branches that no longer exist on remote:

  ```bash
  git fetch --prune
  ```
* Or:

  ```bash
  git remote prune origin
  ```

---

## 🔄 9. Visual Summary

### Merge:

✅ Keeps history of both branches
✅ Adds a **merge commit**

```
main:    A---B---C---M
                  \ /
          feature: D---E
```

---

## 🚫 Common Mistakes

| Mistake                                        | Explanation                                    | Fix                                           |
| ---------------------------------------------- | ---------------------------------------------- | --------------------------------------------- |
| See changes from feature in main               | You switched branches with uncommitted changes | Commit or stash first                         |
| Merge done locally, but not on GitHub          | You didn’t push the `main` branch after merge  | `git push origin main`                        |
| Branch deleted from GitHub, but still in local | Remote not cleaned yet                         | `git fetch --prune` or manually delete        |
| Conflict not resolved                          | Git won't let you commit                       | Manually fix, then `git add` and `git commit` |

---

