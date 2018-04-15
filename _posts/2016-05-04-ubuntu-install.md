---
layout: post
title: Fresh System Install Guide
date: 2016-03-04 00:00:00 -0000
image: Ubuntu_logo.png
tags: [software]
---

I use Ubuntu 16.04 LTS on my laptop, it's the base for what I use in production 
and I think its a fantastic OS generally. Like any good engineer I appreciate 
(semi)frequent maintence, so I do a fresh reinstall of my OS and system software 
every few months. Partly to get rid of packages installed to test things I no 
longer use and have forgotten about (sorry emscripten), and partly because it 
makes me feel zen. I decided to make my own guide with the bash scripts and host 
it here so I can access it from my freshly installed OS.

<h2 class="section-heading">Steps</h2>
<ol>
	<li>Back up files</li>
	<li>Make sure back ups work</li>
	<li>Make boot disk with correct OS image</li>
	<li>Boot from disk</li>
	<li>Install OS</li>
	<li>Configure OS</li>
	<li>Install software</li>
</ol>
<h2 class="section-heading">1. Back up files</h2>
<p>
	My important files are stored on remote servers and backed up on local external drives to avoid lossing anything. I use Ubuntu's deja-dup automatic backup service in between external drive back ups as well.
</p>
<h2 class="section-heading">2. Make sure back ups work</h2>
<p>
	It may seem obvious but its worthwhile to actually test that your most important files actually are backed up and didn't get corrupted or become otherwise inaccessible. I tend to just make important directories are the same size and try openning a few random files, or a few particular very important ones.
</p>
<h2 class="section-heading">3. Make boot disk with correct OS image</h2>
<p>
	Choosing the correct OS image comes down to if you have a PC or a server and what processor you have. I need the AMD64 Ubuntu 16.04 disk image (.iso file). You can get the <a href="http://releases.ubuntu.com/16.04/">official releases from Ubuntu here.</a>
</p>
<p>
	Once you have the OS disk image downloaded get a blank or RW CD/DVD and burn the image onto it. You can use a standard Ubuntu disk burning program like <a href="https://en.wikipedia.org/wiki/Brasero_(software)">Brasero</a>. If you don't have Brasero you can always install it using Bash with the command:
</p>

```bash
sudo apt install brasero
```
<p>
	A noteable problem I had with Brasero was that it halted while creating the disk checksum at the end of writing. This is a somewhat common issue and can be solved by going into the Brasero preferences and turning the disk checksum plug-ins off. Having a checksum is for validating that the OS image is from a trust worthy source. If you are downloading it directly from the distributor and installing it immediately then you can likely get by without the checksum.
</p>
<h2 class="section-heading">4. Boot from disk</h2>
<p>
	Reboot the computer and enter the system BIOS. This is something that the manufacturer of the computer sets so you need to look up how to do that with your computer. Usually its by tapping or holding the function keys at boot. Find the boot order and put CD disk first (before booting from the hard drive). Once CD has priority in the boot order just let your computer boot up normally.
</p>
<h2 class="section-heading">5. Install OS</h2>
<p>
	The CD may take a while to be read but will prompt you to choose either a live demo of the OS or fully install the OS on the computer. Choosing to fully install it then prompts you to allow the install to wipe your hard drive and current OS. I chose to wipe everything because it's easier though if you have a partition on your hard drive ready for it you could install it there for testing.
</p>
<p>
	You can also choose to encrypt your hard drive with a password. You do have to enter this password each time you boot up your computer however so think carefully about using it. Follow the installation guide to configure users, passwords, and whatnot and you should have your new OS up and running soon.
</p>
<h2 class="section-heading">6. Configure OS</h2>
<p>
    Connect to your network now if you can because now is a good time to update your system:</p>
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt autoremove
```
<p>
	I really like having the window options always visible and in the window, not the menu bar so go to <strong>Settings -> Appearance -> Behavior</strong>.
</p>
<div style="text-align: center;">
{% include captioned-image.html url="Appearance_001.png" description="" %}
</div>
<p>
	Next install the Canonical, community, and restricted software for Ubuntu. Go to <strong>Settings -> Software & Updates -> Ubuntu Software</strong>
</p>
<div style="text-align: center;">
{% include captioned-image.html url="Software_Updates_1.png" description="" style="" %}
</div>
<div style="text-align: center;">
{% include captioned-image.html url="Software_Updates_2.png" description="" style="" %}
</div>
<p>
	Now intall the Ubuntu Restricted Extras:
</p>

```bash
sudo apt install ubuntu-restricted-extras
```
<p>
	Configure the settings how you see fit. Also, you can now however move the taskbar from the side of the screen to the bottom using the Unity Tweak Tool or if you don't want to download the tweak tool, with this code:
</p>
```bash
gsettings set com.canonical.Unity.Launcher launcher-position Bottom
```
<p>
	Another nice customization is one-click minimize/maximize from your launcher.
</p>
```bash
gsettings set org.compiz.unityshell:/org/compiz/profiles/unity/plugins/unityshell/ launcher-minimize-window true
```
<p>
	I added a command to turn of my touchpad because I never use it to /etc/rc.local
</p>
```
synclient TouchpadOff=1
```

<p>
	Now to fix the login screen background. No need to install anything, open dconf-editor, deal with the LightDM user or anything terribly complicated. This is done from the file /usr/share/glib-2.0/schemas/com.canonical.unity-greeter.gschema.xml.
</p>
```
sudo vim /usr/share/glib-2.0/schemas/com.canonical.unity-greeter.gschema.xml
```
<p>
	add xml lines:<br><br>
<textarea rows="20" cols="80" style="border:none;">
<key name="background" type="s">
  <default>'/usr/share/backgrounds/milky_way.png'</default>
  <summary>Background file to use</summary>
</key>
<key name="background-color" type="s">
  <default>'#000000'</default>
  <summary>Background color, set before wallpaper is seen</summary>
</key>
<key name="draw-user-backgrounds" type="b">
  <default>false</default>
  <summary>Whether to draw user backgrounds</summary>
</key>
<key name="draw-grid" type="b">
  <default>true</default>
  <summary>Whether to draw an overlay grid</summary>
</key>
<key name="show-hostname" type="b">
  <default>true</default>
  <summary>Whether to show the hostname in the menubar</summary>
</key>
<key name="logo" type="s">
  <default>'false'</default>
  <summary>Logo file to use</summary>
</key>
<key name="background-logo" type="s">
  <default>'false'</default>
  <summary>Background logo file to use</summary>
</key>
</textarea><br>
and recompile schemas:
</p>
```bash
sudo glib-compile-schemas /usr/share/glib-2.0/schemas/
```
# 7. Install and configure software packages

These are my frequently used packages and by no means exhaustive. You can use 
the new Ubuntu Software application or the interwebs to explore the vast ecosystem 
of available packages.

## Install build-tools and essential libraries

```bash
sudo apt-get install -y build-essential libssl-dev default-jdk curl vim git vlc 
shutter gimp chromium-browser
```

## Setup Git
Setup instructions [here](https://help.github.com/articles/set-up-git/#setting-up-git).

## Install i3wm

Instructions [here](https://i3wm.org/docs/repositories.html). Configuration from
 ~/.i3 (see DotFiles). To solve issues with nautilus desktop window (if present):
```
gsettings set org.gnome.desktop.background show-desktop-icons false
```

## Install vifm

vifm is a vim-like file manager, lightweight and has great key bindings for navigating,
 launching .pdf etc., and moving files around. Configuration from ~/.vifm (see DotFiles). 

```bash
sudo apt-get install vifm
```

## DotFiles

Clone DotFiles repo and move .config files to user directory: 

```bash
git clone https://github.com/TStesco/DotFiles.git
mv DotFiles/* ~/
```

## Install Sublime Text 3

Follow package manager instructions [here](https://www.sublimetext.com/3). Add 
the package installer. 

## Install Anaconda

Get the latest installer version for your computer and version of Python 
[here](https://www.continuum.io/downloads#_unix)
```bash
bash "nameOfFile".sh
```

## Install Docker
The community edition is freely available here for all major
OS: [https://www.docker.com/community-edition](https://www.docker.com/community-edition)

## Install nvm
Node volume manager for node.js and npm. Use install script in the master repo:
 [https://github.com/creationix/nvm](https://github.com/creationix/nvm)

## Install Wine

```bash
sudo add-apt-repository ppa:ubuntu-wine/ppa
sudo apt-get update
sudo apt-get install -y wine1.7
```

Additional software packages seldom used: wireshark, nginx, arduino IDE 
