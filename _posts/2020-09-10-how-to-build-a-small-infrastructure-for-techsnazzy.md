---
layout: post
title: 'How to Build a Small Infrastructure for TechSnazzy'
date: 2020-09-10 10:00:00 -0700
categories: [infrastructure, windows, macos, active directory]
author: Sean Morrison
---

A recent objective I embarked upon was to explore and potentially construct a modern IT infrastructure suitable for a small business. This is planned to be a long-term, ongoing project. I will undertake this initiative from my home, utilizing the resources I have, including on-premises servers, various cloud platforms, mobile devices, and more. A detailed list can be found below.

![1_cX0FFOZ_dKpnHfgRLnTWdQ.jpg]({{ site.url }}/{{ site.baseurl }}/assets/images/1_cX0FFOZ_dKpnHfgRLnTWdQ.jpg)

In my current role as an IT HelpDesk for a medium-sized company, I contract full time through my company, [TechSnazzy, LLC](https://www.techsnazzy.com). I established [TechSnazzy](https://www.techsnazzy.com) to carry out IT contract work, but it also serves as a platform for other pursuits like Front-End Web Development (though I'm still learning in this area). My primary focus, for now, is on IT.

![1_8N13gRUK6uzC_R5rkKentw.png]({{ site.url }}/{{ site.baseurl }}/assets/images/1_8N13gRUK6uzC_R5rkKentw.png)

During the pandemic, most of my work has been remote, with occasional trips to the office. My tasks include providing remote support mainly for Windows users, but I also deal with a few Macs, several iOS devices, some Android, and a smattering of Linux support.

Over recent years, I've noticed a preference for Mac among many tech and software development companies. This has spurred my interest in learning more about Mac systems and enhancing my skills in that domain.

![1_dkz0QLgAPzbeRpysL9tR0w.jpg]({{ site.url }}/{{ site.baseurl }}/assets/images/1_dkz0QLgAPzbeRpysL9tR0w.jpg)

Initially, I'll set up a small infrastructure for [TechSnazzy](https://www.techsnazzy.com), comprising Windows Server 2016 domain controllers to manage Active Directory, DNS, and DHCP. I'll also integrate Windows and Mac clients into this network.

Some thoughts and queries have arisen, such as:

- How do non-Windows clients join an Active Directory domain?
- Is it possible for those clients to be mobile?
- What strategies exist for managing mobile devices and app installations?
- What are the best practices for data backup and device security?
- How can users access resources?

The only way to answer these questions is to dive in and learn.

![1_Wn-jvUStWnEL6i9tT8IjWg.jpg]({{ site.url }}/{{ site.baseurl }}/assets/images/1_Wn-jvUStWnEL6i9tT8IjWg.jpg)

#### List of Items to Learn or Build

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

With this comprehensive list of focus areas to explore and develop, I must also generate a list of tangible steps to commence this journey. I'll be documenting my progress, so expect to see plenty of Medium posts and social media updates on this topic.

Here's a preliminary list of To-Do items to get started:

- Decide between building a physical LDAP server or using a VM, considering the available hardware, such as an Intel NUC 5i5RYB.
- Begin crafting Medium posts.
- Engage with the TechSnazzy community on Twitter, IG, and Facebook.

This exciting project isn't just about building technical skills and understanding. It's also about sharing knowledge, fostering community, and discovering innovative ways to address common IT challenges. Here's how I plan to proceed:

### Building the Infrastructure

Constructing a modern IT infrastructure requires thoughtful planning and precise execution. My initial focus will be on the following:

1. **Assessing Needs and Resources**: Evaluating the available hardware and software, as well as identifying the specific needs of the small business environment I aim to emulate.

2. **Creating a Virtual Environment**: Utilizing tools like VMWare and Virtualbox to simulate a real-world network environment, where different server OS and client OS can interact.

3. **Implementing Security Measures**: Ensuring that all devices and data are protected through robust security protocols, including MFA and SSO.

4. **Networking**: Planning both wired and wireless networking, keeping in mind the need for efficiency and security.

5. **Managing Devices and Users**: Using LDAP, Active Directory, and MDM solutions to manage user access and mobile device usage.

6. **Data Management**: Implementing file storage, file sharing, and backup strategies, possibly utilizing Veeam for backups.

7. **Communication and Collaboration Tools**: Exploring options for meeting platforms, telephone systems, and ticketing solutions.

### Learning and Growth

While working on this project, continuous learning is vital. Here's how I plan to approach it:

- **Research**: Continuously seeking out information from reputable sources to understand best practices in IT.

- **Community Engagement**: Engaging with other IT professionals and enthusiasts, whether through social media, forums, or professional networks.

- **Hands-On Experimentation**: Learning by doing, including trying different configurations and troubleshooting issues as they arise.

- **Documenting the Journey**: Sharing the process through Medium posts and social media, allowing others to follow along, learn, and contribute their insights.

### Next Steps

With the plan laid out and a clear vision in mind, the next steps include:

- **Prioritizing Tasks**: Breaking down the project into manageable parts and prioritizing them.

- **Setting Milestones**: Creating realistic and achievable milestones to track progress.

- **Budgeting**: If additional resources are required, a clear budget will help guide purchasing decisions.

- **Collaborating**: Seeking collaboration and insights from others who have experience in the field can enhance the project's success.

- **Starting the Journey**: Finally, diving in, hands-on, with excitement and a readiness to learn and grow.

This project embodies more than a professional development endeavor. It's a challenge, an adventure, and an opportunity to connect with others who share similar passions.

Stay tuned to [TechSnazzy's Twitter](https://twitter.com/TechSnazzy), IG, and Facebook for regular updates, insights, and opportunities to engage in this fascinating journey.

Let the adventure begin!

---

_Please note I originally posted this on my [Medium](https://medium.com/@seanmorrison) blog. I am currently in the process of moving all my writings and any documentation I've ever written to here._
