---
layout: post
title: "Running Jekyll Site Locally and on GitHub"
date:   2023-08-03 10:00:00 -0700
categories:
- Blog
- Technology
- Jekyll
- Git
author: Sean Morrison
---

I've been working on learning how to build a Jekyll site for awhile now and I've learned quite a lot. In fact I'm starting to document what I've learned here. That said, one thing that has been baffling me is how to run Jekyll both locally and from Github after I've pushed an update.

Until now, I've been using the code below. I'd comment out the Local code if I'm pushing it to Github and then comment out Github if I'm running it locally.

I do this  if I push to Github...
```yaml
#Local
# baseurl: ""
# url: ""

# GitHub
baseurl: "sean-blog"
url: "https://techsnazzy.com"
```

And I do this if I'm running it locally...
```yaml
#Local
baseurl: ""
url: ""

# GitHub
#baseurl: "sean-blog"
#url: "https://techsnazzy.com"
```

You can see how tedious that could get. But then ChatGPT gave me a great suggestion. Here's what I did:

1. Leave the `_config.yml` file as it is with the Local code commented out.
2. Create another file called `_config_dev.yml` that has the Local code uncommented.
3. This way when I push an update it's using the default `_config.yml` file.
4. But when I run it locally the config dev file takes over.

Now I don't have to keep commenting or uncommenting. Yay!

```bash
bundle exec jekyll serve --config _config.yml,_config_dev.yml
```