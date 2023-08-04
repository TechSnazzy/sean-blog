---
layout: post
title: 'How to Build a Small Infrastructure for TechSnazzy'
date: 2020-09-10 10:00:00 -0700
categories: [infrastructure, windows, active directory]
author: Sean Morrison
---

A recent goal I set was to see if I could build out (or at least learn how to build out) a modern computer infrastructure for a small business. This will be a long-term, ongoing work in progress. I will do this from home using the resources I have. This would include on-prem servers, some cloud resources, mobile and other things. I have created a more comprehensive list below.

![](/assets/images/1_cX0FFOZ_dKpnHfgRLnTWdQ.jpg)

In my day to day job, I am an IT HelpDesk at a medium-sized company. I contract full-time through my [TechSnazzy, LLC](https://www.techsnazzy.com) company. I created [TechSnazzy](https://www.techsnazzy.com) so that I could do this sort of IT contract work. I also use it as an umbrella to do other things such as Front-End Web Development (currently still in a learning mode though). For now, I will be focusing mostly on IT.

![](/assets/images/1_8N13gRUK6uzC_R5rkKentw.png)

During the pandemic I have done most of my work from home with an occasional trip to the office. At my current company, most of my work is to provide remote support for Windows users. However, there are some Macs, many iOS devices, some Android and a bit of Linux to support as well.

Over the last decade or so, I have noticed that many high-tech and software development companies seem to prefer Mac. Because of that, I have been wanting to learn more about how that works build up my skills in that area.

![](/assets/images/1_dkz0QLgAPzbeRpysL9tR0w.jpg)

First, I will build out a small infrastructure for [TechSnazzy](https://www.techsnazzy.com). I will create a group of Windows Server 2016 domain controllers that will handle Active Directory, DNS and DHCP. Then I will join Windows and Mac clients to that network.

As I’ve been thinking about this, I came up with some questions. For example,…

- How do non-Windows clients join an Active Directory domain?
- Can those clients be mobile?
- What are some ways to manage mobile devices and the apps that get installed?
- What can I use to backup data and secure the devices?
- How can users access resources?

There is only one way to answer these questions so it’s time to dive in.

![](/assets/images/1_Wn-jvUStWnEL6i9tT8IjWg.jpg)

#### List of Items to Learn or Build

- Server OS (Windows, Mac, Ubuntu, CentOS)
- Virtualization (VMWare, Virtualbox)
- Virtual Private Server (VPS)
- DNS
- DHCP
- Application Suite (GSuite, O365)
- Client OS Deployment (MDT)
- Deploy Updates (SCCM)
- User and Group Accounts
- User and Group Access
- LDAP (Active Directory, OpenLDAP)
- MDM (Jamf Pro)
- MFA
- SSO
- Networking
- Security
- Meetings
- Telephone
- Ticketing
- File Storage
- File Sharing
- Backups (Veeam)
- Networking (Wired, Wireless)

Now that I have a list of focus areas to learn and build out, I also need to come up with a list of things to start working on. As I go through this, I will be documenting everything I do. So there will be plenty of Medium and social media posts about all this.

That said, here’s my list of To Do items get started…

- Build physical LDAP server. Or would VM be better? The hardware I have to use is an Intel NUC 5i5RYB.
- Start writing Medium posts.
- Post to TechSnazzy Twitter, IG and Facebook.

---

_Please note I originally posted this on my [Medium](https://medium.com/@seanmorrison) blog. I am currently in the process of moving all my writings and any documentation I've ever written to here._
