---
layout: post
title: 'Setting Up Ubuntu 22.04 LTS with DLNA, Samba, Mounting External USB Disks, and RDP'
date: 2024-06-04 10:00:00 -0700
categories: [Blog, Technology, Git, Website]
author: Sean Morrison
---

In this guide, I'll walk you through setting up an Ubuntu 22.04 LTS system with the following features:

1. **DLNA server with MiniDLNA**: Allows you to stream media files to devices on your network.
2. **Samba for file sharing**: Facilitates file sharing between Linux and Windows systems.
3. **Mounting external USB disks**: Provides a way to access external storage devices.
4. **Remote Desktop Protocol (RDP) with GNOME**: Enables remote access to your Ubuntu desktop.

## 1. Setting Up DLNA Server with MiniDLNA

DLNA (Digital Living Network Alliance) allows you to stream media files like videos, music, and pictures to compatible devices within your home network. It's a great way to make your media library accessible on smart TVs, game consoles, and other media players.

**Step 1: Install MiniDLNA**

First, we need to install MiniDLNA, a lightweight DLNA server.

```bash
sudo apt update
sudo apt install minidlna
```

**Step 2: Configure MiniDLNA**

Next, we configure MiniDLNA to point to the directories where your media files are stored.

```bash
sudo vi /etc/minidlna.conf
```

In the configuration file, add the following lines to specify your media directories:

```plaintext
media_dir=V,/media/USB/MOVIES
media_dir=V,/media/USB/TV
media_dir=V,/media/USB/CONCERTS
media_dir=V,/media/USB/NFL
```

This setup ensures that MiniDLNA serves video files from the specified folders. You can add directories for music and pictures similarly.

**Step 3: Start and Enable MiniDLNA**

Finally, we restart the MiniDLNA service to apply the changes and enable it to start on boot.

```bash
sudo systemctl restart minidlna
sudo systemctl enable minidlna
```

## 2. Setting Up Samba for File Sharing

Samba allows you to share files between Linux and Windows systems. This is particularly useful in mixed-OS environments where you need seamless access to files from any device.

**Step 1: Install Samba**

First, we install the Samba package.

```bash
sudo apt update
sudo apt install samba
```

**Step 2: Configure Samba**

Next, we configure Samba by editing its configuration file to define our shared directories.

```bash
sudo vi /etc/samba/smb.conf
```

Add the following share definitions:

```plaintext
[FILES]
path = /media/FILES
browseable = yes
read only = no
writable = yes
valid users = sean
create mask = 0777
directory mask = 0777

[USB]
path = /media/USB
browseable = yes
read only = no
writable = yes
valid users = sean
create mask = 0777
directory mask = 0777
```

These settings create two shares: one for general files and another for USB storage, making them accessible over the network.

**Step 3: Set Permissions and Create Samba User**

Set the correct permissions for the shared directories to ensure they are accessible.

```bash
sudo chown -R sean:sean /media/FILES /media/USB
sudo chmod -R 0777 /media/FILES /media/USB
```

Add your user to Samba to manage access.

```bash
sudo smbpasswd -a sean
```

**Step 4: Restart Samba Service**

Finally, restart the Samba service to apply the changes.

```bash
sudo systemctl restart smbd
sudo systemctl enable smbd
```

## 3. Mounting External USB Disks

Mounting external USB disks allows you to use external storage devices seamlessly with your system, making it easier to manage large files and backups.

**Step 1: Identify USB Disk**

Identify your USB disk using the `lsblk` command.

```bash
lsblk
```

Assume it’s `/dev/sdb1`.

**Step 2: Create Mount Point**

Create a mount point for the USB disk.

```bash
sudo mkdir -p /media/USB
```

**Step 3: Configure fstab**

Get the UUID of the disk.

```bash
sudo blkid /dev/sdb1
```

Add the following line to `/etc/fstab`:

```plaintext
UUID=A1B2C3D4E5F67890  /media/USB  ntfs  defaults  0  0
```

Mount all filesystems.

```bash
sudo mount -a
```

This ensures the USB disk is mounted automatically on boot, making it always available without manual intervention.

## 4. Setting Up Remote Desktop Protocol (RDP) with GNOME

RDP allows you to access your Ubuntu desktop from another machine, such as a Windows PC, making remote management and access convenient.

**Step 1: Install XRDP**

Install the XRDP package.

```bash
sudo apt update
sudo apt install xrdp
```

**Step 2: Configure XRDP to Use GNOME**

Create or edit the `.xsession` file to use the GNOME session.

```bash
echo "gnome-session" > ~/.xsession
```

Edit the `/etc/xrdp/startwm.sh` file.

```bash
sudo vi /etc/xrdp/startwm.sh
```

Ensure the file contains the following:

```bash
#!/bin/sh
if [ -r /etc/profile ]; then
    . /etc/profile
fi

if [ -r ~/.profile ]; then
    . ~/.profile
fi

# start GNOME
export DESKTOP_SESSION=gnome
export XDG_SESSION_DESKTOP=gnome
export XDG_CURRENT_DESKTOP=GNOME
export GNOME_SHELL_SESSION_MODE=ubuntu
export XDG_SESSION_TYPE=x11
export GDMSESSION=ubuntu
unset DBUS_SESSION_BUS_ADDRESS

exec /usr/libexec/gnome-session-binary --session=ubuntu
```

This setup ensures that when you connect via RDP, you get a GNOME desktop session.

**Step 3: Allow RDP Through the Firewall**

Allow RDP connections through the firewall.

```bash
sudo ufw allow 3389/tcp
```

**Step 4: Restart and Enable XRDP Service**

Restart the XRDP service and enable it to start on boot.

```bash
sudo systemctl restart xrdp
sudo systemctl enable xrdp
```

## Connecting from Windows

1. **Open Remote Desktop Connection:**
   Open the Remote Desktop Connection application on your Windows 11 machine.

2. **Enter the IP Address:**
   Enter the IP address of your Ubuntu machine (e.g., `192.168.0.115`) and click "Connect."

3. **Log In:**
   Use your Ubuntu username and password to log in.

---

This completes the setup of your Ubuntu 22.04 LTS system with DLNA, Samba, mounting external USB disks, and RDP. You should now have a fully functional media server and remote desktop setup!

