# 🏛️ Git Remote Repository & Multi‑Machine Collaboration — Notes

---

## 1️⃣ Remote Repository (GitHub)

The **central source of truth**, hosted on GitHub.

Example URL:

```
https://github.com/<username>/myprojectrepo
```

Everyone **pushes to** and **pulls from** this single remote repository.

---

## 2️⃣ Local Repository — Machine 1

The Git repo stored on your first local laptop/PC/server.

Example path:

```
/home/ubuntu/project1
```

Example files:

```
index1.html
app.js
style.css
```

### 🔗 How Machine 1 connects to GitHub

| Method | Auth Type                   | Notes                                                |
| ------ | --------------------------- | ---------------------------------------------------- |
| HTTPS  | Personal Access Token (PAT) | Token replaces password                              |
| SSH    | Public + private key        | Add public key to GitHub → GitHub trusts the machine |

### 📤 Actions from Local Repo 1

```
git push   → uploads commits to GitHub
git pull   → downloads new changes from GitHub
```

---

## 3️⃣ Local Repository — Machine 2

Another device (or another developer) cloned the **same** GitHub repo.

Example path:

```
D:\git\myprojectrepo
```

Interact with GitHub in the **same way** as Machine 1:

```
git pull   → gets updates made from Machine 1
git push   → sends new updates to GitHub
```

---

## 🔄 4️⃣ Interaction Flow — Full Example

### 🧑‍💻 Developer 1 (Machine 1)

```
# modifies index1.html
git add .
git commit -m "updated homepage"
git push
```

Remote GitHub now contains the update.

### 🧑‍💻 Developer 2 (Machine 2)

```
git pull   # receives Developer 1 updates
```

Then Developer 2 makes new changes → and pushes:

```
git push
```

GitHub now holds **both developers' changes**.

---

## 🔐 Connection Types (Summary)

### 1️⃣ HTTPS + Personal Access Token (PAT)

* Easiest to set up
* Used like:

```
https://github.com/<username>/<repo>.git
```

### 2️⃣ SSH Keys — Most secure

```
ssh-keygen -t ed25519
```

Copy the generated `.pub` key to **GitHub → SSH Keys** section.

Clone using:

```
git@github.com:<username>/<repo>.git
```

---

## 🚀 Final Understanding

| Component              | Location | Role                                |
| ---------------------- | -------- | ----------------------------------- |
| Remote repo            | GitHub   | Central storage + collaboration hub |
| Local repo (Machine 1) | Device 1 | Makes changes and pushes/pulls      |
| Local repo (Machine 2) | Device 2 | Gets updates & contributes back     |

Developers collaborate by **pushing to GitHub** and **pulling from GitHub**.

---

# 🌐 Git Remote + GitHub Workflow (HTTPS + PAT)

A complete guide for connecting a local Git repo to GitHub using **HTTPS + Personal Access Token (PAT)**.

---

## ✅ 1. Add a Remote Repository

If a GitHub repo already exists, connect it to your local repo:

```bash
git remote add origin https://github.com/raviteja1108/myproject01.git
```

✔ Creates a connection named `origin`
✔ `origin` points to your GitHub repository URL

Check if the remote is added:

```bash
git remote -v
```

Example output:

```
origin  https://github.com/raviteja1108/myproject01.git (fetch)
origin  https://github.com/raviteja1108/myproject01.git (push)
```

---

## ✅ 2. First Push to GitHub (requires authentication)

```bash
git push origin master
```

Git now asks:

```
Username: 
```

👉 **Paste your Personal Access Token (PAT) here** — NOT your GitHub username.

```
Password:
```

👉 **Press Enter (leave empty)**

---

## 🔐 3. Creating a Personal Access Token (PAT)

Go to:

```
https://github.com/settings/tokens
```

➡ Click **Generate new token (classic)**
➡ Select scopes:

* ✔ `repo`
* ✔ `workflow`
* ✔ `read:user`

📌 Copy the token immediately — it won't be visible again.
🧠 PAT replaces your GitHub password for Git HTTPS operations.

> 🔥 GitHub removed password authentication — PAT is mandatory.

---

## ✅ 4. Remove an Incorrect Remote

If wrong URL was added:

```bash
git remote rm origin
```

Add the correct one again:

```bash
git remote add origin https://github.com/raviteja1108/myproject01.git
```

---

## ✅ 5. First Push With Upstream Tracking

If pushing `master` for the first time:

```bash
git push --set-upstream origin master
```

OR shorter:

```bash
git push -u origin master
```

✔ Sets `origin/master` as the upstream tracking branch → future pushes become:

```bash
git push
git pull
```

### 🧠 What is "Upstream"?

Local `master` now automatically tracks `origin/master`. Git knows:

* Where to push
* Where to pull
* How to compare branches & histories

---

## 🔄 Full Real Example (Complete Flow)

```bash
git init

git add .
git commit -m "first commit"

git remote add origin https://github.com/raviteja1108/myproject01.git

git remote -v

git push -u origin master
```

During push:

```
Username: <paste PAT>
Password: <press Enter>
```

✔ Push succeeds
✔ Token is cached — next pushes won't ask again

---

## 🧹 Optional — Reset Remote if URL Is Wrong

```bash
git remote rm origin
```

```bash
git remote add origin https://github.com/raviteja1108/myproject01.git
```

---

## 📝 Commands Summary Table

| Command                       | Explanation                        |
| ----------------------------- | ---------------------------------- |
| `git remote add origin <URL>` | Connect local repo → GitHub remote |
| `git remote -v`               | Show remote URLs                   |
| `git push origin master`      | Push code using HTTPS + PAT        |
| `git push -u origin master`   | Set upstream tracking branch       |
| `git remote rm origin`        | Remove remote                      |
| `github.com/settings/tokens`  | Create PAT                         |
| **PAT → Username field**      | Used as authentication             |
| **Password field**            | Leave empty                        |

---

# 🚀 Password‑less Git Push using SSH Authentication (GitHub)

With **SSH authentication**, GitHub does **not** ask for username or Personal Access Token (PAT).
Your machine authenticates automatically using the **private key stored locally**.

---

## ✅ 1. Add Remote Repository Using SSH URL

Instead of HTTPS, use SSH:

```bash
git remote add origin git@github.com:raviteja1108/myproject01.git
```

Verify:

```bash
git remote -v
```

Output:

```
origin  git@github.com:raviteja1108/myproject01.git (fetch)
origin  git@github.com:raviteja1108/myproject01.git (push)
```

---

## ✅ 2. Generate SSH Key Pair

Run on EC2 / local machine:

```bash
ssh-keygen -t rsa -b 4096 -C "raviteja@example.com"
```

When asked:

```
Enter file in which to save the key (~/.ssh/id_rsa):
```

➡ Press **Enter** (default path)

Next prompt:

```
Enter passphrase:
```

➡ Press **Enter** (empty) → **password‑less access**

Keys generated:

```
Private key → ~/.ssh/id_rsa
Public key  → ~/.ssh/id_rsa.pub
```

🔴 **Never share the private key**

---

## ✅ 3. Copy Your Public Key

```bash
cat ~/.ssh/id_rsa.pub
```

Copy the full output starting with:

```
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQC...
```

---

## ✅ 4. Add SSH Key to GitHub

Go to:

```
GitHub → Settings → SSH and GPG keys → New SSH Key
```

* **Title:** EC2 key / Laptop key
* **Key:** paste the copied public key

🟢 Now GitHub **trusts your machine**.

---

## ✅ 5. Test SSH Connection

Run:

```bash
ssh -T git@github.com
```

Expected output:

```
Hi raviteja1108! You've successfully authenticated, but GitHub does not provide shell access.
```

➡ Means SSH authentication is working.

---

## ✅ 6. Push Code Password‑less

```bash
git push -u origin master
```

From now on:

```bash
git push
git pull
```

👉 No username or password will be asked.

---

## 🔁 Switching from HTTPS to SSH (if wrong remote added earlier)

Remove old remote:

```bash
git remote rm origin
```

Add SSH remote:

```bash
git remote add origin git@github.com:raviteja1108/myproject01.git
```

---


# 🚀 Git Fetch + Merge Only One File from Remote

---

## 🔥 1. What `git fetch` Does

`git fetch` downloads changes from the remote repository but **does NOT merge** them automatically.

```bash
git fetch origin
```

After this:

```
origin/master
origin/dev
origin/feature-1
```

These are **remote‑tracking branches** — read‑only references.
👉 Your **local working directory does NOT change** yet.

---

## 🔥 2. Scenario — Merge ONLY One File From Remote to Local

Suppose:

* You are on **local `master`**
* Remote (`origin/master`) has an updated file `index.html`
* You want **only that file**, not the whole branch

---

### ✔ Step 1 — Fetch latest from remote

```bash
git fetch origin
```

This updates the remote reference `origin/master`, but **does not affect your local files**.

---

### ✔ Step 2 — Checkout only one file from remote

```bash
git checkout origin/master -- index.html
```

This brings only `index.html` from `origin/master` into your working directory.

🔹 No branch switch
🔹 No merge
🔹 Only that one file is updated in working directory

⚠️ Note: the file is present but **not yet committed**.

---

### ✔ Step 3 — Stage and commit the file

```bash
git add index.html
git commit -m "Merged index.html from origin/master"
```

This finalizes the one‑file merge into local history.

---

## 🎯 Why Use This Technique?

Useful when:

* You want only **one specific file from remote**
* You don't want to merge/pull the entire branch
* You want to **avoid conflicts in unrelated files**

Perfect for:
✔ Hotfixing
✔ Updating only documentation
✔ Syncing selective config files

---

## 🔁 Full Command Sequence

```
git fetch origin
git checkout origin/master -- index.html
git add index.html
git commit -m "Merged index.html from origin/master"
```

---

## 📝 More Useful Variations

| Action                            | Command                                                     |
| --------------------------------- | ----------------------------------------------------------- |
| Checkout multiple files           | `git checkout origin/master -- index.html style.css app.js` |
| Checkout a full folder            | `git checkout origin/master -- static/`                     |
| Checkout file from another branch | `git checkout feature/login -- login.html`                  |
| Restore file from older commit    | `git checkout <commit-id> -- index.html`                    |

---

### 💡 Tip

To see differences before checkout:

```bash
git diff origin/master index.html
```

---

If you'd like, I can also add:

* Version of this method using **`git restore`** (new command)
* Comparison between **`git fetch` vs `git pull`**
* A workflow diagram for your documentation


# GitHub Organization

## What Is a GitHub Organization?

A GitHub Organization is a shared workspace where multiple people can
collaborate on repositories with controlled access and permissions.

## Key Features

-   Centralized repository management
-   Team-based permissions
-   Enhanced security and audit logs

## How to Create an Organization

1.  Go to GitHub Settings → Organizations → New Organization.
2.  Choose the plan (Free/Team/Enterprise).
3.  Provide an organization name.
4.  Complete setup.

## Add Members

Navigate to: Organization → People → Invite Member.

## Roles

-   **Owner**: Full administrative control.
-   **Member**: Standard permissions.

## Teams & Permissions

  Team          Permission   Description
  ------------- ------------ --------------------
  dev-team      Write        Developer commits
  qa-team       Read         Testing only
  devops-team   Maintain     CI/CD & operations
  admin-team    Admin        Manage settings

## Create Repositories in an Organization

When creating a repo, choose your organization as the **Owner**

## SSH/HTTPS Access

HTTPS:

    https://github.com/org-name/repo.git

SSH:

    git@github.com:org-name/repo.git