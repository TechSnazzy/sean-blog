---
layout: post
title: 'Hosting with GitHub and Managing Domains: A Guide'
date: 2023-08-07 10:00:00 -0700
categories: [Blog, Technology, Git, Website]
author: Sean Morrison
---

GitHub provides three primary types of web hosting: personal pages, organization pages, and project pages. While there are private pages available too, that's a topic for another day. In this post, we'll dive into how these pages work and how I manage my domains using Cloudflare.

### **1. GitHub Organization Page**

You can have one personal or organization page per GitHub account and multiple project pages. My GitHub organization page is hosted at [TechSnazzy.github.io](https://TechSnazzy.github.io), serving as a primary landing page for my TechSnazzy business.

### **2. GitHub Project Page**

Project pages, on the other hand, host individual projects or blogs. My blog, for instance, is a project page hosted at [TechSnazzy.github.io/sean-blog](https://TechSnazzy.github.io/sean-blog). In the future, I plan to move away from the default GitHub Pages domain name and use my custom domain.

## **Domain Registration and Management**

After initially registering my domain with Google Domains, I moved to another provider due to Google's decision to discontinue domain registration services. Here's a quick look at my domains:

- [https://techsnazzy.com](https://techsnazzy.com): My main business domain, pointing to my GitHub organization page.
- [https://seanmorrison.dev](https://seanmorrison.dev) and [https://seanmorrison.cloud](https://seanmorrison.cloud): These playful domains were registered during different stages of learning and creativity. They both point to my blog.

## **DNS Configuration**

While I'll leave the in-depth DNS configuration for another post, let's take a quick look at how I point my .dev and .cloud domains to my blog (project page).

I manage my DNS through Cloudflare, a robust and free solution for my needs. For example:

- My [techsnazzy.com](https://www.techsnazzy.com) site is configured to direct to my GitHub organization page, integrated with Microsoft 365.
- The .dev and .cloud domains direct to my blog, and here's how I set that up:

### **Steps to Point Domains to Blog**

1. **Namecheap Configuration**
   - Navigate to the domain list.
   - Locate `seanmorrison.cloud` domain and click manage.
   - Go to Name servers, choose "Custom DNS."
   - Enter `aragorn.ns.cloudflare.com` and `rita.ns.cloudflare.com` as the name servers and save.

2. **Cloudflare Configuration**
   - Navigate to the DNS tab.
   - Add an A record with the placeholder IP address `192.0.2.1`.
   - Head over to the Rules tab.
   - Create a new rule with the URL `seanmorrison.cloud/*`, set it as a Forwarding URL with a 301 Permanent Redirect Status, and set the destination URL as `https://www.techsnazzy.com/sean-blog`.

Voila! This tells Namecheap about Cloudflare, and then Cloudflare redirects any traffic going to `seanmorrison.cloud` to my blog. It's simple, efficient, and opens the door to countless possibilities in web hosting and domain management.
