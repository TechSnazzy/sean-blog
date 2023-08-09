---
layout: post
title: 'Managing Jekyll Configurations for Local and GitHub Deployment'
date: 2023-08-03 10:00:00 -0700
categories: [Blog, Technology, Jekyll, Git]
author: Sean Morrison
---

I've been diving into the world of Jekyll, a simple and blog-aware static site generator, for some time now, and I've gathered a wealth of knowledge that I'm excited to share. One aspect that has been particularly challenging for me was figuring out how to run Jekyll both locally and on GitHub after pushing an update. Let me share with you the journey of what I've discovered and a smart solution that makes the process far less cumbersome.

### Traditional Way: Manual Commenting and Uncommenting

Initially, I found myself in a repetitive cycle of commenting and uncommenting lines of code to switch between local and GitHub configurations. Here's what it looked like:

**When pushing to GitHub:**

```yaml
#Local
# baseurl: ""
# url: ""

# GitHub
baseurl: 'sean-blog'
url: 'https://techsnazzy.com'
```

**When running it locally:**

```yaml
#Local
baseurl: ''
url: ''
# GitHub
#baseurl: "sean-blog"
#url: "[https://techsnazzy.com](https://techsnazzy.com)"
```

While this method works, you can probably relate to how tedious it quickly becomes.

### A Better Approach: Separate Configuration Files

I was lucky enough to stumble upon a great solution, thanks to ChatGPT. Here's what it entails:

1. **Keep the `_config.yml` file as is with the local code commented out.** This will be your default configuration for GitHub.
2. **Create another file named `_config_dev.yml` with the local code uncommented.** This will be your specific configuration for local development.
3. **When pushing an update, GitHub will continue to use the default `_config.yml` file.** No changes are needed here.
4. **When running locally, use a specific command that includes both config files.** This lets your local development environment take over the GitHub settings, like so:

```bash
bundle exec jekyll serve --config _config.yml,_config_dev.yml
```

By adopting this approach, you no longer have to get caught up in the endless loop of commenting and uncommenting lines of code. Hooray for efficiency and simplicity!

Feel free to share your experiences or ask any questions. Happy Jekyll-ing! 🚀