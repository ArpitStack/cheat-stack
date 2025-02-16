# Advanced Git Commands CheatSheet

A comprehensive guide covering advanced Git commands for power users, including interactive rebasing, advanced merging, debugging, and performance optimization.

## Table of Contents

- [Interactive Rebasing](#interactive-rebasing)
- [Squashing Commits](#squashing-commits)
- [Rewriting History](#rewriting-history)
- [Bisecting](#bisecting)
- [Sparse Checkout](#sparse-checkout)
- [Worktrees](#worktrees)
- [Advanced Merging](#advanced-merging)
- [Performance Optimization](#performance-optimization)

## Interactive Rebasing

Rebase interactively to modify commit history:

```bash
git rebase -i HEAD~5
```

## Squashing Commits

Squash multiple commits into one during a rebase:

```bash
git rebase -i HEAD~3
```

Mark commits as `squash` (or `s`) to merge them.

## Rewriting History

Change author of last commit:

```bash
git commit --amend --author="New Name <new.email@example.com>"
```

Modify commit messages for multiple past commits:

```bash
git rebase -i --root
```

## Bisecting

Find the commit that introduced a bug:

```bash
git bisect start
git bisect bad  # Mark current commit as bad
git bisect good <commit-hash>  # Mark a known good commit
git bisect run <script-to-test>
git bisect reset  # Exit bisect mode
```

## Sparse Checkout

Checkout only part of a repository:

```bash
git sparse-checkout init
git sparse-checkout set <directory>
```

## Worktrees

Create a new worktree to work on multiple branches simultaneously:

```bash
git worktree add ../new-branch new-branch
```

Remove a worktree:

```bash
git worktree remove ../new-branch
```

## Advanced Merging

Resolve merge conflicts with a tool:

```bash
git mergetool
```

Merge branches while keeping only one side's changes:

```bash
git merge -X ours <branch>
git merge -X theirs <branch>
```

## Performance Optimization

Speed up Git for large repositories:

```bash
git gc --aggressive --prune=now
git repack -a -d --depth=250 --window=250
```

Enable file system monitor for faster status checks:

```bash
git config --global core.fsmonitor true
```