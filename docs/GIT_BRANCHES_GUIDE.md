# Git Branch Workflow Guide

A step-by-step guide for working with Git branches and GitHub.

---

## Table of Contents

1. [Delete a Branch](#1-delete-a-branch)
2. [Create a New Branch](#2-create-a-new-branch)
3. [Push a Branch to GitHub](#3-push-a-branch-to-github)
4. [Switch Between Branches](#4-switch-between-branches)
5. [List Branches](#5-list-branches)
6. [Common Workflow](#6-common-workflow)

---

## 1. Delete a Branch

### Delete locally

**Important:** You cannot delete the branch you're currently on. Switch to another branch first.

| Step | Command | What it does |
|------|---------|--------------|
| 1 | `git checkout main` | Switch to `main` (or any other branch) |
| 2 | `git branch -d feature/next` | Delete the branch locally (safe—only if merged) |
|   | `git branch -D feature/next` | Force delete (use if branch has unmerged changes) |

### Delete on GitHub (remote)

| Step | Command | What it does |
|------|---------|--------------|
| 1 | `git push origin --delete feature/next` | Remove the branch from the remote repository |

### Summary

```bash
# Switch away from the branch you want to delete
git checkout main

# Delete locally
git branch -d feature/next

# Delete on GitHub (if it was pushed)
git push origin --delete feature/next
```

---

## 2. Create a New Branch

| Step | Command | What it does |
|------|---------|--------------|
| 1 | `git checkout -b feature/my-feature` | Create and switch to new branch in one command |
|   | `git branch feature/my-feature` | Create branch only (doesn't switch) |
| 2 | `git checkout feature/my-feature` | Switch to the new branch (if created separately) |

The new branch starts from your current commit (wherever you are when you create it).

---

## 3. Push a Branch to GitHub

| Step | Command | What it does |
|------|---------|--------------|
| 1 | `git push --set-upstream origin feature/my-feature` | Push branch and set remote tracking |
|   | `git push -u origin feature/my-feature` | Same as above (short form) |

After setting upstream, you can use `git push` and `git pull` without extra arguments.

---

## 4. Switch Between Branches

| Command | What it does |
|---------|--------------|
| `git checkout main` | Switch to `main` |
| `git checkout error-tracking` | Switch to `error-tracking` |
| `git switch main` | Same as checkout (newer Git syntax) |

Make sure you have committed or stashed changes before switching.

---

## 5. List Branches

| Command | What it does |
|---------|--------------|
| `git branch` | List local branches (current has `*`) |
| `git branch -a` | List local + remote branches |
| `git branch -v` | List with last commit info |

---

## 6. Common Workflow

### Start new work

```bash
git checkout main
git pull origin main
git checkout -b feature/new-feature
# ... make changes ...
git add .
git commit -m "Add new feature"
git push -u origin feature/new-feature
```

### Clean up after merging

```bash
git checkout main
git pull origin main
git branch -d feature/merged-feature
git push origin --delete feature/merged-feature
```

### Discard a branch you no longer need

```bash
git checkout main
git branch -D feature/abandoned
git push origin --delete feature/abandoned
```

---

## Quick Reference

| Task | Command |
|------|---------|
| Create + switch | `git checkout -b branch-name` |
| Switch branch | `git checkout branch-name` |
| Push new branch | `git push -u origin branch-name` |
| Delete local | `git branch -d branch-name` |
| Delete remote | `git push origin --delete branch-name` |
| List branches | `git branch` |
