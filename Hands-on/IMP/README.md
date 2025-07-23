# ✅ Git `origin` vs `origin/main` – Cheat Sheet

| Command                                       | ✅ Correct Usage            | ❌ Incorrect Usage       | Explanation                                       |
| --------------------------------------------- | -------------------------- | ----------------------- | ------------------------------------------------- |
| **Pull latest from remote**                   | `git pull origin main`     | `git pull origin/main`  | `origin` is the remote name, `main` is the branch |
| **Push to remote**                            | `git push origin main`     | `git push origin/main`  | Push `main` to remote `origin`                    |
| **Fetch all branches**                        | `git fetch origin`         | `git fetch origin/main` | `origin` is a remote, not a branch                |
| **View remote branch logs**                   | `git log origin/main`      | —                       | View commit history of remote-tracking branch     |
| **Compare remote vs local**                   | `git diff origin/main`     | —                       | Compare current branch to remote-tracking branch  |
| **Rebase onto remote branch**                 | `git rebase origin/main`   | —                       | Reapply your changes on top of `origin/main`      |
| **Check out a remote branch (detached HEAD)** | `git checkout origin/main` | —                       | Temporarily switch to the remote branch           |
| **Prune deleted remote branches**             | `git fetch --prune origin` | —                       | Cleans up remote-tracking branches                |

---

## 🧠 Conceptual Summary

| Term          | Meaning                                              |
| ------------- | ---------------------------------------------------- |
| `origin`      | Name of the remote (default when you clone)          |
| `main`        | Branch name                                          |
| `origin/main` | Local copy (remote-tracking ref) of `main` on GitHub |

---

### 💡 Tips

* Always use **`origin main`** (with space) in **push/pull/fetch**
* Use **`origin/main`** (with slash) for **viewing, rebasing, comparing**

---

