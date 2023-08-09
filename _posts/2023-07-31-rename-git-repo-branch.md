---
layout: post
title: 'How to Change the Default Branch Name to "main"'
date: 2023-07-31 10:04:00 -0700
categories: [Blog, Technology, Jekyll, Git]
author: Sean Morrison
---

Hello there! Welcome to another tech-savvy update from [techsnazzy.com](https://www.techsnazzy.com). I've got something special to share with you about the fascinating world of website hosting.

Let's take a stroll down memory lane. When I first launched my technology consultation services business back in 2018, the world of Git was a bit different. Remember the default branch name "master"? Times have changed, and so has the default branch name, which is now called "main" to foster a more inclusive language.

Recently, I realized that my very own website still used the old-fashioned name "master." Naturally, I wanted to make things right, and in the spirit of tech-forward thinking, I changed it to "main." Let me guide you through how I did it, just in case you need to do the same!

### 1. **Create a Backup**

You know the saying, "better safe than sorry?" That's the mantra to follow when making significant changes to your site. Since I use a Mac, I relied on Time Machine to create my backup. It's a quick and easy process that ensures you're covered if something unexpected happens.

### 2. **Navigate to GitHub**

With my data safe and sound, I headed over to GitHub. If you need to do the same, follow these simple steps:

- Go to your repository.
- Click on Settings.
- Find the Default Branch section.
- Edit the name from "master" to "main."

Once that's done, GitHub will kindly provide you with some commands.

### 3. **Execute the Commands**

Here's what you'll need to do next:

1. Open your terminal.
2. Navigate to your repository using `cd path/to/your/repo`.
3. Paste and execute the following commands:

```zsh
git branch -m master main
git fetch origin
git branch -u origin/main main
git remote set-head origin -a
```

4. Run a `git pull` followed by `git status` to ensure everything is up-to-date and synchronized.

And voila! Your default branch name has been changed. You've successfully modernized your Git setup, aligning it with contemporary practices. Pretty awesome, right?

Feel free to share your thoughts or ask any questions, and remember to keep up with all the latest and greatest over at [techsnazzy.com](https://www.techsnazzy.com). Happy coding! 🚀