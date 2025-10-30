# Git

git is an open source, distributed version control system designed for speed and efficiency

git is a command line, GitHub is the web interface. GitHub is also a code hosting site, free for public repositories. Gitlab the open-source github, that enterprises can run on their own servers.
> git is basically working locally, but github is something working like globally.

# Version Control

* A system that keeps records of your changes.
* Allows for collaborative development.
* Allows yu to know who made what changes and when.
* Allows you to revert any changes.

Version Control:
    *CVS - Centralized
    * SVN - Centralized
    * GIT - Distributed

* **Fork** can create an entire copy of your Original Source

# 🧩 Git Concepts and Configuration Guide

## ① Working Directory
This is your current project folder where you create and modify files.

### Example files:
- index.html
- index2.html

You edit files here before tracking them with Git.

---

## ② Staging Area (Index)
A temporary space where Git keeps track of files you intend to commit.

### Command to add files:
```bash
git add index.html
git add .
```
It means: “Hey Git, I’m ready to save these changes!”

---

## ③ Local Repository (.git folder)
Located inside your project folder.

It stores committed versions of your files as snapshots.

### You create it with:
```bash
git init
```
Each commit is like a “save point” that you can revert to.

---

## 🔁 Flow Summary:
1. Create/modify files → **Working directory**
2. Stage files → `git add` → **Staging area**
3. Commit files → `git commit -m "message"` → **Local repository**

---

## 🧭 Git Configuration Levels
Git allows configuration at three levels — **system**, **global**, and **local**.

| Configuration Type | Location | Applies To | File |
|--------------------|-----------|-------------|------|
| System | Entire system (all users) | Every user & repo on that server | `/etc/gitconfig` |
| Global | Current user | All repos for that user | `~/.gitconfig` |
| Local | Current repository only | That one project | `<repo>/.git/config` |

---

## 🔧 Commands to Configure Git

### 1️⃣ System Configuration
```bash
sudo git config --system user.name "Raviteja"
sudo git config --system user.email "raviteja@example.com"
```
Affects all repositories and users on the system.  
Stored in `/etc/gitconfig`.

---

### 2️⃣ Global Configuration
```bash
git config --global user.name "Raviteja"
git config --global user.email "raviteja@example.com"
```
Applies to all repositories for your user account.  
Stored in `~/.gitconfig`.

To open or edit directly:
```bash
vim ~/.gitconfig
```

---

### 3️⃣ Local Configuration
```bash
git config --local user.name "Raviteja"
git config --local user.email "raviteja@example.com"
```
Applies only to the current repository.  
Stored in `.git/config` inside your repo folder.

---

## 🕵️ View Your Configuration
```bash
git config --list --show-origin
```
Displays where each setting comes from (system, global, or local).

---

## 🧮 Useful Git Commands

| Command | Description |
|----------|-------------|
| `git init` | Initializes a new Git repo |
| `git add <file>` | Adds file to staging area |
| `git commit -m "message"` | Saves staged files to local repo |
| `git status` | Shows tracked/untracked file status |
| `git ls-files` | Lists all files currently tracked by Git |
| `git log` | Shows commit history |
| `git config --list` | Shows configuration settings |

---

## 🗂 File Paths Recap

| File | Description |
|------|--------------|
| `/etc/gitconfig` | System-wide configuration |
| `~/.gitconfig` | User-level (global) configuration |
| `.git/config` | Repository-level (local) configuration |

---

## ✅ Quick Example
Here’s how a setup might look on your AWS EC2 Ubuntu server:

```bash
# Step 1: Initialize repo
git init

# Step 2: Set user details for this repo (local)
git config --local user.name "Raviteja"
git config --local user.email "raviteja@ec2.com"

# Step 3: Add files
git add index.html

# Step 4: Commit snapshot
git commit -m "First commit"

# Step 5: List tracked files
git ls-files
```




# installation & configuration

```console
$ git --version         # to check git is installed or not
$ git config --list     # previous configurations
$ git config --global user.name "gdagdg"
$ git config --global user.email "ks@visotech.com"
```

//Initializing a Repository in an Existing Directory

```console
$ touch hello-world.py             # create a file
$ git init                         # Initialize git in current directory
$ tree -a .git/objects             # show tree list of files
```

```console
$ ls -la                           # to view hidden files
$ ls .git                          # .git file is responsible for everything
```

```console
$ git add .                        # stage the changes
$ git status                       # Review your changes
$ git commit -m "initial version"   # commit the changes
$ git push                         # to push the changes
$ git branch -r                    # to view all the branches
$ git branch                       # shows a list of local branches
$ git branch branch_name           # to create a branch with a name   
$ git checkout branch_name         # to move to other branch
$ git merge branch_name            # to merge the branch
$ git branch -d branch_name        # to delete a branch
```

```console
$ git diff                         # to see the exact changes
$ git log                          # to see the commits 
$ git reset --hard commit_id       # versioning- going back to previous commit
$ git log --oneline                # to see previous commits
$ git checkout commit_id           # to go to that version
```

> master , Feature Branch, Release Branch  

* merge:
  * fast-forward merge

# 🧩 Advanced Git Commands — Detailed Guide with Scenarios

---

## 🧾 1️⃣ git log --oneline

Displays the commit history in a short, one-line format.

### 🧠 Why Use It:
- To quickly review recent commits.  
- To find short commit IDs for `git show`, `git diff`, or `git revert`.

### 🧩 Example:
```bash
git log --oneline
```

**Output:**
```
9f8e7b1 Update contact form validation
b13e3a0 Add CSS styling for footer
a3c45df Initial commit
```

💡 **Scenario:**  
You want to revert to an earlier version of your code.  
Instead of looking through long commit logs, `--oneline` gives you compact info to identify commit IDs easily.

---

## 🧾 2️⃣ git log --stat --oneline

Shows commit history plus file-level statistics (what changed, how many lines added or removed).

### 🧩 Example:
```bash
git log --stat --oneline
```

**Output:**
```
b13e3a0 Add CSS styling for footer
 style.css | 5 ++++-
 1 file changed, 4 insertions(+), 1 deletion(-)

a3c45df Initial commit
 index.html | 10 ++++++++++
```

💡 **Scenario:**  
You’re reviewing what your teammate changed last week and want to know which files were affected, without viewing actual code differences.

---

## 🧾 3️⃣ git show <commit-id>

Displays detailed information about a specific commit — including author, timestamp, message, and exact code changes.

### 🧩 Example:
```bash
git show b13e3a0
```

**Output:**
```
commit b13e3a0
Author: Raviteja <raviteja@example.com>
Date:   Thu Oct 30 14:21:33 2025 +0530

    Add CSS styling for footer

diff --git a/style.css b/style.css
+ footer {
+   background: black;
+   color: white;
+ }
```

💡 **Scenario:**  
You want to check what was added in a particular commit before merging it into the main branch.  
Use `git show` to verify the code content before approval.

---

## 🧾 4️⃣ git diff --name-only <commit1> <commit2>

Shows only filenames that differ between two commits — no code shown.

### 🧩 Example:
```bash
git diff --name-only a3c45df b13e3a0
```

**Output:**
```
index.html
style.css
```

💡 **Scenario:**  
You’re writing a deployment script and need to know which files changed between two releases — for example, to upload only modified files to your server.

---

## 🧾 5️⃣ git diff <commit1> <commit2>

Shows actual line-by-line differences between two commits.

### 🧩 Example:
```bash
git diff a3c45df b13e3a0
```

**Output:**
```diff
- <footer>Contact us</footer>
+ <footer>Contact us at support@example.com</footer>
```

💡 **Scenario:**  
You found a bug introduced recently. Use `git diff` to identify what exact code lines changed between the last working commit and the current one.

---

## 🧾 6️⃣ git rm index.html

Removes the file from both the working directory and Git tracking.

### 🧩 Example:
```bash
git rm index.html
git commit -m "Removed old homepage"
```

### 🧠 What Happens:
- File is deleted from your folder.  
- Deletion is staged for commit.  
- When committed, Git records the deletion.

💡 **Scenario:**  
You’ve replaced `index.html` with `home.html` and no longer want `index.html` in the repository.

---

## 🧾 7️⃣ git rm --cached <file>

Removes a file from tracking only, but keeps it on disk.

### 🧩 Example:
```bash
git rm --cached .env
git commit -m "Stop tracking .env file"
```

💡 **Scenario:**  
You accidentally committed sensitive credentials in `.env`.  
You want to keep the file locally but remove it from the Git history going forward.

Then, you’d add it to `.gitignore`:
```bash
echo ".env" >> .gitignore
```

---

## 8️⃣ `git revert <commit-id>`

### 🔍 Definition
`git revert` creates a **new commit** that undoes the changes introduced by a specific commit — without modifying history.

It’s **safe for shared repositories**, because it doesn’t rewrite or delete commit history.

### 🧠 How It Works
Imagine your repo history looks like this:
```
A → B → C → D (HEAD)
```
If commit **C** introduced a bug, you can revert it using:
```bash
git revert C
```
This will create a **new commit E** that undoes the changes from C:
```
A → B → C → D → E (HEAD)
```

### 💻 Example
```bash
git revert c8d1f42
```
You can revert multiple commits too:
```bash
git revert HEAD~3..HEAD
```

### ✅ When to Use
- To undo a bad commit in a **shared branch**
- To maintain **transparent history**
- When collaborating with others

### ⚠️ Notes
- Doesn’t delete commits — it **adds** a new one.
- Can be reverted again if needed.

---

## 9️⃣ `git reset --soft <commit-id>`

### 🔍 Definition
`git reset --soft` moves `HEAD` to a previous commit but **keeps all your changes staged** (in the index).

Useful for **combining commits** or **editing commit messages** before pushing.

### 🧠 How It Works
Example:
```
A → B → C → D (HEAD)
```
Run:
```bash
git reset --soft B
```
Now commits **C** and **D** are undone, but their changes are **still staged** and ready to recommit.

You can create a new clean commit:
```bash
git commit -m "Combined fixes from C and D"
```

### 💻 Example
```bash
git reset --soft HEAD~2
git commit -m "Squashed last two commits"
```

### ✅ When to Use
- To combine or rewrite recent commits
- Before pushing changes
- To adjust your commit message or grouping

### ⚠️ Notes
- Doesn’t delete work — everything stays staged.
- Safe only for **local changes** (not yet pushed).

---

## 3️⃣ `git reset --hard <commit-id>`

### 🔍 Definition
`git reset --hard` resets the `HEAD`, **index**, and **working directory** to a specific commit.

It **deletes all uncommitted changes** — both staged and unstaged.

### 🧠 How It Works
Example:
```
A → B → C → D (HEAD)
```
Run:
```bash
git reset --hard B
```
Now commits **C** and **D** are gone, and your working directory matches commit **B** exactly:
```
A → B (HEAD)
```

### 💻 Example
```bash
git reset --hard HEAD~2
```

### ✅ When to Use
- To completely discard local changes
- To return to a stable commit
- To fix a broken state or unwanted merges

### ⚠️ Notes
- **Dangerous:** deletes all local work permanently.
- Never use on **shared repositories** (others may lose commits).
- If unsure, stash first:
```bash
git stash
git reset --hard HEAD~1
git stash pop
```

---

## 🧩 Comparison Table

| Command | Changes History | Keeps Changes | Safe for Shared Repo | Use Case |
|----------|------------------|---------------|-----------------------|-----------|
| `git revert <commit>` | ❌ No | ✅ Yes | ✅ Yes | Safely undo a commit |
| `git reset --soft <commit>` | ✅ Yes | ✅ Staged | ⚠️ Only local | Combine commits |
| `git reset --hard <commit>` | ✅ Yes | ❌ No | ❌ No | Discard all changes |

---

## 🧭 Practical Example

Repo state:
```
A → B → C → D (HEAD)
```

### 🧩 Case 1: Undo a commit safely
```bash
git revert C
```
Result:
```
A → B → C → D → E (HEAD)
```
(E is the inverse of C)

---

### 🧩 Case 2: Combine commits before push
```bash
git reset --soft B
git commit -m "Clean combined commit"
```
Result:
```
A → B → E (HEAD)
```

---

### 🧩 Case 3: Start over cleanly
```bash
git reset --hard B
```
Result:
```
A → B (HEAD)
```

---

## ✅ Best Practices

| Situation | Recommended Command |
|------------|--------------------|
| Undo bad commit safely | `git revert` |
| Combine commits locally | `git reset --soft` |
| Wipe everything and restart | `git reset --hard` |
| Unsure or shared repo | Always use `git revert` |

---

## 🧠 Summary

- **`revert`** → Safe, creates a new commit that undoes previous changes.  
- **`reset --soft`** → Moves HEAD back, keeps staged changes.  
- **`reset --hard`** → Moves HEAD back and deletes all changes.

---

🧑‍💻 **Pro Tip:** Before using reset or revert, always check:
```bash
git log --oneline
git status
```



## To Visualize the Git

follow this link -   <http://git-school.github.io/visualizing-git/>
