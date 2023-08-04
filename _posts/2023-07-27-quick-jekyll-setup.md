---
layout: post
title: 'Quick Guide to Getting Up and Running with Jekyll'
date: 2023-07-27 10:30:00 -0700
categories: [Blog, Technology, Jekyll]
author: Sean Morrison
---

Here’s a quick guide on how I setup my Jekyll site and pushed it to Github to run as a Github Pages site. I’ll describe this step by step from scratch. I’ll also cover how to create some posts to get you started and even a little bit of how to work with git (more on git in another future post).

## Step 1: Check the Jekyll documentation and install packages

The first step is to check the documentation on the [Jekyll website here](https://jekyllrb.com/). You’ll need to determine whether you are on Windows, Mac or Linux and follow the steps accordingly. I have been working mostly on macOS and then I did a lot of work in Ubuntu as well. So most of my experience is with either of those. Getting setup is slightly different for both. But if you click on the [Jekyll Docs](https://jekyllrb.com/docs/) and read carefully you should have no problem getting setup.

This can also be done in Windows. However, I have tried doing this in Windows and find it to be a bit clunky. The irony here is that all the tools I am using (Github, VSCode, etc.) all seem to be Microsoft products. But I digress...

To test if you are setup with everything you need, check the versions of everything to make sure you have everything installed and up to date.

```bash
# all of these are requirements
ruby -v
gem -v
jekyll -v
bundler -v
git -v
```

## Step 2: Create a new Jekyll site

Now it's time to actually scaffold a new Jekyll site. I have a directory called `Development` that I use to store all my projects. So I’ll `cd` to it and create my Jekyll site.

```bash
cd ~/Development
jekyll new test-blog
cd test-blog
bundle exec jekyll serve
```

Once you do that, you can head over to your browser and type [127.0.0.1:4000](https://127.0.0.1:4000) and see if it's working.

If all goes well you'll see your new Jekyll site with the bare bones Minima theme. And don't worry you can customize Minima but we'll talk about all that another time. For now this is more of a high level getting started guide. And I'm writing this because everyone talks about how easy this is to setup but it took me awhile to get familiar with everything and start to understand how this all works. So I want to share because everything I read always left things out. So I want to write something that will show how to really get started. But again, I digress...

## Step 3: Create a new git repo and push it to Github

At this point you have your site. Now let’s turn it into a git repo and `git push` it to Github. If you have never run `git config` on your computer then you'll need to first do a little bit of setup. Please read this [first time git config setup guide](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup) and make sure you can `git push` your git repo to your GitHub site. This also means you'll need a Github site. So if you haven't already then sign up for that by going to [github.com](https://www.github.com).

Once you verify that you can do that then please follow these steps to push your repo to Github.

From your terminal on your computer `cd` to your project and do this...

```bash
git init # initialize the repo
git add . # add all folders and files to the staging area
git commit -m "First commit" # commit all folders and files to the repo
git status
```

Now go to Github and create a new repo that has the same name as your project. So for example, if your repo on your local computer is called, `test-blog` then create a new repo in Github called `test-blog`. Once you create the new repo it will ask you to enter these commands. So go back to your terminal and `cd` to your local repo and run these commands to push your repo to Github.

```bash
git remote add origin https://github.com/TechSnazzy/test-blog.git
git branch -M main
git push -u origin main
```

Now go back to your Github page and refresh the browser and you'll see your files have been uploaded. So at this point you should have your local repo, it's pushed to your Github and everything is in the `main` branch. But for this to work in Github Pages, the branch needs to be called `gh-pages`. Here's how to take care of that.

```bash
git checkout -b gh-pages
git add .
git commit -m "Created gh-pages branch"
git push --set-upstream origin gh-pages
git status
```

Now head back to your Github repo and make sure the `gh-pages` branch is there. Go ahead and switch to the `gh-pages` branch. Then click on settings > pages you will see that your site is now live. Yay! However there is still work to do. The last step is to work with the config file and create some posts.

## Step 4: Edit the config file and add some posts

At this point you have a working project with git versioning and Github Pages working. So you are all set with the functionality. You'll be able to easily create new posts and push them to your site. Now we need to configure the site and add some posts and you’ll be all set.

You’ll need to first update your config file. You can do that by opening the folder in your favorite text editor. Personally, I mostly use vscode. From there you can take a look at your `_config.yml` file. Here are the things you'll need to update.

This will be the title you'll see in the header of your blog.

```yaml
title: TechSnazzy Blog
```

Here you can write anything you want. This section will show up in the footer in the lower right when using the Minima theme.

```yaml
description: >- # this means to ignore newlines until "baseurl:"
  Write any description you want here
```

This line is very important. So my site is [https://www.techsnazzy.com/sean-blog/](https://www.techsnazzy.com/sean-blog/). The `baseurl` defines the `sean-blog` portion of that.

```yaml
baseurl: 'test-blog' # the subpath of your site, e.g. /blog
```

In fact the url will be your website url. By default mine would be [https://TechSnazzy.github.io](https://TechSnazzy.github.io) but what you can do is register a domain and point it to your Github Pages site. My domain was previously registered with Google Domains but recently I moved it to Namecheap. And I use CloudFlare as my DNS provider. So now my site is [https://www.techsnazzy.com](https://www.techsnazzy.com) instead of [https://TechSnazzy.github.io](https://TechSnazzy.github.io). Again, more on this in another future post.

```yaml
url: 'https://techsnazzy.com'
```

Please note that when you are testing your site on your local computer with the `bundle exec jekyll serve` command then you'll want to leave the `baseurl` and `url` attributes blank.

Here's an example of how I do it. Curretly the "Local" is uncommented which means I'm running things locally. If I am ready to `git push` them I'll comment out the two lines in `# Local` and uncomment the two lines in `# Github`.

```yaml
# Local
baseurl: ''
url: ''
# GitHub
# baseurl: "sean-blog"
# url: "https://techsnazzy.com"
```

Then you’ll need some content. The content will be in the `_posts` directory in the form of markdown files. The file format should look like this [`2016-05-19-super-short-article.md`](http://2016-05-19-super-short-article.md/) (year-month-day-description.md). Also, the post should contain [front matter](https://jekyllrb.com/docs/front-matter/). Below is an example of a post with front matter. The front matter is some yaml code that gives the post instructions. For example, the front matter gives the layout which is define as either a post, page, etc. It also has a title and the date along with categories, author and meta data. Then below that is some [markdown code](https://www.markdownguide.org/getting-started/) which includes some headings and paragraph content.

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

Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce bibendum neque eget nunc mattis eu sollicitudin enim tincidunt. Vestibulum lacus tortor, ultricies id dignissim ac, bibendum in velit.

## Some great heading

Proin convallis mi ac felis pharetra aliquam. Curabitur dignissim accumsan rutrum. In arcu magna, aliquet vel pretium et, molestie et arcu.
```

Finally, once you are done creating your post you can git push it and then go check it out on your site. With any luck you have a new Jekyll site and happy blogging to you!
