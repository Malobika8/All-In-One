## 🔄 Difference between `reset` vs `revert`

| Feature                        | `git reset`                                    | `git revert`                            |
| ------------------------------ | ---------------------------------------------- | --------------------------------------- |
| **Purpose**                    | Move branch pointer (undo commits)             | Create a new commit that undoes changes |
| **Destructive?**               | ✅ Yes (can delete history & changes)           | ❌ No (safe and reversible)              |
| **Used for?**                  | Local undo, rewriting history                  | Undoing public commits                  |
| **Affects working directory?** | Yes (depends on `--soft`, `--mixed`, `--hard`) | No (keeps history, makes new commit)    |
| **Safe for shared branches?**  | ❌ No                                           | ✅ Yes                                   |
| **Example usage**              | `git reset --hard HEAD~1`                      | `git revert HEAD`                       |

---

### 🔁 In simpler terms:

* `reset` **moves the branch pointer** back in time.
* `revert` **adds a new commit** that cancels the effect of a previous commit.

---

### ✅ When to use:

* Use `reset` when working **alone** or in a **local branch**.
* Use `revert` when the commit has been **pushed** and shared — safe for teams.

---

## 🧠 Git Reset vs Revert – Scenario Based Question:

You are working in a **shared Git repository** with your team.
You accidentally committed and pushed a commit that **broke the production build**.

Here is the commit history on `main`:

```
HEAD -> main
⬆️  e7f9abc  ❌ Added buggy logic
⬆️  a1b2c3d  ✅ Refactored user service
⬆️  d4e5f6g  ✅ Initial setup
```

You now want to **undo the buggy commit**, but other teammates have already pulled this code.

### ❓Which of the following is the **safest** way to fix this on a shared branch?

**A.** `git reset --hard HEAD~1`
**B.** `git reset --soft HEAD~1`
**C.** `git revert HEAD`
**D.** `git commit --amend`

### `git revert HEAD` is **the right and safest choice** for shared/public branches.

---

### 🔍 Why?

* `git revert HEAD` creates a **new commit** that undoes the changes from the last commit.
* It **doesn't rewrite history**, so your teammates won’t face conflicts or broken references.
* Perfect for fixing mistakes **after pushing**.

---

### 🔥 Why *not* the others?

| Option                    | Why not?                                                                                     |
| ------------------------- | -------------------------------------------------------------------------------------------- |
| `git reset --hard HEAD~1` | ❌ Rewrites history. Dangerous if others have pulled — leads to conflicts.                    |
| `git reset --soft HEAD~1` | ❌ Also rewrites history. Just keeps changes staged. Not safe for shared branches.            |
| `git commit --amend`      | ❌ Only edits the last commit’s message or content. Doesn’t **remove** it or fix pushed bugs. |

---

## 🧠 Scenario-Based Question – Reset vs Revert

You are on the `main` branch and just committed some sensitive test credentials **by mistake** 😨.
The commit has **already been pushed** to the remote repository, and your teammates may have pulled it.

Here’s your commit history:

```
HEAD -> main
⬆️  abcd123  ❌ Added dummy login credentials
⬆️  89ef456  ✅ Refactored error handler
⬆️  67bc789  ✅ Initial commit
```

---

### ❓What is the **safest** way to undo the sensitive commit **without breaking others’ work**?

**A.** `git reset --hard HEAD~1`
**B.** `git reset --soft HEAD~1`
**C.** `git revert HEAD`
**D.** Delete the repo and re-clone

---

## 🧠 Scenario: Local Commit, But Not Yet Pushed

You're working on a new feature locally. You’ve made 3 commits in a row like this:

```
HEAD -> main
⬆️  e3c1d2f  ❌ Added temporary debug print statements
⬆️  a7b4e6c  ✅ Finished feature logic
⬆️  f6a2d3b  ✅ Set up feature skeleton
```

You realize:

> The top commit (debug prints) was just for testing and should not be part of history at all.

You haven’t pushed **anything** to the remote yet.

### ❓What’s the cleanest way to remove the last commit **completely**, including code?

**A.** `git reset --soft HEAD~1`
**B.** `git reset --hard HEAD~1`
**C.** `git revert HEAD`
**D.** `git commit --amend`

