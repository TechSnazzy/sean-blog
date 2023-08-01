---
layout: post
title: "Renaming Default Git Branch to Promote More Inclusive Language"
date:   2023-07-31 10:04:00 -0700
categories:
- Blog
- Technology
- Jekyll
- Git
author: Sean Morrison
---

My website is [techsnazzy.com](https://www.techsnazzy.com). I created it back in 2018 when I first started my technology consultation services business. Back then the default name for the default branch in a git repo was "master". These days the default branch name is "main" in an effort to promote more inclusive language.

Just recently I noticed my website still has the old-fashioned name "master" so I want to update it to "main" and here's how I did it.

First, I made sure to make a backup. You just never know if something could go wrong so it's always best to make a backup first before making a major change. So since I am on a Mac, I'm using Time Machine to make my backup.

Once my backup is done, I can do head over to GitHub. From there I go to my repo and then Settings. Then under Default Branch, I can edit the name from "master" to "main". Once I do that, some commands will pop up.

These are the commands...
```zsh
git branch -m master main
git fetch origin
git branch -u origin/main main
git remote set-head origin -a
```

Now head over to your terminal and cd over to your repo and paste those commands. Then do a `git pull` and `git status` to make sure you're all caught up and that's it. Default branch name has been changed. Awesome! 