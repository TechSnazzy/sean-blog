---
layout: post
title: 'Github, Namecheap and Cloudflare Config'
date: 2023-08-07 10:00:00 -0700
categories: [Blog, Technology, Git, Website]
author: Sean Morrison
---

Hey there! Let's dive into the world of web hosting and domain management that I'm dealing with. If you've ever wondered how websites get set up, here's a sneak peek into my setup with GitHub and more!

### GitHub Pages

My website is hosted on [GitHub Pages](https://pages.github.com/), and I've got a few different types of pages:

1. **Organization Page**: [TechSnazzy.github.io](https://TechSnazzy.github.io) - This is the hub for everything related to TechSnazzy on GitHub.
2. **Project Page**: [TechSnazzy.github.io/sean-blog](https://TechSnazzy.github.io/sean-blog) - Like this blog right here! You can have multiple project pages, but only one organization or user page.

### Custom Domains

I've also ventured into the domain registration world:

- **[techsnazzy.com](https://techsnazzy.com)**: This is my main business landing page. Feel welcome to explore!
- **[seanmorrison.dev](https://seanmorrison.dev)** and **[seanmorrison.cloud](https://seanmorrison.cloud)**: My playground domains, both pointing to my blog.

Oh, and since Google stepped away from domain registration, I had to move my domains elsewhere.

### DNS Configuration with Cloudflare

Managing domains leads us to the DNS topic. Without diving too deep, I use Cloudflare (it's free!) to handle DNS. Here's how I've set things up:

1. **For [techsnazzy.com](https://www.techsnazzy.com)**:
    - It points to my GitHub organization page and is configured with Microsoft 365.

2. **For .dev and .cloud domains**:
    - On Namecheap, I select "Custom DNS" and input Cloudflare's name servers.
    - Over in Cloudflare, I add a placeholder IP address.
    - Then I create a forwarding rule that takes any visitors to seanmorrison.cloud and redirects them right to [my blog](https://www.techsnazzy.com/sean-blog).

By following these steps, I've connected everything together, from Namecheap to Cloudflare, and then to my blog. Easy peasy!

### Wrap Up

So, that's a quick tour of how I manage my web presence. From hosting on GitHub to playing around with different domains and working with DNS settings, it's an exciting digital playground. Stay tuned for more details in future posts! Feel free to drop a visit to my [TechSnazzy website](https://www.techsnazzy.com)! 🚀
