---
layout: post
title: Ubuntu 18.04 Install Guide
date: 2019-02-11 00:00:00 -0000
image: ubuntu-1804.png
tags: [software]
---

I use Ubuntu 18.04 LTS on my laptop its a fantastic OS for general use. 
Like any good engineer I appreciate (semi)frequent maintenance, so I do a fresh reinstall of my OS and system software 
every few months. I made my own guide with the bash scripts and host it here so I can access it from my freshly installed OS.

# Steps
<ol>
    <li>Back up files</li>
    <li>Make sure back ups work</li>
    <li>Make boot USB thumb drive with OS image</li>
    <li>Boot from USB drive</li>
    <li>Install OS</li>
    <li>Configure OS</li>
    <li>Install software</li>
</ol>

## 1. Back up files

My important files are stored on remote servers and backed up on local external drives to avoid lossing anything.

## 2. Make sure back ups work
<p>
    It may seem obvious but its worthwhile to actually test that your most important files actually are backed up and didn't get corrupted or become otherwise inaccessible. I tend to just make important directories are the same size and try opening a few random files, or a few particular very important ones.
</p>

## 3. Make boot USB thumb drive with OS image

You can use any thumb drive with 2GB or more storage. See official tutorial on 
how to do this [here](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-ubuntu).

## 4. Boot from thumb drive

On Sager NP7851 I had an issue with the Nvidia drivers and GRUB settings similar to the bug reported [here](https://bugs.launchpad.net/ubuntu/+source/ubiquity/+bug/1767594).
The proposed fix did work for me:
1. Disable Fast Boot and Secure Boot (or Secure loader).
2. Plug in the bootable USB with the Linux distro (mine was Ubuntu 18.04)
3. When you see the loader to "Install Ubuntu" etc ... press "e" and edit a line: Replace "quiet splash" to "nomodeset" and press F10 to boot. Then after the installation is complete, you will have to reboot. 
4. This time you will now encounter the GRUB. Again, press "e" and edit a line: In the line that starts with "linux", add "nouveau.modeset=0" at the end of that line.

## 5. Install OS

You can now choose `Install Ubuntu` from the GRUB list and follow the install guide. You can also choose to encrypt your hard drive with a password. You do have to enter this password each time you boot up your computer and there is a performance hit however. Think carefully about using it. Follow the installation guide to configure users, passwords, and whatnot and you should have your new OS up and running soon.

## 6. Configure OS

Connect to your network now if you can because now is a good time to update your system:</p>
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt autoremove
```

Now intall the Ubuntu Restricted Extras for media codecs (.mp3 etc):

```bash
sudo apt install ubuntu-restricted-extras
```

### Disable touchpad with synclient

```
sudo apt-get install synclient
```
add this line to .bashrc: `synclient TouchpadOff=1`

### BIOS settings

Hit F2 to enter BIOS (should already know this) and select the XMP memory profile, enable fast boot, and the other chipset features 

### Remove GRUB boot delay

Edit the grub menu is found at: `/etc/default/grub `.
Set GRUB_TIMEOUT=0 to not show the menu and directly boot.
Run `sudo update-grub` to regenerate `/boot/grub/grub.cfg` based on the `/etc/default/grub` settings.

## 7. Install and configure software packages

These are my frequently used packages and by no means exhaustive. You can use 
the new Ubuntu Software application or the web and your own discretion to explore the vast ecosystem of available packages.

### Install build-tools and essential libraries

```bash
sudo apt-get install -y build-essential libssl-dev default-jdk curl vim git vlc 
shutter gimp firefox vifm
```

### Setup Git
Setup instructions [here](https://help.github.com/articles/set-up-git/#setting-up-git).

### Install i3wm

Instructions [here](https://i3wm.org/docs/repositories.html). Configuration from ~/.i3 (see [DotFiles](https://github.com/TStesco/DotFiles)). To solve issues with nautilus desktop window (if present)
```
gsettings set org.gnome.desktop.background show-desktop-icons false
```

### DotFiles

Clone [DotFiles repo](https://github.com/TStesco/DotFiles) and move .config files to user directory using rsync script: 

```bash
git clone https://github.com/TStesco/DotFiles.git
. rsync_src_to_dst.sh
```

Now do a reboot and log in with i3.

### Configure gnome terminal

Open default terminal which should be set in dotfiles (UXTerm). Select preferences 
as desired. I like to have the menu bar be hidden and use custom colours.

### tmuxinator

```bash
sudo apt-get install tmux
sudo gem install tmuxinator
```

Add the bash completion from: https://github.com/tmuxinator/tmuxinator/blob/master/completion/tmuxinator.bash

### Install Sublime Text 3

Follow package manager instructions [here](https://www.sublimetext.com/3). Add 
the package installer. 

### Install Anaconda

Get the latest installer version for your computer and version of Python 
[here](https://www.continuum.io/downloads#_unix)
```bash
bash "nameOfFile".sh
  ```

### Install Docker
The community edition is freely available here for all major
OS: [https://www.docker.com/community-edition](https://www.docker.com/community-edition)

### Install nvm
Node volume manager for node.js and npm. Use install script in the master repo:
 [https://github.com/creationix/nvm](https://github.com/creationix/nvm)

### Install Wine

```bash
sudo add-apt-repository ppa:ubuntu-wine/ppa
sudo apt-get update
sudo apt-get install -y wine1.7
```

Additional software packages seldom used: wireshark, nginx, arduino IDE 
