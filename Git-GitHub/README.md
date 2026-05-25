# Git and GitHub for DevOps Engineers

# Introduction

Git is a distributed version control system used to:
- track code changes
- collaborate with teams
- manage releases
- automate deployments
- maintain infrastructure code

GitHub is a cloud platform built around Git.

Every DevOps engineer uses Git daily for:
- CI/CD pipelines
- Infrastructure as Code
- Kubernetes manifests
- Dockerfiles
- Terraform configurations
- GitOps workflows

---

# What is Version Control?

Version control allows:
- tracking changes
- reverting changes
- collaboration
- branching
- release management

Without version control:
- deployments become risky
- rollback becomes difficult
- collaboration becomes chaotic

---

# Git Architecture

Git has three main areas:

| Area | Purpose |
|---|---|
| Working Directory | Current files |
| Staging Area | Prepared changes |
| Repository | Permanent history |

---

# Git Workflow

1. Modify files
2. Add changes
3. Commit changes
4. Push to remote

---

# Configure Git

Set username:

```bash
git config --global user.name "Amtul Saboor"
```

Set email:

```bash
git config --global user.email "your-email@example.com"
```

View config:

```bash
git config --list
```

---

# Initialize Repository

```bash
git init
```

---

# Clone Repository

```bash
git clone REPOSITORY_URL
```

Example:

```bash
git clone https://github.com/user/repo.git
```

---

# Check Status

```bash
git status
```

---

# Add Files

Add single file:

```bash
git add file.txt
```

Add all:

```bash
git add .
```

---

# Commit Changes

```bash
git commit -m "Initial commit"
```

---

# View Commit History

```bash
git log
```

Compact:

```bash
git log --oneline
```

---

# Push Changes

```bash
git push origin main
```

---

# Pull Changes

```bash
git pull origin main
```

---

# Branching

Create branch:

```bash
git branch feature-login
```

Switch branch:

```bash
git checkout feature-login
```

Create and switch:

```bash
git checkout -b feature-login
```

---

# Merge Branch

```bash
git checkout main

git merge feature-login
```

---

# Delete Branch

```bash
git branch -d feature-login
```

Force delete:

```bash
git branch -D feature-login
```

---

# Rebase

```bash
git rebase main
```

Rebase rewrites commit history.

---

# Merge vs Rebase

| Merge | Rebase |
|---|---|
| Keeps history | Cleaner history |
| Creates merge commit | Rewrites history |

---

# Git Stash

Temporarily save changes:

```bash
git stash
```

View stash:

```bash
git stash list
```

Apply stash:

```bash
git stash apply
```

---

# Cherry Pick

Apply specific commit:

```bash
git cherry-pick COMMIT_ID
```

---

# Undo Changes

Discard local changes:

```bash
git checkout -- file.txt
```

Reset staging:

```bash
git reset HEAD file.txt
```

Hard reset:

```bash
git reset --hard
```

---

# Git Tags

Create tag:

```bash
git tag v1.0
```

Push tag:

```bash
git push origin v1.0
```

---

# Remote Repositories

View remotes:

```bash
git remote -v
```

Add remote:

```bash
git remote add origin URL
```

---

# Fetch vs Pull

| Fetch | Pull |
|---|---|
| Downloads changes | Downloads + merges |

---

# Git Diff

```bash
git diff
```

Staged diff:

```bash
git diff --staged
```

---

# Git Ignore

Create:

```bash
vim .gitignore
```

Example:

```bash
node_modules/
.env
*.log
```

---

# GitHub Pull Requests

PR workflow:
1. Create branch
2. Push branch
3. Open PR
4. Review
5. Merge

---

# GitHub Actions

GitHub Actions automates:
- CI/CD
- testing
- deployments

Workflow location:

```bash
.github/workflows/
```

---

# Sample GitHub Actions Workflow

```yaml
name: CI Pipeline

on:
  push:
    branches:
      - main

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v3

      - name: Run Script
        run: echo "Hello DevOps"
```

---

# Git Internals

Git objects:
- blob
- tree
- commit
- tag

Git stores data in:

```bash
.git/
```

---

# View Git Objects

```bash
git cat-file -p COMMIT_ID
```

---

# Git Hooks

Hooks automate tasks.

Location:

```bash
.git/hooks/
```

Examples:
- pre-commit
- post-commit
- pre-push

---

# Git Aliases

Example:

```bash
git config --global alias.st status
```

Use:

```bash
git st
```

---

# Git Security Best Practices

- never commit secrets
- use .gitignore
- sign commits
- enforce branch protection
- use pull requests
- enable MFA

---

# Git Branching Strategies

| Strategy | Usage |
|---|---|
| Git Flow | Enterprise |
| GitHub Flow | Simpler workflows |
| Trunk Based | DevOps teams |

---

# GitOps

GitOps uses Git as source of truth.

Tools:
- ArgoCD
- FluxCD

Infrastructure changes happen through Git commits.

---

# 50 Most Used Git Commands

```bash
git init
git clone
git status
git add
git commit
git push
git pull
git fetch
git branch
git checkout
git switch
git merge
git rebase
git stash
git stash pop
git stash apply
git reset
git reset --hard
git revert
git cherry-pick
git tag
git log
git diff
git remote -v
git remote add
git rm
git mv
git show
git blame
git reflog
git clean
git config
git restore
git shortlog
git describe
git archive
git bisect
git grep
git notes
git fsck
git gc
git worktree
git submodule
git ls-files
git rev-parse
git cat-file
git commit --amend
git push --force
git pull --rebase
git branch -a
git branch -r
```

---

# Real World Production Scenarios

# Scenario 1 — Merge Conflict During Deployment

Symptoms:
- CI pipeline failure
- deployment blocked

Resolve:

```bash
git status
```

Edit conflict markers manually.

Then:

```bash
git add .
git commit
```

---

# Scenario 2 — Accidentally Pushed Secrets

Problem:
AWS keys committed.

Immediate Actions:
1. Remove secrets
2. Rotate credentials
3. Rewrite history

Commands:

```bash
git filter-branch
```

---

# Scenario 3 — Wrong Commit in Production

Rollback:

```bash
git revert COMMIT_ID
```

---

# Scenario 4 — Lost Commits

Recovery:

```bash
git reflog
```

---

# Scenario 5 — Detached HEAD State

Fix:

```bash
git checkout branch-name
```

---

# Production Troubleshooting Workflow

# Step 1 — Check Status

```bash
git status
```

---

# Step 2 — Check History

```bash
git log --oneline
```

---

# Step 3 — Check Branch

```bash
git branch
```

---

# Step 4 — Check Remote

```bash
git remote -v
```

---

# Step 5 — Resolve Conflicts

```bash
git diff
```

---

# Common Git Errors

| Error | Cause |
|---|---|
| merge conflict | conflicting changes |
| detached HEAD | checked out commit directly |
| rejected push | remote ahead |
| authentication failed | bad credentials |
| not a git repository | missing .git |

---

# CI/CD Integration

Git triggers:
- Jenkins pipelines
- GitHub Actions
- ArgoCD sync
- Kubernetes deployment

---

# Enterprise Git Best Practices

- small commits
- meaningful commit messages
- branch protection
- PR reviews
- avoid force push on main
- use tags for releases
- use signed commits

---

# 50 Git and GitHub Interview Questions

## Beginner

1. What is Git?
2. What is GitHub?
3. Difference between Git and GitHub?
4. What is version control?
5. What is repository?
6. Difference between local and remote repository?
7. What is commit?
8. What is branch?
9. What is merge?
10. What is clone?

---

## Intermediate

11. Difference between merge and rebase?
12. What is stash?
13. What is cherry-pick?
14. Explain detached HEAD.
15. What is Git tag?
16. Difference between fetch and pull?
17. What is .gitignore?
18. What is pull request?
19. What is fast-forward merge?
20. What is Git hook?

---

## Advanced

21. Explain Git internals.
22. What are Git objects?
23. What is reflog?
24. Explain Git garbage collection.
25. How Git stores data?
26. Explain Git index.
27. What is sparse checkout?
28. Difference between reset and revert?
29. Explain Git bisect.
30. What is shallow clone?

---

## Production Based

31. How to resolve merge conflicts?
32. Accidentally pushed secrets to GitHub. What will you do?
33. CI/CD pipeline failing due to Git issue.
34. How to rollback production code?
35. How to recover deleted branch?
36. How to secure Git repositories?
37. Large repository performance issues.
38. Git authentication failure troubleshooting.
39. Branch protection strategies.
40. Enterprise release management process.

---

## Scenario Based

41. Developer force pushed to main branch.
42. Deployment failed after merge.
43. Git history corrupted.
44. Repository size too large.
45. Lost local changes accidentally.
46. Wrong branch merged into production.
47. GitHub Actions failing suddenly.
48. Infrastructure code accidentally deleted.
49. Rebase created conflicts in production branch.
50. Explain your Git workflow in DevOps projects.

---

# Summary

Git is the foundation of modern DevOps workflows.

Strong Git skills are essential for:
- CI/CD
- GitOps
- Infrastructure as Code
- Kubernetes deployments
- release management
- team collaboration
- production rollback
- automation pipelines
