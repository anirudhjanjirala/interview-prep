# **GIT (FULL NOTES + DIAGRAMS + COMMANDS + INTERVIEW Q&A)**

---

# #️⃣ **3. GIT — COMPLETE NOTES**

---

# 🧠 **3.1 What is Git? (Very Simple)**

Git is a:

* **Distributed Version Control System (DVCS)**
* Tracks changes in files (mainly code)
* Allows team members to collaborate without overwriting work
* Stores complete history of the project locally

---

# 🏛 **3.2 Git Architecture (Diagram)**

Git works with **3 major areas**:

```
                +-----------------------------+
                |      Remote Repository      |
                | (GitHub, GitLab, Bitbucket) |
                +--------------+--------------+
                               ^
                               | push / pull
                               |
+----------------+             |
|  Working Dir   | -- add -->  v
| (Your Files)   |         +-----------+
+--------+-------+         | Staging   |
         ^                 |   Area    |
         |                 +-----+-----+
         |                       |
         |                       v
         |                +-------------+
         +---- checkout --|  Local Repo |
                          | (Commits)   |
                          +-------------+
```

---

# 🔁 **3.3 Basic Git Workflow Diagram**

```
Write Code
   ↓
git add
   ↓
git commit
   ↓
git push
```

---

# 📦 **3.4 Git Components Explained**

### ✔ **1. Working Directory**

The place where you modify files.

### ✔ **2. Staging Area**

Temporary area before commit.

### ✔ **3. Local Repository**

Stores committed snapshots permanently.

### ✔ **4. Remote Repository**

Hosted on GitHub, GitLab, etc.

---

# 🔀 **3.5 Branching Diagram**

```
master/main: ---A---B---C----------------
                   \
feature/login:       D---E---F
```

Branches allow multiple people to work safely without affecting main code.

---

# 🔍 **3.6 HEAD Pointer (Diagram)**

```
HEAD → points to current branch

HEAD → main
HEAD → feature/login
```

---

# 🧪 **3.7 Git Commands (With Explanation, Use Case & Output)**

Below are the **most important 50 Git commands** (you will realistically be asked these in interviews).

---

## 🔹 **1. git init – Create Git repo**

```bash
git init
```

Output:

```
Initialized empty Git repository in /project/.git/
```

---

## 🔹 **2. git clone – Download repo**

```bash
git clone https://github.com/user/project.git
```

Output:

```
Cloning into 'project'...
```

---

## 🔹 **3. git status – Check status**

```bash
git status
```

Output:

```
modified: app.py
untracked: test.txt
```

---

## 🔹 **4. git add – Stage file**

```bash
git add app.py
```

Or stage everything:

```bash
git add .
```

---

## 🔹 **5. git commit – Save changes**

```bash
git commit -m "Fixed bug in login"
```

---

## 🔹 **6. git log – View commit history**

```bash
git log --oneline
```

Output:

```
f23ab12 Fix login bug
a223596 Initial commit
```

---

## 🔹 **7. git branch – List branches**

```bash
git branch
```

---

## 🔹 **8. git branch newbranch – Create branch**

```bash
git branch feature-login
```

---

## 🔹 **9. git checkout – Switch branch**

```bash
git checkout feature-login
```

---

## 🔹 **10. git switch – New modern command**

```bash
git switch -c feature-login
```

---

## 🔹 **11. git merge – Merge branches**

```bash
git merge feature-login
```

---

## 🔹 **12. git pull – Fetch + merge**

```bash
git pull origin main
```

---

## 🔹 **13. git fetch – Fetch only**

```bash
git fetch origin
```

---

## 🔹 **14. git push – Upload commits**

```bash
git push origin main
```

---

## 🔹 **15. git remote – View remote repos**

```bash
git remote -v
```

---

## 🔹 **16. git diff – Show differences**

```bash
git diff
```

---

## 🔹 **17. git stash – Save uncommitted work**

```bash
git stash
```

Output:

```
Saved working directory and index state
```

Retrieve:

```bash
git stash pop
```

---

## 🔹 **18. git revert – Undo commit without deleting**

```bash
git revert <commit-id>
```

---

## 🔹 **19. git reset – Undo and remove commits**

Soft:

```bash
git reset --soft HEAD~1
```

Hard:

```bash
git reset --hard HEAD~1
```

⚠ Deletes commit history!

---

## 🔹 **20. git cherry-pick – Apply specific commit**

```bash
git cherry-pick <commit-id>
```

---

## 🔹 **21. git rm – Remove file from repo**

```bash
git rm file.txt
```

---

## 🔹 **22. git tag – Create tag**

```bash
git tag v1.0
```

---

## 🔹 **23. git blame – Show who modified each line**

```bash
git blame app.py
```

---

## 🔹 **24. git show – Show commit details**

```bash
git show <commit-id>
```

---

## 🔹 **25. git clean – Remove untracked files**

```bash
git clean -f
```

---

# 🧩 **3.8 Merge vs Rebase (Diagram + Explanation)**

## **Merge Diagram**

```
main:    A---B-------E
                \    
feature:         C---D
```

After merge:

```
main: A---B---E
             \  
              C---D (merge commit)
```

## **Rebase Diagram**

```
main:    A---B---E
feature:         C'--D'
```

**Simpler history**, but rewrites commits.

---

# ⚠️ **3.9 Merge Conflict Example**

### Command:

```bash
git merge feature1
```

### Conflict message:

```
CONFLICT (content): Merge conflict in index.html
```

### File looks like:

```
<<<<<< HEAD
<h1>Version A</h1>
======
<h1>Version B</h1>
>>>>>> feature1
```

### Fix manually → then:

```bash
git add index.html
git commit
```

---

# 📝 **3.10 10 Git Interview Questions (With Easy Answers)**

---

## **Q1. What is Git and how is it different from other VCS?**

Git is a **distributed version control system**.
Every developer has a full copy of repository.

**Difference:**

| Feature | Git         | SVN         |
| ------- | ----------- | ----------- |
| Type    | Distributed | Centralized |
| Offline | Yes         | No          |
| Speed   | Fast        | Slow        |

---

## **Q2. Explain basic Git workflow.**

```
Modify files → git add → git commit → git push
```

---

## **Q3. How to create a branch?**

```bash
git branch feature-xyz
git checkout feature-xyz
```

OR:

```bash
git switch -c feature-xyz
```

---

## **Q4. Difference between git pull and git fetch?**

| Command     | Meaning                |
| ----------- | ---------------------- |
| `git fetch` | Only downloads changes |
| `git pull`  | fetch + merge          |

---

## **Q5. What is merge conflict and how to resolve it?**

When two people change the **same part** of a file.

Steps:

1. Open file → resolve conflict manually
2. Add file:

```bash
git add file.txt
```

3. Commit:

```bash
git commit
```

---

## **Q6. git merge vs git rebase**

| Feature                | Merge                | Rebase           |
| ---------------------- | -------------------- | ---------------- |
| History                | Keeps history        | Rewrites history |
| Commit type            | Creates merge commit | Linear commits   |
| Safe for shared branch | Yes                  | No               |

---

## **Q7. How to undo commit?**

Safe:

```bash
git revert <id>
```

Dangerous:

```bash
git reset --hard <id>
```

---

## **Q8. What is git stash?**

Used to **save temporary changes** without committing.

Store:

```bash
git stash
```

Retrieve:

```bash
git stash pop
```

---

## **Q9. What is cherry-pick?**

Applies specific commit from one branch to another:

```bash
git cherry-pick <commit>
```

---

## **Q10. How to view commit history?**

```bash
git log --oneline --graph --all
```

---

# 🎉 **SECTION 3 COMPLETED**

Next section:

# 👉 **SECTION 4 — JENKINS (Full Notes + Pipelines + Diagrams + Commands + Interview Q&A)**

Reply **Next** to continue.
