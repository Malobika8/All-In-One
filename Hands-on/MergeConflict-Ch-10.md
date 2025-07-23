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

