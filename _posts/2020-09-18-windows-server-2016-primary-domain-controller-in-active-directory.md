---
layout: post
title: "Windows Server 2016 Primary Domain Controller in Active Directory"
date: 2020-09-18 10:00:00 -0700
categories: [infrastructure, windows, macos, active directory]
author: Sean Morrison
---

If you've been following my previous posts, you're aware that I've set up a cluster of virtual machines on my MacBook Pro 16. The primary goal? Setting up an Active Directory domain.

I currently have three servers operating with Windows Server 2016. For the time being, they're configured as member servers, labeled `DC-1`, `DC-2`, and `DC-3`. I've decided on a `192.168.0.x` network to maintain simplicity.

In this piece, I'll walk through adding the AD DS role to `DC-1`, which will be assigned an IP address of `192.168.0.5`. Its gateway is set to `192.168.0.1`.

> **Note**: Each virtual machine's NIC operates in bridged mode. Meanwhile, the host NIC connects via a dynamic LAN address. For a seamless experience, I've turned off the wireless NIC on the host.

While I won't dive deep into the intricate steps (as numerous detailed guides are available), consider this an overview of my setup journey.

Our first task? Install the AD DS role, then elevate `DC-1` to Domain Controller status.

![Image 1]({{ site.url }}/{{ site.baseurl }}/assets/images/1_zwsx0h6N_8N1PFgpadHS2g.png)

Given that this is our pioneer server, the creation of a new forest is mandatory.

The functional level selection is based on the oldest server version. For instance, if a 2008 server existed on this network, I'd opt for a 2008 functional level. But with a 2016 foundation, the default is optimal.

Additionally, this setup:
- Installs a DNS server,
- Functions as a Global Catalog server, and
- Generates a NetBIOS name. Ah, nostalgia!

![Image 2]({{ site.url }}/{{ site.baseurl }}/assets/images/1_D28Vflutqb4LPvTfKWAJpg.png)
![Image 3]({{ site.url }}/{{ site.baseurl }}/assets/images/1_o8R-OKoe3nptC1y8zWYgwg.png)
![Image 4]({{ site.url }}/{{ site.baseurl }}/assets/images/1_HhTkKTtmCkKnXx55FHR6Gw.png)

Following through with the subsequent prompts completes the installation.

Voila! Presenting an Active Directory domain named `techsnazzy.local` on a Windows Server 2016 domain controller.

![Image 5]({{ site.url }}/{{ site.baseurl }}/assets/images/1_my94UJkFgoS4EvTG6e2opA.png)
![Image 6]({{ site.url }}/{{ site.baseurl }}/assets/images/1_H1BBEmnoBcg9jT1tQO_lrA.png)

![1_OU2yct7MeaQeWfXLvVRR2w.jpg]({{ site.url }}/{{ site.baseurl }}/assets/images/1_OU2yct7MeaQeWfXLvVRR2w.jpg)

With everything in place, I'm now poised to create user accounts and integrate clients into this network.

---
*Please note I originally posted this on my [Medium](https://medium.com/@seanmorrison) blog. I am currently in the process of moving all my writings and any documentation I've ever written to here.*