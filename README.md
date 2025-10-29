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


## To Visualize the Git

follow this link -   <http://git-school.github.io/visualizing-git/>
