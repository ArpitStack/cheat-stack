# Git Commands CheatSheet

A comprehensive guide covering essential Git commands for version control, collaboration, and repository management.

## Table of Contents

- [Git Configuration](#git-configuration)
- [Repository Management](#repository-management)
- [Branching & Merging](#branching--merging)
- [Committing Changes](#committing-changes)
- [Undoing Changes](#undoing-changes)
- [Working with Remotes](#working-with-remotes)
- [Tagging](#tagging)
- [Stashing](#stashing)
- [Rebasing](#rebasing)
- [Cherry-Picking](#cherry-picking)
- [Logging & History](#logging--history)
- [Submodules](#submodules)
- [Git Hooks](#git-hooks)

## Git Configuration

Set your Git username:

```bash
git config --global user.name "Your Name"
```

Set your Git email:

```bash
git config --global user.email "your.email@example.com"
```

Check current configuration:

```bash
git config --list
```

## Repository Management

Initialize a new repository:

```bash
git init
```

Clone an existing repository:

```bash
git clone <repo-url>
```

## Branching & Merging

List branches:

```bash
git branch
```

Create a new branch:

```bash
git branch <branch-name>
```

Switch to a branch:

```bash
git checkout <branch-name>
```

Create and switch to a new branch:

```bash
git checkout -b <branch-name>
```

Merge a branch into the current branch:

```bash
git merge <branch-name>
```

Delete a branch:

```bash
git branch -d <branch-name>
```

## Committing Changes 

Check the status of changes:

```bash
git status
```

Add files to staging:

```bash
git add <file>
git add .  # Add all changes
```

Commit changes: 

```bash
git commit -m "Commit message"
```

Amend the last commit:

```bash
git commit --amend
```

## Undoing Changes

Unstage a file:

```bash
git reset <file>
```

Revert a commit:

```bash
git revert <commit-hash>
```

Reset branch to a previous commit:

```bash
git reset --hard <commit-hash>
```

## Working with Remotes

List remote repositories:

```bash
git remote -v
```

Add a new remote repository:

```bash
git remote add origin <repo-url>
```

Fetch changes from remote:

```bash
git fetch origin
```

Push changes to remote:

```bash
git push origin <branch-name>
```

Pull latest changes from remote:

```bash
git pull origin <branch-name>
```

## Tagging

List all tags:

```bash
git tag
```

Create a new tag:

```bash
git tag -a <tag-name> -m "Tag message"
```

Push tags to remote:

```bash
git push origin --tags
```

## Stashing

Save uncommitted changes:

```bash
git stash
```

Apply stashed changes:

```bash
git stash pop
```

List stashes:

```bash
git stash list
```

## Rebasing

Rebase current branch onto another branch:

```bash
git rebase <branch-name>
```

Continue rebase after conflict resolution:

```bash
git rebase --continue
```

Abort a rebase:

```bash
git rebase --abort
```

## Cherry-Picking

Apply a specific commit from another branch:

```bash
git cherry-pick <commit-hash>
```

## Logging & History

View commit history:

```bash
git log --oneline --graph --decorate --all
```

View changes in a specific commit:

```bash
git show <commit-hash>
```

## Submodules

Add a submodule:

```bash
git submodule add <repo-url>
```

Initialize and update submodules:

```bash
git submodule update --init --recursive
```

## Git Hooks

List available hooks:

```bash
ls .git/hooks/
```

Enable a hook (e.g., pre-commit):

```bash
chmod +x .git/hooks/pre-commit
```

