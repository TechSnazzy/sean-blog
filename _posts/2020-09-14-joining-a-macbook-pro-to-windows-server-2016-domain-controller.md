---
layout: post
title: 'Joining a MacBook Pro to Windows Server 2016 Domain Controller'
date: 2020-09-14 10:00:00 -0700
categories: [infrastructure, windows, macos, active directory]
author: Sean Morrison
---

Now that my blog is set up and I've mapped out my plans, I embarked on constructing my small Active Directory network.

I began by building a minimal network with just two devices. The setup included a Windows Server 2016 domain controller on an Intel NUC 5i5RYB and a MacBook Pro 13 laptop client running macOS Catalina that would be joined to it. These are the tools I had at my disposal.

![1_OU2yct7MeaQeWfXLvVRR2w.jpeg]({{ site.url }}/{{ site.baseurl }}/assets/images/1_OU2yct7MeaQeWfXLvVRR2w.jpeg)

To initiate this project, I engaged in some research, finding guidance on these online pages. While I didn't follow these references to the letter, they offered some valuable insights:

- [How to join a Mac in Microsoft Active Directory?](https://www.blackvoid.club/how-to-join-a-mac-in-microsoft-active-directory)
- [How to enable Integrated Authentication on macOS and Linux using Kerberos](https://github.com/Microsoft/vscode-mssql/wiki/How-to-enable-Integrated-Authentication-on-macOS-and-Linux-using-Kerberos)
- [Configure domain access in Directory Utility on Mac](https://support.apple.com/guide/directory-utility/configure-domain-access-diru11f4f748/mac)

Despite exploring these resources, I encountered a hurdle: I couldn't get the Mac to join the domain through the GUI. It was a perplexing challenge, given I expected it to "just work."

However, every story has its turning point. I discovered a simple terminal command that allowed the Mac to join the domain with ease.

Here's an illustrative example of the command:

```bash
dsconfigad -preferred adserver.example.com -a <computername> -domain example.com -u administrator -p <password>
```

And here's the specific command that succeeded on my network:

```bash
dsconfigad -preferred server.techsnazzy.local -a seanmbp13 -domain techsnazzy.local -u administrator -p <password>
```

Upon completion, I was greeted with a green light of success. Pure joy! 🎉

![1_WZMsVjfW0uweY0G_Xtgi0g.png]({{ site.url }}/{{ site.baseurl }}/assets/images/1_WZMsVjfW0uweY0G_Xtgi0g.png)

What I learned from this experience is that sometimes running a command can be more effective than wrestling with the GUI. I'll need to investigate further why the GUI option didn't work. Before finding success with the terminal, I also performed a few other configurations:

- On the MacBook Pro, I disabled wireless and manually configured an IP address on the wired network port.
- I manually added the DNS addresses `8.8.8.8` and `8.8.4.4`, with a preference for these Google addresses.
- For good measure, I manually entered the WINS server address into the network settings.
- I also attempted to configure it through the Directory Utility GUI, though without success.
- Ultimately, as mentioned earlier, the command-line interface proved to be the most efficient method.

Next on my agenda is configuring a group of three Windows servers using VirtualBox on my MacBook Pro 16. Stay tuned!

---

_Please note I originally posted this on my [Medium](https://medium.com/@seanmorrison) blog. I am currently in the process of moving all my writings and any documentation I've ever written to here._
