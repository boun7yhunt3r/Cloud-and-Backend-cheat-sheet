# Git Cheat Sheet

A concise, visually organized guide to essential Git commands for setup, local repository management, branching, remote operations, and collaboration.

---

## **1. Setup & Configuration**

### **`git init`**
- **Purpose**: Initialize a new Git repository
- **Syntax**: `git init`
- **Notes**:
  - Creates a `.git` folder in the current directory
- **Example**:
  ```bash
  git init
  ```

### **`git config`**
- **Purpose**: Set user info and configurations
- **Syntax**: `git config [OPTIONS] <key> <value>`
- **Key Options**:
  - `--global` — Apply to all repositories
  - `--local` — Apply to current repo only
- **Examples**:
  ```bash
  git config --global user.name "Your Name"
  git config --global user.email "your.email@example.com"
  ```

---

## **2. Local Repository Management**

### **`git add`**
- **Purpose**: Stage changes for commit
- **Syntax**: `git add [OPTIONS] <path>`
- **Key Options**:
  - `.` — Stage all changes
  - `-u` — Stage modified and deleted files
  - `-A` — Stage all (new, modified, deleted)
- **Example**:
  ```bash
  git add .
  ```

### **`git commit`**
- **Purpose**: Save staged changes to local repo
- **Syntax**: `git commit [OPTIONS]`
- **Key Options**:
  - `-m` — Add commit message
  - `-a` — Auto-stage tracked files
  - `--amend` — Modify the last commit
- **Example**:
  ```bash
  git commit -m "Initial commit"
  ```

### **`git status`**
- **Purpose**: Check repo status
- **Syntax**: `git status [OPTIONS]`
- **Key Options**:
  - `-s` — Short format
  - `-b` — Show branch info
- **Example**:
  ```bash
  git status
  ```

### **`git log`**
- **Purpose**: View commit history
- **Syntax**: `git log [OPTIONS]`
- **Key Options**:
  - `--oneline` — One line per commit
  - `--graph` — Visualize branch history
  - `-n` — Limit to n commits (e.g., `-2`)
- **Example**:
  ```bash
  git log --oneline --graph
  ```

---

## **3. Branching**

### **`git branch`**
- **Purpose**: List, create, or delete branches
- **Syntax**: `git branch [OPTIONS] [branch-name]`
- **Key Options**:
  - `-d` — Delete branch
  - `-r` — List remote branches
  - `-a` — List all branches (local + remote)
- **Example**:
  ```bash
  git branch feature-x
  ```

### **`git checkout`**
- **Purpose**: Switch branches or restore files
- **Syntax**: `git checkout [OPTIONS] <branch>|<commit>|<file>`
- **Key Options**:
  - `-b` — Create and switch to new branch
- **Example**:
  ```bash
  git checkout -b feature-x
  ```

### **`git switch`**
- **Purpose**: Switch to a branch (modern alternative to `checkout`)
- **Syntax**: `git switch [OPTIONS] <branch>`
- **Key Options**:
  - `-c` — Create and switch to new branch
- **Example**:
  ```bash
  git switch -c feature-x
  ```

### **`git merge`**
- **Purpose**: Merge a branch into the current one
- **Syntax**: `git merge [OPTIONS] <branch>`
- **Key Options**:
  - `--no-ff` — No fast-forward, create merge commit
  - `--abort` — Cancel a merge in progress
- **Example**:
  ```bash
  git merge feature-x
  ```

---

## **4. Remote Operations**

### **`git remote`**
- **Purpose**: Manage remote repositories
- **Syntax**: `git remote [OPTIONS] <name> <url>`
- **Key Options**:
  - `add` — Add a remote repo
  - `-v` — List remotes verbosely
- **Example**:
  ```bash
  git remote add origin https://github.com/user/repo.git
  ```

### **`git push`**
- **Purpose**: Push local changes to remote repo
- **Syntax**: `git push [OPTIONS] <remote> <branch>`
- **Key Options**:
  - `-u` — Set upstream branch
  - `-f` — Force push (use cautiously)
- **Example**:
  ```bash
  git push -u origin main
  ```

### **`git pull`**
- **Purpose**: Fetch and merge remote changes
- **Syntax**: `git pull [OPTIONS] <remote> <branch>`
- **Key Options**:
  - `--rebase` — Rebase instead of merge
- **Example**:
  ```bash
  git pull origin main
  ```

### **`git fetch`**
- **Purpose**: Download remote changes without merging
- **Syntax**: `git fetch [OPTIONS] <remote>`
- **Key Options**:
  - `--all` — Fetch all remotes
- **Example**:
  ```bash
  git fetch origin
  ```

---

## **5. Collaboration & History**

### **`git clone`**
- **Purpose**: Copy a remote repo to local
- **Syntax**: `git clone [OPTIONS] <repository> [directory]`
- **Key Options**:
  - `--depth` — Shallow clone (e.g., `--depth 1`)
- **Example**:
  ```bash
  git clone https://github.com/user/repo.git my-repo
  ```

### **`git rebase`**
- **Purpose**: Reapply commits on top of another base
- **Syntax**: `git rebase [OPTIONS] <branch>`
- **Key Options**:
  - `-i` — Interactive rebase (edit commits)
  - `--abort` — Cancel rebase
- **Example**:
  ```bash
  git rebase -i main
  ```

### **`git reset`**
- **Purpose**: Reset current HEAD to a state
- **Syntax**: `git reset [OPTIONS] <commit>`
- **Key Options**:
  - `--soft` — Keep changes staged
  - `--hard` — Discard all changes
- **Example**:
  ```bash
  git reset --hard HEAD~1
  ```

### **`git stash`**
- **Purpose**: Temporarily save uncommitted changes
- **Syntax**: `git stash [OPTIONS]`
- **Key Options**:
  - `push` — Stash changes
  - `pop` — Apply and remove latest stash
  - `list` — Show stashed changes
- **Example**:
  ```bash
  git stash push -m "WIP changes"
  git stash pop
  ```

---

**Note**: Save this as `GIT_CHEAT_SHEET.md` in your GitHub repo for a clean, readable reference!