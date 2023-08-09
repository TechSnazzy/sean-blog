---
layout: post
title: 'Quick Guide to Getting Up and Running with Jekyll'
date: 2023-07-27 10:30:00 -0700
categories: [Blog, Technology, Jekyll]
author: Sean Morrison
---

Here's a quick guide on how I set up my Jekyll site and hosted it using GitHub Pages. I'll walk you through the entire process step by step, covering everything from the basics to creating your first posts and introducing git (I'll expand on git in a future post).

## Step 1: Consult Jekyll Documentation and Install Necessary Packages

The initial step is to review the [Jekyll documentation](https://jekyllrb.com/). Depending on your operating system - Windows, Mac, or Linux - you'll need to follow the corresponding instructions. Personally, I've worked with macOS and Ubuntu, so I'm more familiar with them. The setup is slightly different for each system, but the [Jekyll Docs](https://jekyllrb.com/docs/) explain everything you need to know.

Although you can install Jekyll on Windows, my experience found it to be less smooth compared to using it on macOS or Ubuntu. Interestingly, most tools I use, like Github and VSCode, are Microsoft products.

To ensure everything is correctly set up, check the versions of the required tools with these commands:

```bash
ruby -v
gem -v
jekyll -v
bundler -v
git -v
```

## Step 2: Create a New Jekyll Site

Now, let's scaffold a new Jekyll site. I typically store my projects in a directory called `Development`, so let's navigate there and create the site:

```bash
cd ~/Development
jekyll new test-blog
cd test-blog
bundle exec jekyll serve
```

Open your browser and type [127.0.0.1:4000](https://127.0.0.1:4000) to see your new site, sporting the minimalist Minima theme. Customization details can wait; this guide focuses on getting you started.

## Step 3: Initialize a git Repository and Push to Github

Your site is ready; now let's manage it with git and host it on Github Pages. If git is new to you, follow this [first-time git setup guide](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup) and sign up on [github.com](https://www.github.com) if needed.

Once set up, use these commands to push your repository to Github:

```bash
git init
git add .
git commit -m "First commit"
git status
```

On Github, create a new repository with the same name as your local project (e.g., `test-blog`) and follow the provided commands to push:

```bash
git remote add origin https://github.com/TechSnazzy/test-blog.git
git branch -M main
git push -u origin main
```

Since Github Pages requires a `gh-pages` branch, create and push it:

```bash
git checkout -b gh-pages
git add .
git commit -m "Created gh-pages branch"
git push --set-upstream origin gh-pages
git status
```

Verify the `gh-pages` branch on Github, and your site should now be live!

## Step 4: Customize Config File and Add Posts

Your Jekyll project with Github Pages is functional. Now, it's time to configure the site and add posts.

Open the `_config.yml` file to make the necessary updates. Here's an overview:

### Blog Title

```yaml
title: TechSnazzy Blog
```

### Description

```yaml
description: >-
  Write any description you want here
```

### Base URL

```yaml
baseurl: 'test-blog'
```

### Website URL

```yaml
url: 'https://techsnazzy.com'
```

To toggle between local and live testing, use these configurations:

```yaml
# Local
baseurl: ''
url: ''
# GitHub
# baseurl: "sean-blog"
# url: "https://techsnazzy.com"
```

Next, you'll need content. Create posts in markdown in the `_posts` directory following this format: [`2016-05-19-super-short-article.md`](http://2016-05-19-super-short-article.md/). Include [front matter](https://jekyllrb.com/docs/front-matter/) for layout, title, date, categories, author, and metadata.

Here's a post example:

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

Lorem ipsum...
```

Once you're done, push your changes, and your Jekyll site is ready for visitors. Happy blogging!