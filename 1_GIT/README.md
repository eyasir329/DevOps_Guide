# Git for DevOps

Git is a core DevOps tool because it helps you collaborate with developers, track infrastructure/automation changes, and recover quickly when something breaks.

### Guiding principles

- As a system admin: take a backup (or snapshot) before risky changes.
- Git tracks files, not empty directories.
- Git is a great rollback mechanism, but it is not a substitute for backups unless your work is committed and stored somewhere durable (for example, a remote like GitHub).

---

## Why DevOps engineers use Git

- **Shared workflow with developers**: pull code, build, test, deploy.
- **Versioning automation**: scripts, configs, IaC, pipelines, documentation.
- **Audit + recovery**: see who changed what and revert when needed.

---

## Evolution of version control

![vcs](vcs1.png)
![vcs](vcs2.png)
![vcs](vcs3.png)

- **Local version control**: changes tracked only on one machine (like manual timestamped backups).
- **Centralized version control**: a single server stores history (single point of failure).
- **Distributed version control (Git)**: each clone has the full history; you can commit offline and sync later.

![vcs](vcs5.png)
![vcs](vcs6.png)
![vcs](vcs7.png)
![vcs](vcs8.png)
![vcs](vcs9.png)
![vcs](vcs10.png)

### Key context

- Git was created by **Linus Torvalds** to manage Linux kernel development.
- GitHub hosts Git repositories and enables team collaboration.

![vcs](vcs11.png)
![vcs](vcs12.png)

---

## Installation and initial setup

### Install Git

- **Windows**: install Git Bash
- **macOS**: `brew install git`
- **Linux**: install via your distro package manager (APT/YUM/SNAP, etc.)

![versioning](v1.png)
![versioning](v2.png)
![versioning](v3.png)
![versioning](v4.png)
![versioning](v5.png)
![versioning](v6.png)

### Configure identity (one-time)

```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```

### Create a new repository

```bash
git init
```

This creates the `.git/` directory which stores your history and metadata.

---

## Local workflow (working tree → staging → commit)

![versioning](v7.png)

### Everyday commands

```bash
git status
git add .
git commit -m "Describe your change"
```

### Inspect changes

- Unstaged changes: `git diff`
- Staged changes: `git diff --cached`

### History

- `git log` (full)
- `git log --oneline` (compact)
- `git show <commit-id>` (details for one commit)

---

## Remote integration (GitHub)

### Link local repo to a remote

```bash
git remote add origin <URL>
git branch -M main
git push -u origin main
```

### Sync

- Push local commits: `git push origin main`
- Pull remote updates: `git pull`

![versioning](v8.png)
![versioning](v9.png)
![versioning](v10.png)
![versioning](v11.png)
![versioning](v12.png)
![versioning](v13.png)
![versioning](v14.png)
![versioning](v15.png)
![versioning](v16.png)
![versioning](v17.png)

---

## Branching, merging, and repository management

Branches let multiple people work in parallel without breaking the stable branch.

### Branch basics

- Create a branch: `git branch <branch-name>`
- Create + switch (older): `git checkout -b <branch-name>`
- Switch (recommended): `git switch <branch-name>`
- List branches: `git branch -a`

### Push branches

- Push one branch: `git push origin <branch-name>`
- Push all local branches: `git push --all origin`

### Merge

```bash
git switch main
git merge <feature-branch>
```

Git may open an editor for the merge commit message.

### Ignore files

Use `.gitignore` to prevent committing generated files (for example, `*.log`).

### Common file operations

- Remove tracked file: `git rm <file>`
- Rename/move with history: `git mv <old-name> <new-name>`
- Clone a repo: `git clone <URL>`

![branches](B1.png)
![branches](B2.png)
![branches](B3.png)
![branches](B4.png)
![branches](B5.png)
![branches](B6.png)
![branches](B7.png)
![branches](B8.png)
![branches](B9.png)
![branches](B10.png)
![branches](B11.png)
![branches](B12.png)
![branches](B13.png)
![branches](B14.png)
![branches](B15.png)

---

## Rolling back changes

Git gives you different rollback options depending on where you are in the workflow.

### 1) Undo before staging (discard local edits)

- Discard changes in a file (recommended):

  ```bash
  git restore <filename>
  ```

- Older equivalent:

  ```bash
  git checkout -- <filename>
  ```

- Verify what will be discarded: `git diff`

### 2) Undo after staging (unstage without losing edits)

```bash
git restore --staged <filename>
```

- Verify staged delta: `git diff --cached`

### 3) Undo after committing

- **Revert (safe, keeps history)**:

  ```bash
  git revert HEAD
  ```

- **Reset (destructive, rewrites history)**:

  ```bash
  git reset --hard <commit-id>
  ```

Use `reset --hard` only when you understand the impact (especially if commits were already pushed/shared).

### Helpful verification

- `git status`
- `git log --oneline`
- `git diff <previous-id>..<current-id>`

![rollback](./R1.png)
![rollback](./R2.png)
![rollback](./R3.png)
![rollback](./R4.png)
![rollback](./R5.png)
![rollback](./R6.png)
![rollback](./R7.png)
![rollback](./R8.png)

---

## SSH authentication with GitHub

SSH enables password-free Git operations and works well for automation and CI/CD.

### Why SSH instead of HTTPS

- More secure (key-based auth)
- No repeated credential prompts
- Works well in non-interactive automation

### SSH setup

#### Generate keys

Recommended (modern):

```bash
ssh-keygen -t ed25519 -C "your_email@example.com"
```

Fallback (if you specifically need RSA):

```bash
ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
```

This creates a private key (keep secret) and a public key you can share.

#### Add public key to GitHub

```bash
cat ~/.ssh/id_ed25519.pub
```

Then GitHub → Settings → SSH and GPG keys → New SSH key.

#### Clone using SSH

```bash
git clone git@github.com:username/repository.git
```

On first connection, verify the fingerprint and type `yes`.

![ssh](S1.png)
![ssh](S2.png)
![ssh](S3.png)
![ssh](S4.png)
![ssh](S5.png)
![ssh](S6.png)
![ssh](S7.png)

---

## Hands-on notes (practice session)

### Manual backups vs Git

- Manual backups:

  ```bash
  cp file.sh file.sh.bak
  tar czvf remotexecmulti.Backup.tar.gz *.bakup
  rm -rf *.bakup
  ```

Manual backups are error-prone and hard to manage at scale. Git makes changes traceable and recoverable.

### Common repository operations

```bash
git status
git merge sprint1
git switch sprint1
git push --all origin
```

### Recovery via clone

```bash
rm -rf titanwork
git clone https://github.com/imranvisualpath/titanwork.git
```

This demonstrates how a remote can act as a recovery source.

### Inspecting and rolling back files

```bash
git diff
git restore jupiter1.rb
git restore --staged jupiter1.rb
```

Note: older docs may show `git checkout <file>`. Prefer `git restore <file>`.

### Commit + compare

```bash
git commit -m "playbook"
git log --oneline
git diff <commit-id1>..<commit-id2>
```

### Key takeaway

Git replaces fragile manual backups, enables safe recovery via remotes, supports rollbacks at each stage, and SSH improves security + automation.

---

## References

- https://about.gitlab.com/images/press/git-cheat-sheet.pdf
- https://wac-cdn.atlassian.com/dam/jcr:e7e22f25-bba2-4ef1-a197-53f46b6df4a5/SWTM-2088_Atlassian-Git-Cheatsheet.pdf?cdnVersion=3145

---

## Git command cheat sheet (quick table)

| **Category**          | **Command**                               | **Example**                                              | **Description**                         |
| --------------------- | ----------------------------------------- | -------------------------------------------------------- | --------------------------------------- |
| **Setup**             | `git config --global user.name "Name"`    | `git config --global user.name "John Doe"`               | Set your Git username                   |
|                       | `git config --global user.email "email"`  | `git config --global user.email "john@example.com"`      | Set your Git email                      |
|                       | `git init <dir>`                          | `git init titanwork`                                     | Initialize a new repo                   |
| **Status & Tracking** | `git status`                              | `git status`                                             | Check staged/unstaged/untracked files   |
|                       | `git add <file>`                          | `git add saturn1.py`                                     | Stage a file                            |
|                       | `git add .`                               | `git add .`                                              | Stage all changes                       |
|                       | `git commit -m "msg"`                     | `git commit -m "Initial commit"`                         | Commit staged changes                   |
|                       | `git log`                                 | `git log`                                                | View commit history                     |
|                       | `git log --oneline`                       | `git log --oneline`                                      | Condensed commit history                |
| **Branching**         | `git branch`                              | `git branch`                                             | List branches                           |
|                       | `git checkout -b <branch>`                | `git checkout -b sprint1`                                | Create & switch (older)                 |
|                       | `git switch <branch>`                     | `git switch main`                                        | Switch branch (recommended)             |
|                       | `git merge <branch>`                      | `git merge sprint1`                                      | Merge branch into current               |
| **Remote**            | `git clone <url>`                         | `git clone https://github.com/user/repo.git`             | Copy remote repo locally                |
|                       | `git remote add <name> <url>`             | `git remote add origin https://github.com/user/repo.git` | Link local to remote                    |
|                       | `git push <remote> <branch>`              | `git push origin main`                                   | Push commits to remote                  |
|                       | `git pull`                                | `git pull`                                               | Fetch & merge remote changes            |
| **Undo Changes**      | `git restore <file>`                      | `git restore saturn1.py`                                 | Discard unstaged changes                |
|                       | `git restore --staged <file>`             | `git restore --staged saturn1.py`                        | Unstage file but keep edits             |
|                       | `git revert <commit>`                     | `git revert HEAD`                                        | Undo a commit by creating a new one     |
|                       | `git reset --hard <commit>`               | `git reset --hard a1b2c3d`                               | Reset branch & delete later commits     |
| **Diff / Inspect**    | `git diff`                                | `git diff`                                               | Show unstaged changes                   |
|                       | `git diff --cached`                       | `git diff --cached`                                      | Show staged vs last commit              |
|                       | `git diff HEAD~1..HEAD`                   | `git diff HEAD~1..HEAD`                                  | Show changes in last commit             |
|                       | `git diff <c1>..<c2>`                     | `git diff a1b2..d4e5`                                    | Show changes between two commits        |