---
layout: post
title: 'How to Change the Default Branch Name from "master" to "main"'
date: 2023-07-31 10:04:00 -0700
categories: [Blog, Technology, Jekyll, Git]
author: Sean Morrison
---

1. **Backup Your Data**: Before making any significant changes, ensure you have a backup of your data. On a Mac, you can use Time Machine to make a backup.

2. **Navigate to GitHub Repository**: Head over to your GitHub account and go to the specific repository for your website.

3. **Access Repository Settings**:
   - Click on the "Settings" tab.
   - Then, find the "Default Branch" section.

4. **Edit the Branch Name**:
   - Click the edit button next to the "master" branch name.
   - Change the name from "master" to "main."
   - Upon confirming the change, GitHub will provide you with a set of commands to run in your local terminal.

5. **Update Local Repository**:
   - Open your terminal and navigate (`cd`) to your local repository.
   - Run the following commands provided by GitHub to rename the branch:

   ```zsh
   git branch -m master main
   git fetch origin
   git branch -u origin/main main
   git remote set-head origin -a
   ```

   - Perform a `git pull` and `git status` to ensure everything is up to date.

6. **Verify the Change**: Check both on GitHub and your local environment to confirm that the default branch name has been successfully changed to "main."

7. **Celebrate**: You've modernized your branch naming, aligning it with the inclusive language initiative. Your default branch name has been changed. Awesome!

This guide represents a careful step-by-step approach to update a critical part of your version control system, reflecting more inclusive language. It's a small but meaningful change, and your detailed instructions make it accessible for others to follow.
