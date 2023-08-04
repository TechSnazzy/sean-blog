---
layout: post
title: 'Create a Windows Server 2016 Active Directory Domain in VirtualBox'
date: 2020-09-17 10:00:00 -0700
categories: [blog, javascript]
author: Sean Morrison
---

After my success with binding an old MacBook Pro running Catalina to a physical Windows Server 2016 AD environment, I decided to move forward to bigger things.

I have a **MacBook Pro 16** with 32GB of RAM and a fast GPU and I9 processor, I knew I could just build out my environment of **Windows Server 2016** servers in **VirtualBox** on it. So I did.

First, I went ahead and installed **VirtualBox** and then installed three Windows Server 2016 guest servers. It all went pretty well and I got it setup pretty fast.

![]({{ site.url }}/{{ site.baseurl }}/assets/images/1_8UjKmjWbGybVg3CUrsQDRg.png)

Right after I built up my servers, I ran into an issue. I couldn’t get a network connection over the wireless on the host. In other words, my Mac host was on wireless and I couldn’t get the network interfaces on the guests to ping the host or gateway. To fix this, the host will need to be connected to a wired network.

![]({{ site.url }}/{{ site.baseurl }}/assets/images/1_8gzH0HwGCR2nZFnVDgFwGg.jpg)

**Note**: I’m not sure why I need to be on a wired network in VirtualBox rather than wireless in order for guests to ping things outside of the host or each other. But being on the wired network is the only way I can get it to work. I will definitely research and dive into that topic in another post someday.

Anyway, this should be an easy fix right? Just plug in a Cat 5 cable and move on to bigger and better things. Wrong — Not that simple in this case. This MacBook Pro doesn’t have an Ethernet port. All it has are 4, USB-C ports.

To work around this, I needed an adapter so I could get wired network connectivity.

First, I found this [TP-Link adapter on Amazon](https://www.amazon.com/gp/product/B00YUU3KC6/ref=ppx_yo_dt_b_asin_title_o04_s00?ie=UTF8&psc=1). It goes from Ethernet to USB. Great! But my Mac still doesn’t have USB.

Next, in order to adapt from USB to USB-C, I used my [Anker USB hub](https://www.amazon.com/gp/product/B07YZ48HCT/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1).

![]({{ site.url }}/{{ site.baseurl }}/assets/images/1_gQwBGSD2dllRc7Yv9Ox2mg.jpg)

**Side note**: To be clear, I am not advertising any products. I’m just listing the items I am using for reference.

After all that adapting, I now have a disabled wireless network port and an enabled wired port with a manually assigned IP address + DNS and 3 identical Windows servers named DC-1, DC-2 and DC-3 and all of them can ping each other, the host and any other nodes on the network. Great!

In my next post, I will talk about creating a new domain with my small group of Windows servers and then connect some clients.

---

_Please note I originally posted this on my [Medium](https://medium.com/@seanmorrison) blog. I am currently in the process of moving all my writings and any documentation I've ever written to here._
