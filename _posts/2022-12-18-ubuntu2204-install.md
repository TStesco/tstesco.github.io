---
layout: post
title: Ubuntu 22.04 Install Guide
date: 2022-12-18 00:00:00 -0000
image: ubuntu-22-04.png
tags: [software]
---

This is a guide with the shell commands for installing Ubuntu 22.04 it and customizing it.

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
It may seem obvious but its worthwhile to actually test that your most important files actually are backed up and didn't get corrupted or become otherwise inaccessible. I tend to just make important directories are the same size and try opening a few random files, or a few particular very important ones.

## 3. Make boot USB thumb drive with OS image

You can use any thumb drive with 4GB or more storage. See official tutorial on 
how to do this [here](https://tutorials.ubuntu.com/tutorial/tutorial-create-a-usb-stick-on-ubuntu).

## 4. Boot from thumb drive

Hit F2 during boot to enter BIOS. This key may be different on your machine, its usually tapping a function key repeatedly during boot before OS slpash screen comes up. Select option to boot from USB drive.

## 5. Install OS

You can now choose `Install Ubuntu` from the GRUB list and follow the install guide. Follow the installation guide to configure users, passwords, and whatnot and you should have your new OS up and running soon.

## 6. Configure OS

Connect to your network (if you havent already done so during install) to update your system:</p>
```bash
sudo apt update
sudo apt upgrade
sudo apt autoremove
```

Now intall the Ubuntu Restricted Extras for media codecs (.mp3 etc):

```bash
sudo apt install ubuntu-restricted-extras
```

### Resolve NVIDIA drivers issues

On Sager NP7851 I had an issue with the Nvidia drivers causing external monitor to not match framerates selected.
https://bugs.launchpad.net/ubuntu/+source/nvidia-graphics-drivers-390/+bug/1799679


add the following line to `/etc/environment`:
```
__GL_SYNC_TO_VBLANK=0
```

Note: you can check future driver issues on this tracker too!

## 7. Install and configure software packages

These are my frequently used packages and by no means exhaustive. You can use 
the new Ubuntu Software application or the web and your own discretion to explore the vast ecosystem of available packages.

### Install python dev libraries and pyenv

These are OS level libraries needed for pyenv, see https://github.com/pyenv/pyenv/wiki#suggested-build-environment for updates:

```
sudo apt update
sudo apt install build-essential libssl-dev zlib1g-dev \
libbz2-dev libreadline-dev libsqlite3-dev curl llvm \
libncursesw5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev libsasl2-dev python3-dev libldap2-dev
```

If you encounter issues see https://github.com/pyenv/pyenv/wiki/Common-build-problems.

From https://github.com/pyenv/pyenv-installer:
```
curl https://pyenv.run | bash
```

Follow `.bash_profile` instructions for pyenv.

### Install other essential libraries

```bash
sudo apt update
sudo apt install -y curl vim git vlc shutter gimp firefox tmux
```

### Setup Git
Setup instructions [here](https://help.github.com/articles/set-up-git/#setting-up-git).

### Install VS Code

See instructions at https://code.visualstudio.com/docs/setup/linux

### DotFiles

Clone [DotFiles repo](https://github.com/TStesco/DotFiles) and follow directions in README.md.

```bash
git clone https://github.com/TStesco/DotFiles.git
```

### Install Anaconda

Get the latest installer version for your computer and version of Python 
[here](https://www.continuum.io/downloads#_unix) and run it with bash.

### Install Docker
The community edition is freely available here for all major
OS: [https://www.docker.com/community-edition](https://www.docker.com/community-edition)

### Install nvm
Node volume manager for node.js and npm. Use install script in the master repo:
 [https://github.com/creationix/nvm](https://github.com/creationix/nvm)

