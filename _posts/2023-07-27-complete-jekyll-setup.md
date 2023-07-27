---
layout: post
title: "Complete Guide to Getting Up and Running with Jekyll"
categories:
- Blog
- Technology
- Jekyll
author:
- Sean Morrison
---

## Complete Guide to Getting Up and Running with Jekyll

## Intro

Hello. Here’s a complete guide on how I setup my Jekyll site and pushed it to Github to run as a Github Pages site. I’ll describe this step by step from scratch. I’ll also cover how to create some posts to get you started.

## Step 1: Check the Jekyll documentation and install packages

The first step is to check the documentation on the [Jekyll website here](https://jekyllrb.com/). You’ll need to determine whether you are on Windows, Mac or Linux and follow the steps accordingly. I have been working mostly on macOS and then I did a lot of work in Ubuntu as well. Getting setup is slightly different for both. But if you click on the [Jekyll Docs](https://jekyllrb.com/docs/) and read carefully you should have no problem getting setup.

To test if you are setup with everything you need, check the versions of everything to make sure it’s all installed and up to date.

```bash
# all of these are requirements
ruby -v
gem -v
jekyll -v
bundler -v
git -v
```

## Step 2: Create a new Jekyll site

Once you are setup you are ready to create a brand new Jekyll site. I have a folder called “Development” that I use to store all my projects. So I’ll cd to it and create my Jekyll site.

```bash
# create your new jekyll site
cd ~/Development
jekyll new test-blog
cd test-blog
bundle exec jekyll serve

# run it from your browser by typing this
127.0.0.1:4000
```

## Step 3: Create a new git repo and push it to Github

At this point you have your site. Now let’s turn it into a git repo and push it to Github.

```bash
# please note that you may need to run git config
# check this site for more info
# link --> https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup

# cd to the root of your project and do this
git init # initialize the repo
git add . # add all folders and files to the staging area
git commit -m "First commit" # commit all folders and files to the repo
git status

# now to to github.com and sign in
# if you don't have a github account then create one
# create a new repo with the same name as your project
# so for example this project is called test-blog
# now go back to your terminal in the root of your project and do this
# mine is TechSnazzy but yours is whatever your github is called
git remote add origin https://github.com/TechSnazzy/test-blog.git
git branch -M main
git push -u origin main

# now go back to your github page and refresh the browser and you'll see your files have been uploaded

# now you will need to create a gh-pages branch for your project to work
# from the terminal go back to the root of your project
git checkout -b gh-pages
git add .
git commit -m "Created gh-pages branch"
git push --set-upstream origin gh-pages
git status

# now to back to your github repo and make sure the gh-pages branch is there
# then if you click settings > pages you will see that your site is now live
# however there is still work to do
```

## Step 4: Add content and style to your project

At this point you have a working project with git versioning and Github Pages working. So you are all set with the functionality. Now we need to configure the site and add some posts and you’ll be all set. 

You’ll need to first update your config file. Best way to do update your files is to open the project folder in VSCode. From there you can take a look at your `_config.yml` file. Here are the things you'll need to update.

```yaml
title: TechSnazzy Test-Blog # update this title to anything you want

description: >- # this means to ignore newlines until "baseurl:"
  Write any description you want here

baseurl: "test-blog" # the subpath of your site, e.g. /blog

url: "https://techsnazzy.com" # this is my domain which points to my github

# the default domain for github pages would be techsnazzy.github.io
# you can also update other things in this config file
# but the items above are most important
```

Then you’ll need some content. The content will be in the `_posts` directory. You may need to read up more on this but to get started here are the requirements:

- File format: [`2016-05-19-super-short-article.md`](http://2016-05-19-super-short-article.md/) (year-month-day-description.md)
- Post should contain front matter. Below is an example of a post with front matter.

```markdown
---
layout: post
title: "This post demonstrates post content styles"
categories: junk
author:
- Bart Simpson
- Nelson Mandela Muntz
meta: "Springfield"
---

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit.

## Some great heading (h2)

Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu.
```