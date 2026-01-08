# 🚀 GitHub Actions — Complete Notes (Beginner to Advanced)

This document explains **GitHub Actions** clearly, with corrected concepts, structured notes, and a **fully commented workflow example using `#` comments inside the YAML itself**.

---

## 🔰 What is GitHub Actions?

**GitHub Actions** is an **open-source CI/CD platform** provided directly by GitHub.

### Key Characteristics

* No installation required
* Built directly into GitHub repositories
* No separate UI (uses GitHub Actions tab)
* Used to create **CI/CD pipelines**, called **workflows**
* Workflows are written in **YAML**
* Authentication handled automatically via GitHub account

📌 GitHub Actions works **only with GitHub repositories**.

---

## 🎯 Why GitHub Actions?

* Create CI/CD pipelines without external tools
* No need to manage servers or agents
* GitHub provides **ready-to-use runners (VMs)**
* Simple YAML syntax
* Tight integration with GitHub (PRs, issues, commits)

---

## 🧩 GitHub Actions Terminology

### 1️⃣ Workflow

A **workflow** is an automated process that:

* Runs one or more jobs
* Is triggered by GitHub events
* Is defined in a YAML file

📌 Workflow files are stored at:

```
.github/workflows/*.yml
```

---

### 2️⃣ Events (Triggers)

Events define **when a workflow should run**.

Examples:

* Push to a branch
* Pull request creation
* Merge request
* Schedule (cron)
* Manual trigger
* Workflow-to-workflow trigger

---

### 3️⃣ Jobs

* A workflow can have **multiple jobs**
* Jobs run **in parallel by default**
* Each job:

  * Runs on a runner
  * Contains steps

📌 Jobs can be made sequential using `needs:`.

---

### 4️⃣ Runner (Dynamic Agent)

A **runner** is a temporary VM where jobs execute.

#### GitHub-Hosted Runners

* Managed by GitHub
* Automatically provisioned
* Automatically destroyed after job completion
* Runs on **Azure infrastructure**

Supported OS:

* Ubuntu (Linux)
* Windows
* macOS

#### Self-Hosted Runners

* Your own VM or server
* Persistent
* Managed by you

---

### 5️⃣ Steps

* A job consists of multiple steps
* Each step:

  * Runs a command OR
  * Uses an action

Steps can:

* Use scripts
* Use conditions
* Use environment variables
* Upload/download artifacts

---

## 🔄 Execution Flow

```
Workflow
  ↓
Job(s)
  ↓
Runner (VM)
  ↓
Steps
```

---

## 📘 YAML Basics (Corrected & Explained)

YAML is:

* Declarative (not programming)
* Key–value based
* Indentation-sensitive

### Comments in YAML

```yaml
# This is a comment
```

---

### Example 1️⃣ Key with Single Value

```yaml
Company: Demo
Trainer: Sonal Mittal
Training: DevOps
Day: Weekday
Time: 7AM
```

---

### Example 2️⃣ Key with List of Values

```yaml
Company: Demo
Trainers:
  - Sonal Mittal
  - Ravi
  - Marc
  - Jack
Trainings:
  - DevOps
  - AWS
  - MLOps
  - GCP
```

---

### Example 3️⃣ Key with Map (List of Objects)

```yaml
Company: Demo
Trainers:
  - name: Sonal
    phone: 35345646
    email: sonal@example.com
  - name: Ravi
    phone: 35436456
    email: ravi@example.com
```

---

## 🏗️ GitHub Actions Workflow Structure

```yaml
# Name of the workflow
name: Demo Workflow

# Events that trigger the workflow
on:
  push:
  workflow_dispatch:  # Manual trigger

# Jobs section (required)
jobs:
  job1:
    runs-on: ubuntu-latest
    steps:
      - name: Step 1
        run: echo "Hello from Job 1"
```

---

## 🔑 Workflow-Level Keys (Top Level)

These keys are defined at the **root of the workflow file**.

```yaml
name:          # Optional name of the workflow shown in Actions UI
run-name:     # Dynamic name shown per run
on:           # Events that trigger the workflow
permissions:  # Permissions for GITHUB_TOKEN
defaults:     # Default settings (e.g., shell, working directory)
env:          # Environment variables (global)
concurrency:  # Workflow concurrency control
jobs:         # Job definitions (REQUIRED)
```

---

## ⚡ Event Trigger Keys (`on:`)

The `on` key defines **when the workflow should run**.

```yaml
on:
  push:              # Trigger on git push
  pull_request:      # Trigger on pull request
  schedule:          # Cron-based scheduling
  workflow_dispatch: # Manual trigger (Run workflow button)
  workflow_call:     # Reusable workflows
  issues:            # Issue events
  repository_dispatch: # External webhook trigger
  check_run:         # Check run events
  release:           # Release events
  # ...over 50 supported GitHub events
```

📌 Multiple events can be combined in the same workflow.

---

## 🧱 Job-Level Keys (`jobs.<job_id>`)

Each job is defined under the `jobs` section.

```yaml
jobs:
  my_job:
    name:         # Optional job name shown in UI
    needs:        # Job dependencies (sequential execution)
    runs-on:      # Runner type (e.g., ubuntu-latest)
    environment:  # Environment context
    permissions:  # Job-level permissions
    concurrency:  # Job concurrency control
    outputs:      # Define outputs to share with other jobs
    if:           # Conditional execution
    strategy:     # Matrix strategy
    container:    # Docker container to run the job
    services:     # Service containers (DB, cache, etc.)
    defaults:     # Default runner options
    steps:        # List of steps to execute
```

---

## 🔁 Matrix Strategy Keys (`strategy:`)

Used to run the same job with **multiple configurations**.

```yaml
strategy:
  matrix:        # Define matrix combinations
  fail-fast:     # Stop all jobs if one fails
  max-parallel:  # Limit parallel job runs
```

📌 Common use cases:

* Multiple OS versions
* Multiple language/runtime versions

---

## 🧩 Step-Level Keys (`jobs.<job_id>.steps[]`)

Each job contains one or more steps.

```yaml
- name:              # Name shown in Actions UI
  id:                # Step ID for referencing outputs
  run:               # Shell command to execute
  uses:              # Action to use
  with:              # Inputs for the action
  env:               # Step-level environment variables
  if:                # Conditional execution
  working-directory: # Directory to run the command
  shell:             # Shell to use
  timeout-minutes:   # Timeout for this step
  continue-on-error: # Do not fail job if step fails
```

---

## 🌍 Environment Variables (`env:`)

Environment variables can be defined at **multiple levels**.

```yaml
env:
  MY_VAR: value
```

Supported levels:

* Workflow level
* Job level
* Step level

---

## 📤 Job Outputs (`outputs:`)

Used to pass values from one job to another.

```yaml
jobs:
  build:
    outputs:
      version: ${{ steps.set_version.outputs.version }}
```

---

## 🔌 `uses:` Formats

Different ways to reference an action.

```yaml
uses: actions/checkout@v4       # Public GitHub action
uses: ./local-action            # Local action in same repo
uses: docker://alpine:latest    # Docker image as action
```

---

## 🧪 Example Workflow

```yaml
# Name of the workflow shown in GitHub Actions UI
name: Sample CI Workflow

# Define when the workflow should run
on:
  push:               # Trigger on push events
    branches:
      - main
  workflow_dispatch:  # Allow manual trigger

# Define jobs
jobs:
  build:
    name: Build Job

    # Runner (dynamic VM provided by GitHub)
    runs-on: ubuntu-latest

    # Job-level environment variables
    env:
      APP_NAME: demo-app

    steps:
      # Step 1: Checkout source code
      - name: Checkout Code
        uses: actions/checkout@v4

      # Step 2: Print message
      - name: Print Message
        run: echo "Building $APP_NAME"

      # Step 3: Run shell commands
      - name: Run Build Commands
        run: |
          echo "Compiling application"
          echo "Build successful"
```

---

## 🧠 Interview-Ready Summary

* GitHub Actions is GitHub’s native CI/CD tool
* Pipelines are called **workflows**
* Written in YAML
* Uses dynamic runners (VMs)
* Jobs run in parallel by default
* Steps execute commands or actions
* No server or agent management required
* `jobs` is the only **mandatory** top-level key
* Jobs run in **parallel by default**
* `needs` makes jobs sequential
* `runs-on` defines the runner
* `steps` define actual execution
* `matrix` enables multiple configurations

---

📌 **Best Practice:**
Keep workflows small, reusable, and use GitHub-hosted runners unless you need full control with self-hosted runners.
