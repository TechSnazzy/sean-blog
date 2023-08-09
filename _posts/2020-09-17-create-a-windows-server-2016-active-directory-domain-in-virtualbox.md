---
layout: post
title: 'Create a Windows Server 2016 Active Directory Domain in VirtualBox'
date: 2020-09-17 10:00:00 -0700
categories: [blog, javascript]
author: Sean Morrison
---

After successfully binding an older MacBook Pro running macOS Catalina to a physical Windows Server 2016 Active Directory (AD) environment, I was eager to expand my knowledge and try my hand at something more complex.

I've been using a MacBook Pro 16, boasting 32GB of RAM, a high-performance GPU, and an Intel i9 processor. I realized that this machine could handle a set of Windows Server 2016 virtual servers on VirtualBox, so I decided to give it a shot.

I began by installing VirtualBox, followed by three Windows Server 2016 guest servers. The process went smoothly, and the setup was completed relatively quickly.

![1_8UjKmjWbGybVg3CUrsQDRg.png]({{ site.url }}/{{ site.baseurl }}/assets/images/1_8UjKmjWbGybVg3CUrsQDRg.png)

However, I soon encountered a network connection issue. Despite being connected to the wireless network on my Mac host, the guest servers couldn't communicate with the host or the gateway. To resolve this, I discovered that the host would need to connect to a wired network.

![1_8gzH0HwGCR2nZFnVDgFwGg.jpg]({{ site.url }}/{{ site.baseurl }}/assets/images/1_8gzH0HwGCR2nZFnVDgFwGg.jpg)

*Note:* The requirement for a wired network in VirtualBox rather than a wireless one for guest-to-guest and guest-to-external communication puzzled me. I intend to research this topic more thoroughly and will surely discuss it in a future post.

You might think the solution would be as simple as plugging in an Ethernet cable, but my MacBook Pro doesn't have a traditional Ethernet port, only USB-C ports. So, things were a bit more complicated.

I found a workaround by using an adapter to achieve wired network connectivity. I started with a [TP-Link adapter on Amazon](https://www.amazon.com/gp/product/B00YUU3KC6/ref=ppx_yo_dt_b_asin_title_o04_s00?ie=UTF8&psc=1) that goes from Ethernet to USB, and then used an [Anker USB hub](https://www.amazon.com/gp/product/B07YZ48HCT/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&psc=1) to adapt from USB to USB-C.

![1_gQwBGSD2dllRc7Yv9Ox2mg.jpg]({{ site.url }}/{{ site.baseurl }}/assets/images/1_gQwBGSD2dllRc7Yv9Ox2mg.jpg)

*Side note:* Just to clarify, I am not endorsing any specific products. I'm merely listing the items that I used for reference.

Once the adapters were connected, I successfully configured the network settings, manually assigned the IP address and DNS, and got my three Windows servers named DC-1, DC-2, and DC-3 to communicate with each other, the host, and other nodes on the network. Fantastic!

Stay tuned for my next post, where I'll discuss creating a new domain with this small group of Windows servers and connecting some clients. It's an exciting journey, and I look forward to sharing it with you!

---

_Please note I originally posted this on my [Medium](https://medium.com/@seanmorrison) blog. I am currently in the process of moving all my writings and any documentation I've ever written to here._
