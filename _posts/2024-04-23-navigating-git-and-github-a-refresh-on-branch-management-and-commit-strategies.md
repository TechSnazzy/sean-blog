---
layout: post
title: 'Navigating Git and GitHub: A Refresh on Branch Management and Commit Strategies'
date: 2024-04-23 10:00:00 -0700
categories:
  [
    git,
    github,
    version control,
    gh-pages,
    development workflow,
  ]
author: Sean Morrison
---

Recently, I revisited some fundamental Git operations while updating my GitHub Pages repository. This post serves as a refresher on some essential commands and procedures that are crucial for maintaining a streamlined development process.

## Fetching and Branch Confirmation
To ensure that your local repository aligns with your remote repository on GitHub, start with a simple `git status`:

```bash
git status
```

This command checks the current status of your local repo but does not compare it with the remote repository. To fetch the latest changes and see how your local branch compares to the remote, use:

```bash
git fetch origin
git diff origin/main
```

Replace `main` with your branch name if different.

## Branch Management
I encountered a mix-up with branch names due to inactivity. To confirm the branch you're currently working on, you can list all branches:

```bash
git branch -a
```

This command helps identify both local and remote branches, indicating the active branch with an asterisk (*).

## Deleting Unwanted Files
During cleanup, I realized `.DS_Store` files had accumulated in the repo. After deleting them locally, they must be staged and committed:

```bash
git add -u
git commit -m "Remove .DS_Store files"
git push origin main
```

## Handling Discrepancies Between Devices
A common issue when working across different devices (e.g., Windows and Mac) is discrepancies in file presence. It's crucial to consistently pull the latest changes before making new commits:

```bash
git checkout correct-branch  # Replace with your actual branch
git pull origin correct-branch
```

## Conclusion
Git is an essential tool for version control. Regular practice and documentation like this blog post help solidify understanding and ensure smoother project management.
