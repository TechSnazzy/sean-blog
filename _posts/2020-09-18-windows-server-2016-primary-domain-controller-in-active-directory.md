---
layout: post
title: "Windows Server 2016 Primary Domain Controller in Active Directory"
date: 2020-09-18 10:00:00 -0700
categories: [blog, javascript]
author: Sean Morrison
---

If you’ve been reading along with my previous posts, you’ll know that I have created a small group of **virtual machine guests** on my **MacBook Pro 16** in order to create an **Active Directory domain**.

There are 3 servers running Windows Server 2016. They are member servers for now and are named **DC-1**, **DC-2** and **DC-3** respectively. I’m also keeping it simple with a **192.168.0.x** network.

For this topic, I will add the **AD DS** role to **DC-1**. It will have an IP address of **192.168.0.5**. The gateway will be **192.168.0.1**.

**Note**: Each guest NIC is running in **bridged mode** while the host NIC is wired with a dynamic address on the LAN. Also, I have disabled the wireless NIC on the host in order to keep things simple.

I won’t be going into too much detail here because there are plenty of step by step guides out there already. This is more of just an overview of what I am doing to get setup.

The first thing is to install the AD DS role and then promote **DC-1** to Domain Controller.

![](/assets/images/1_zwsx0h6N_8N1PFgpadHS2g.png)

And since this is the very first server, I will need to create a new forest.

I will also need to choose a functional level. If I had an old 2008 server on this network then I would create it with a 2008 functional level. But since it’s starting out with 2016, then I will just take the default choice.

This is also going to install a DNS server and will be a Global Catalog server.

It will also create a NetBIOS name for old times sake. Oh goodie!

![](/assets/images/1_D28Vflutqb4LPvTfKWAJpg.png)
![](/assets/images/1_o8R-OKoe3nptC1y8zWYgwg.png)
![](/assets/images/1_HhTkKTtmCkKnXx55FHR6Gw.png)

Once I am done, I follow the next default prompts and complete the installation.

And that’s it. I now have an Active Directory domain of **techsnazzy.local** on a Windows Server 2016 domain controller.

![](/assets/images/1_my94UJkFgoS4EvTG6e2opA.png)
![](/assets/images/1_H1BBEmnoBcg9jT1tQO_lrA.png)

At this point, I can create a user account and join a client to this network.

---
*Please note I originally posted this on my [Medium](https://medium.com/@seanmorrison) blog. I am currently in the process of moving all my writings and any documentation I've ever written to here.*