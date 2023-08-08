---
layout: post
title: 'Quick Guide to Getting Up and Running with Jekyll'
date: 2023-07-27 10:30:00 -0700
categories: [Blog, Technology, Jekyll]
author: Sean Morrison
---

Hey there! Interested in creating a blog site with Jekyll and GitHub Pages? Well, you've come to the right place! Follow this easy guide to set up your very own Jekyll site, push it to GitHub, and even get a glimpse of working with git. Let's get started! 🎉

## Step 1: Check the Jekyll documentation and install packages

First things first, let's dive into the documentation on the [Jekyll website](https://jekyllrb.com/). You'll want to follow different instructions depending on whether you're using Windows, Mac, or Linux. Most of my experience is with macOS and Ubuntu, so I'll focus on those.

Windows is also an option, but I've found it to be a bit tricky. Interestingly, most of the tools I use are Microsoft products. But, let's not get sidetracked!

To make sure you have everything up to date, check the versions of all the required tools:

```bash
# all of these are requirements
ruby -v
gem -v
jekyll -v
bundler -v
git -v
```

## Step 2: Create a new Jekyll site

Now, let's create a new Jekyll site! I usually store my projects in a directory called `Development`. So, I'll `cd` to it and create my Jekyll site:

```bash
cd ~/Development
jekyll new test-blog
cd test-blog
bundle exec jekyll serve
```

Type [127.0.0.1:4000](https://127.0.0.1:4000) in your browser to see your brand-new Jekyll site! If everything goes well, you'll see the minimalist Minima theme, which we can customize later.

## Step 3: Create a new git repo and push it to Github

You've got a site now! Let's turn it into a git repo and `git push` it to GitHub. If you're new to git, check out this [first-time git config setup guide](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup). If you don't have a GitHub account, [sign up here](https://www.github.com).

Now follow these steps to push your repo to Github:

```bash
git init # initialize the repo
git add . # add all folders and files to the staging area
git commit -m "First commit" # commit all folders and files to the repo
git status
git remote add origin https://github.com/TechSnazzy/test-blog.git
git branch -M main
git push -u origin main
```

To make it work with Github Pages, create a `gh-pages` branch like this:

```bash
git checkout -b gh-pages
git add .
git commit -m "Created gh-pages branch"
git push --set-upstream origin gh-pages
git status
```

Head back to your GitHub repo and switch to the `gh-pages` branch, and voila! Your site is live! 🥳

## Step 4: Edit the config file and add some posts

With the functionality all set, it's time to customize your site and create some posts.

### **Config File**

Open your `_config.yml` file and update these sections:

- **Title**:
  ```yaml
  title: TechSnazzy Blog
  ```

- **Description**:
  ```yaml
  description: >-
    Write any description you want here
  ```

- **Base URL and URL**:
  ```yaml
  baseurl: 'test-blog'
  url: 'https://techsnazzy.com'
  ```

  Note: Use different settings for local and GitHub. Here's how I do it:
  ```yaml
  # Local
  baseurl: ''
  url: ''
  # GitHub
  # baseurl: "sean-blog"
  # url: "https://techsnazzy.com"
  ```

### **Create Posts**

Your posts will be in markdown files in the `_posts` directory. The file format should look like this [`2016-05-19-super-short-article.md`](http://2016-05-19-super-short-article.md/) (year-month-day-description.md), and the post should contain [front matter](https://jekyllrb.com/docs/front-matter/).

Here's an example:

```markdown
---
layout: post
title: 'This post demonstrates post content styles'
date: 2023-07-31 10:04:00 -0700
categories: junk
author:
  - Bart Simpson
  - Nelson Mandela Muntz
meta: 'Springfield'
---
## Some great heading
Lorem ipsum dolor sit amet, consectetur adipiscing elit...
```

And that's it! `git push` your changes, and your new post is live on your site. Congratulations on your new Jekyll site, and happy blogging! 🎈

Feel free to explore further and make your site uniquely yours. Whether it's customizing the theme or diving deeper into git, there's always more to learn and experiment with. Enjoy the journey!
