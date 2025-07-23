## 🔁 What is Git Rebase?

### 📖 Definition (Simple):

`git rebase` moves or **re-applies commits** from one branch **on top of another**, as if the work happened later.

Think of it as:

> “Replay my changes as if I started from a newer base.”

---

## 🔍 Why Use Rebase?

To create a **clean, linear history** — especially useful when collaborating.

Without rebase:

```
*---*---*---*      ← main
     \
      *---*---*    ← feature
```

With rebase:

```
*---*---*---*---*---*    ← feature (after rebase onto main)
```

No merge commits. Just a straight line of history.

---

## 🤯 Merge vs Rebase – Core Difference:

| Operation                      | What it does                          | History                                               |
| ------------------------------ | ------------------------------------- | ----------------------------------------------------- |
| `git merge main` (on feature)  | Combines histories                    | Keeps both branch histories + adds a **merge commit** |
| `git rebase main` (on feature) | Replays your commits on top of `main` | Linear, cleaner history                               |

---

## 🔧 Rebase in Action – Example

You start with:

```
main:
A -- B -- C

feature:
A -- B -- C
           \
            D -- E
```

You run:

```bash
git checkout feature
git rebase main
```

Rebase moves commits `D` and `E` **on top of `main`** (which is at `C`):

Result:

```
main:
A -- B -- C

feature (rebased):
A -- B -- C -- D' -- E'
```

> `D'` and `E'` are **new commits** (rewritten versions of `D` and `E`)

---

## 🔁 Why Would You Use Rebase?

* To avoid messy history with lots of merges
* To make pull requests easier to read
* To update your feature branch with the latest from `main` **without a merge commit**

---

## ⚠️ When *NOT* to Use Rebase

> **Never rebase a branch that you’ve already pushed and shared**
> It rewrites history, and can cause big problems for others.

✅ Use rebase for local-only branches
🚫 Don’t rebase shared public branches

---

