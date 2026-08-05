---
layout: post
title: 'Moving My Desktop from ZorinOS to Fedora 44'
date: 2026-08-05 10:30:00 -0700
categories: [Blog, Technology, Linux, Fedora]
author: Sean Morrison
---

I spent a weekend moving my main desktop off ZorinOS and onto Fedora 44 Workstation. This is the write-up of how that went: the backup, the install, the restore, getting NVIDIA configured, a monitor bug that had nothing to do with any of it, and finally getting my shell back to feeling like home. I'm writing this partly for myself, so future-me has a record of what was actually done and why, instead of a vague memory of "yeah I think I ran some rsync command."

## The machine

Nothing fancy, gaming-style computer:

- Fedora 44 Workstation (kernel `7.1.5-201.fc44.x86_64`)
- NVIDIA GeForce RTX 3060, running the proprietary driver, not nouveau
- GNOME on Wayland
- An LG 34" ultrawide monitor (3440x1440, 21:9) as the main display
- zsh with Oh My Zsh as the shell setup

## Why leave ZorinOS

ZorinOS had been fine for a long time, but the real reason for the move is that I've decided to pursue Red Hat certifications to get better with enterprise Linux. I recognize Ubuntu is probably the more well known and popular distro among end users in this space, but my focus going forward is on the server side of things, not the desktop side, and that points toward Red Hat's ecosystem instead. Fedora is the closest thing to RHEL without actually being RHEL, so reverting back to it now gets me working in that world day to day. I'll also be spending time directly in RHEL as I go through this process. Fedora's relationship with NVIDIA hardware isn't perfect, but it's well documented, and RPM Fusion makes the proprietary driver a known quantity rather than a guessing game. So the plan was: back everything up, wipe the drive, install Fedora 44 clean, then pull the important stuff back in.

## Step 1: backing up ZorinOS with rsync

Before touching partitions, I backed up the ZorinOS install to an external USB drive using rsync rather than a disk image. The reasoning was simple: I didn't need a bit-for-bit clone of a system I was about to replace, I needed the data and configuration that actually mattered, in a form I could selectively restore from later.

The backup covered two things specifically: `/etc` (system configuration) and my home directory, organized into its own folder on the drive rather than dumped as a raw `/home/sean`. On the USB drive those ended up as two top level folders, something like:

```
/run/media/sean/BACKUPDISK/etc
/run/media/sean/BACKUPDISK/home-organized
```

One detail worth remembering here, because it trips people up: on Fedora (and most modern distros), removable drives mount under `/run/media/<username>/<label>`, not `/run/media/<label>`. The username is always in the path. I've lost a few minutes to this exact mistake more than once.

The actual copy used rsync with archive mode plus flags to preserve hard links, ACLs, and extended attributes, since this was a full system backup and I wanted permissions and ownership to survive the trip:

```bash
sudo rsync -aHAX --info=progress2 /etc /run/media/sean/BACKUPDISK/
sudo rsync -aHAX --info=progress2 /home/sean/ /run/media/sean/BACKUPDISK/home-organized/
```

`-a` is archive mode (recursive, preserves permissions, timestamps, symlinks). `-H` preserves hard links. `-A` preserves ACLs. `-X` preserves extended attributes, which on a SELinux system includes the `security.selinux` context on every file. That last flag turned out to matter a lot later, but not during the backup itself, only when I tried to restore.

## Step 2: installing Fedora 44 Workstation

The install itself was the boring part, which is exactly what you want from an OS installer. Standard Fedora 44 Workstation image, wiped the target drive, default partitioning, GNOME desktop, done. No dual boot, no manual partition surgery, no drama. The interesting work started after first boot.

## Step 3: restoring files with rsync

With Fedora up and running, I plugged the USB drive back in and started pulling files back off it, one folder at a time rather than all at once, so I could actually watch what was happening instead of trusting a single giant transfer.

First attempt, copying `etc` back over, used the same flags as the original backup:

```bash
sudo rsync -aHAX --info=progress2 /run/media/sean/BACKUPDISK/etc /home/sean/Downloads/
```

This failed partway through with:

```
rsync error: some files/attrs were not transferred (see previous errors) (code 23) at main.c(1356) [sender=3.4.4]
```

Code 23 from rsync is intentionally vague, it just means "something didn't transfer, check the log," so I reran it with plain verbose output redirected to a file instead of the live progress bar (`--info=progress2` constantly rewrites one line, which turns into garbage once you redirect it to a file):

```bash
sudo rsync -aHAX -v /run/media/sean/BACKUPDISK/etc /home/sean/Downloads/ \
  > /home/sean/Claude/rsync-etc-log.txt 2>&1
```

The log came out at 472KB, too big to read start to finish, so I grepped it for anything that looked like an actual failure rather than scrolling:

```bash
grep -iE "error|denied|failed|cannot|no such|refused|rsync:" rsync-etc-log.txt \
  | sort | uniq -c | sort -rn | head -60
```

Every single hit was the same line, just with a different filename:

```
rsync: [receiver] rsync_xal_set: lremovexattr("/home/sean/Downloads/etc/...","security.selinux") failed: Permission denied (13)
```

That's the `-X` flag again. It tries to preserve the `security.selinux` extended attribute on every file, and SELinux blocks writes to that specific xattr unless the process holds a MAC-admin privilege that plain `sudo` doesn't grant. This isn't a bug in these specific folders, it will happen on any full-tree rsync with `-X` under enforcing SELinux on Fedora. Root doesn't automatically mean "can set arbitrary SELinux contexts."

The fix was to just drop `-X` for this copy. I wasn't restoring these files into their original system locations where matching SELinux contexts would matter, I was pulling them into `~/Downloads` for reference, where they'd get Fedora's normal default context regardless:

```bash
# etc
sudo rsync -aH -v /run/media/sean/BACKUPDISK/etc /home/sean/Downloads/ \
  > /home/sean/Claude/rsync-etc-log.txt 2>&1

# home-organized
sudo rsync -aH --info=progress2 /run/media/sean/BACKUPDISK/home-organized /home/sean/Downloads/
```

`-aH` still keeps permissions, ownership, timestamps, symlinks, and hard links, it just stops fighting SELinux over extended attributes. Both copies finished cleanly after that.

One side effect of running the copy under `sudo`: everything under `~/Downloads/etc` ended up owned by `root:root`. Nautilus shows a little padlock icon on folders like that, which looks alarming but just means my regular account has read and execute access without write access, not that anything's broken. Fixed with a straightforward chown once the copy was done:

```bash
sudo chown -R sean:sean /home/sean/Downloads/etc
sudo chown -R sean:sean /home/sean/Downloads/home-organized
```

From there I went through `home-organized` by hand and moved the pieces I actually wanted (dotfiles, project folders, SSH keys, that kind of thing) back into their real locations in `/home/sean`, rather than restoring the whole tree wholesale. Old home directories accumulate a lot of things you don't actually want to carry forward, and a fresh install is a good excuse to leave the rest behind.

## Step 4: getting the NVIDIA driver working

Fedora ships with the open source nouveau driver by default, and nouveau will get a desktop on screen, but it won't give you CUDA or full hardware accelerated OpenGL on an RTX card. Getting the proprietary driver installed and confirmed working went smoothly, though it helps to understand what "installed" versus "actually active" means on Fedora.

First, RPM Fusion's nonfree repo needs to be enabled, since that's what provides `akmod-nvidia`. With that in place:

```bash
sudo dnf install -y akmod-nvidia xorg-x11-drv-nvidia-cuda
```

`akmod-nvidia` doesn't ship a prebuilt kernel module, it builds one against whatever kernel you're currently running, in the background, via the `akmods` service. That build can take a few minutes, and if you reboot before it finishes, you're back on nouveau with no explanation why. So the thing to check before rebooting is whether the module actually built for your running kernel:

```bash
rpm -qa | grep nvidia
modinfo nvidia
```

`modinfo nvidia` should point at a `.ko` or `.ko.xz` file living under `/lib/modules/$(uname -r)/`. If `kmod-nvidia-$(uname -r)-...` isn't listed yet in the rpm query, the build just hasn't finished, wait and check again rather than assuming something's wrong.

The other piece that has to be in place is a nouveau blacklist on the kernel command line. The driver package's install script usually adds this automatically to `/etc/default/grub`:

```
GRUB_CMDLINE_LINUX="... rd.driver.blacklist=nouveau,nova_core modprobe.blacklist=nouveau,nova_core"
```

but `/etc/default/grub` is only a template. What the bootloader actually reads at boot time is the BLS entry under `/boot/loader/entries/*.conf`, and editing the template alone doesn't do anything until that's regenerated, or until you push the args in directly with `grubby`:

```bash
sudo grubby --update-kernel=ALL --args="rd.driver.blacklist=nouveau,nova_core modprobe.blacklist=nouveau,nova_core"
```

After a reboot (`sudo systemctl reboot`), I ran through a short checklist to confirm the proprietary driver was actually the one in use, not just installed alongside nouveau:

```bash
cat /proc/cmdline                     # should show modprobe.blacklist=nouveau,nova_core
lsmod | grep -E "nvidia|nouveau"      # nvidia present, nouveau absent
nvidia-smi                            # should report the GPU
lspci -k | grep -A3 VGA               # "Kernel driver in use: nvidia"
glxinfo | grep "OpenGL renderer"      # NVIDIA renderer, not Mesa/zink/NVK
```

All of that came back clean:

```
$ nvidia-smi --query-gpu=driver_version,name --format=csv
driver_version, name
610.43.03, NVIDIA GeForce RTX 3060
```

Worth noting: dracut is set up (via `/usr/lib/dracut/dracut.conf.d/99-nvidia-dracut.conf`) to deliberately leave the nvidia modules out of the initramfs. That's expected behavior, not a misconfiguration, the driver loads from userspace later in the boot process. No initramfs rebuild needed.

## Step 5: an unrelated monitor bug

Not part of the migration exactly, but it happened in the same window of getting the machine dialed in, so it's going in this write-up. My external LG 34" ultrawide monitor (3440x1440 native, 21:9) looked stretched no matter what resolution I picked in Settings. Turned out GNOME/Mutter was driving it at 1920x1080, a 16:9 resolution, and since the panel doesn't letterbox a mismatched aspect ratio, it just stretched the image horizontally to fill the full 21:9 width. Any 16:9 resolution produced the same stretch, which is why it looked like nothing I picked fixed it.

The monitor's EDID reports `4096x2160@24Hz` as its "preferred" mode and calls itself `LG SMART WQHD`, both of which are red herrings for what's actually a 34" ultrawide panel. I confirmed the real state with Mutter's D-Bus interface directly:

```bash
gdbus call --session --dest org.gnome.Mutter.DisplayConfig \
  --object-path /org/gnome/Mutter/DisplayConfig \
  --method org.gnome.Mutter.DisplayConfig.GetCurrentState
```

and set it to the correct native mode with 1.25x scaling (3440x1440 at 1.0x is uncomfortably small to read):

```bash
gdbus call --session --dest org.gnome.Mutter.DisplayConfig \
  --object-path /org/gnome/Mutter/DisplayConfig \
  --method org.gnome.Mutter.DisplayConfig.ApplyMonitorsConfig \
  1 2 \
  "[(0, 0, 1.25, uint32 0, true, [('HDMI-2', '3440x1440@49.987', @a{sv} {})])]" \
  "{}"
```

The `2` at the start selects persistent mode, which writes the result to `~/.config/monitors.xml` so it survives logout and reboot rather than only applying to the live session.

## Step 6: setting up zsh and Oh My Zsh

Bash is fine, but I've used zsh with Oh My Zsh for years and a fresh install isn't a good enough reason to switch. Installing it was routine:

```bash
sudo dnf install -y zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
chsh -s $(which zsh)
```

That drops a default `~/.zshrc` and an `~/.oh-my-zsh` directory with `custom/plugins` and `custom/themes` folders for anything not bundled with the core install. From there it was a matter of rebuilding my actual config rather than living with the defaults.

### Theme and plugins

I use the built in `gentoo` theme rather than the Oh My Zsh default, and only two plugins: `git` (for branch/status info in the prompt) and `zsh-autosuggestions`, which isn't bundled and has to be cloned in manually:

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions \
  ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
```

Once it's sitting in `custom/plugins/`, Oh My Zsh picks it up automatically as long as it's listed in the `plugins` array in `.zshrc`:

```bash
export ZSH="$HOME/.oh-my-zsh"
ZSH_THEME="gentoo"

plugins=(
  git
  zsh-autosuggestions
)

source $ZSH/oh-my-zsh.sh
```

### A custom prompt on top of the theme

The `gentoo` theme's default prompt is fine, but I override the git prompt segment colors and the whole `PS1` to get a specific look, blues and purples for the username, host, and current directory, with git status folded in wherever there's a repo:

```bash
ZSH_THEME_GIT_PROMPT_PREFIX="%{$(tput setaf 117)%}("
ZSH_THEME_GIT_PROMPT_SUFFIX="%{$(tput setaf 117)%}) "
ZSH_THEME_GIT_PROMPT_DIRTY="%{$(tput setaf 210)%}*"
ZSH_THEME_GIT_PROMPT_CLEAN=""

export PS1="%{$(tput setaf 39)%}%n%{$(tput setaf 45)%}@%{$(tput setaf 51)%}%m %{$(tput setaf 195)%}%1~ \$(git_prompt_info)%{$(tput sgr0)%}$ "
```

`tput setaf <n>` picks a 256 color palette entry rather than hardcoding raw ANSI codes, which makes each color easy to swap without decoding escape sequences by hand. `git_prompt_info` is a function Oh My Zsh's `git` plugin provides, and calling it inside `PS1` means the prompt only shows a git segment when the current directory is actually inside a repo.

### Recoloring the whole terminal when connecting over SSH

This is the part of my config I like most. When I SSH into this machine from somewhere else on the network, say from another box at `10.0.0.x`, I want the terminal to visually announce "you are on a remote connection" so I don't accidentally run something destructive on the wrong machine while on autopilot. `.zshrc` checks for `$SSH_CONNECTION`, which zsh sets automatically for any shell started over SSH, and if it's present, repaints the entire terminal color palette to a warm red/orange scheme using OSC escape sequences:

```bash
if [[ -n "$SSH_CONNECTION" ]]; then
  # Push hot (red/orange/yellow) colors to the remote terminal via OSC sequences
  printf '\e]11;#120800\e\\'   # background
  printf '\e]10;#ffcc88\e\\'   # foreground
  printf '\e]12;#ff6600\e\\'   # cursor
  printf '\e]4;0;#1a0800\e\\'  # black
  printf '\e]4;1;#ff3300\e\\'  # red
  printf '\e]4;2;#ff8800\e\\'  # green -> orange
  # ...and so on through all 16 palette slots

  ZSH_THEME_GIT_PROMPT_PREFIX="%{$(tput setaf 216)%}("
  ZSH_THEME_GIT_PROMPT_SUFFIX="%{$(tput setaf 216)%}) "
  ZSH_THEME_GIT_PROMPT_DIRTY="%{$(tput setaf 196)%}*"
  export PS1="%{$(tput setaf 196)%}%n%{$(tput setaf 202)%}@%{$(tput setaf 208)%}%m %{$(tput setaf 220)%}%1~ \$(git_prompt_info)%{$(tput sgr0)%}$ "
fi
```

`\e]11;...\e\\` and `\e]10;...\e\\` are OSC 10/11, which set the terminal's default foreground and background colors directly, and `\e]4;N;...\e\\` is OSC 4, which remaps palette slot `N` to a specific hex color. Any terminal emulator that supports these OSC sequences (most modern ones do) will pick this up the moment the shell prints it, no terminal side configuration required. The practical effect: local sessions on this desktop stay in cool blues, and the instant I'm working inside an SSH session on this box from somewhere else, everything shifts to warm orange, at a glance, no reading required.

### Aliases

A handful of aliases round out the config. Nothing fancy, mostly shortcuts for things I do often enough that typing them out fully got annoying:

```bash
alias ll="ls -lah"

alias vm='qemu-system-x86_64 -m 1024 -cpu pentium3 -hda /home/sean/VMs/winxp/winxp.qcow2 \
  -boot c -vga std -usb -device usb-tablet -netdev user,id=n1 -device rtl8139,netdev=n1 \
  -rtc base=localtime -display gtk,zoom-to-fit=on'
```

`vm` boots a small Windows XP virtual machine I keep around under QEMU, useful for the odd case where something only runs on ancient Windows. The `-cpu pentium3` and low memory allocation match what XP actually expects rather than throwing modern CPU features and RAM at an OS from 2001 that doesn't know what to do with either.

## Step 7: keeping backups going forward

Now that the machine is set up the way I want, I added an alias for ongoing backups to an external drive, rather than only backing up once during the migration and never again:

```bash
alias backup='mountpoint -q /media/sean/BACKUP && \
  rsync -aHAX --delete --info=progress2 /home/sean/ /media/sean/BACKUP/ || \
  echo "backup: /media/sean/BACKUP is not mounted, plug in the BACKUP drive first" >&2'
```

`mountpoint -q` checks first whether the drive is actually plugged in and mounted before doing anything, so a stray `backup` command with no drive attached fails with a clear message instead of either erroring out confusingly or, worse, silently doing nothing. `--delete` keeps the backup a mirror of the current home directory rather than an ever growing archive of files I've since removed. This time I kept `-X` in the flags, since this backup does need to preserve SELinux contexts, unlike the one time copy into `~/Downloads` for reference.

## Where things stand now

The desktop is fully on Fedora 44, running the proprietary NVIDIA driver with CUDA and hardware accelerated OpenGL confirmed working, the ultrawide monitor is displaying at its correct native resolution, and the shell feels like the same one I've been using for years, cool blue prompt locally, warm orange the moment I'm in over SSH. The whole migration came down to three tools doing almost all the real work: rsync for moving data both directions, dnf and RPM Fusion for getting the right driver installed, and a D-Bus call to Mutter for a display bug that had nothing to do with the migration but needed fixing anyway.

The main lesson worth carrying forward: when an rsync copy fails partway through with a vague error code, don't guess, redirect verbose output to a log file and grep it for the actual error lines. The real cause is usually one specific line repeated hundreds of times, not hundreds of different problems.
