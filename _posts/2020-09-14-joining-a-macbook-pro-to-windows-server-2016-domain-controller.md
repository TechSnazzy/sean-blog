---
layout: post
title: "Joining a MacBook Pro to Windows Server 2016 Domain Controller"
date: 2020-09-14 10:00:00 -0700
categories: blog javascript
author: Sean Morrison
---

Now that my blog is setup and my planning is complete, I decided to get started building my small Active Directory network.

### Joining a MacBook Pro to Windows Server 2016 Domain Controller

Now that my blog is setup and my planning is complete, I decided to get started building my small Active Directory network.

The first thing I did was build out a really small network with just two computers. I wanted to build out a **Windows Server 2016 domain controller** on an **Intel NUC 5i5RYB** and then bind a **MacBook Pro 13** laptop client running Catalina to it. These are the items I had to work with for now.

![](https://cdn-images-1.medium.com/max/800/1*OU2yct7MeaQeWfXLvVRR2w.jpeg)To do this, I first did some research and ended up referring to the these pages on the Internet. I didn’t exactly follow those pages but I did get some interesting things to work on from each page.

* [How to join a Mac in Microsoft Active Directory?](https://www.blackvoid.club/how-to-join-a-mac-in-microsoft-active-directory)
* [How to enable Integrated Authentication on macOS and Linux using Kerberos](https://github.com/Microsoft/vscode-mssql/wiki/How-to-enable-Integrated-Authentication-on-macOS-and-Linux-using-Kerberos)
* [Configure domain access in Directory Utility on Mac](https://support.apple.com/guide/directory-utility/configure-domain-access-diru11f4f748/mac)

However, after going through those pages I still could not get the Mac to join the domain using the GUI. It was pretty frustrating because I was hoping for it to “just work”.

However, this story has a happy ending. I finally got it join very easily using a command on the terminal.

This is an example of the command:


```
dsconfigad -preferred adserver.example.com -a <computername> –domain example.com -u administrator -p <password>
```
And this is the actual command I ran for my specific network:


```
dsconfigad -preferred server.techsnazzy.local  -a seanmbp13 -domain techsnazzy.local -u administrator -p <password>
```
When I was done, I had the green light of success. Joy! 🎉

![](https://cdn-images-1.medium.com/max/800/1*WZMsVjfW0uweY0G_Xtgi0g.png)So the lesson I learned here is to just run the command rather than deal with the GUI. I’ll have to dive in deeper to find out why the GUI doesn’t work. Also, before I had success with the terminal, I did some other things.

* On the MacBook Pro I disabled wireless and configured a manual IP address on the wired network port.
* I also manually added the DNS addresses of `8.8.8.8` and `8.8.4.4`. There are others but I like using these Google addresses.
* And just for good measure, I manually entered the WINS server address into the network settings.
* I also attempted to configure it through the **Directory Utility** GUI but had little success.
* Finally, as I noted earlier, configuring with the CLI above worked best.

Next up, I will configure a group of three Windows servers using VirtualBox on my MacBook Pro 16.

---
*Please note I originally posted this on my [Medium](https://medium.com/@seanmorrison) blog. I am currently in the process of moving all my writings and any documentation I've ever written to here.*