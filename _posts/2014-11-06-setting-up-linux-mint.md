---
layout: post
title: "Setting up Linux Mint"
categories:
tags: "Linux"
---


### Essential Packages
 
* launchy
* dropbox
* google-chrome-stable
* terminator
* keepass2
* truecrypt
* xclip
* qterm
* sublime-text

#### Configure the Tex Environment

```bash
sudo apt-get install texlive texlive-generic-extra texlive-fonts-extra texmaker
```

##### To use the normal tlmgr package manager:
    
```bash
# To install a pckage
tlmgr install <package name>

# To update a package use:
tlmgr update <package name>

# To update all packages (and tlmgr itself):
tlmgr update --self --all
```

#### setup chinese

``bash 
sudo apt-get install language-pack-zh-hans language-pack-gnome-zh-hans ibus-table-wubi ibus-pinin
```

#### Install Oracle Java
    
```bash
# Download from oracle and extract
sudo mkdir -p /usr/lib/jvm/
sudo mv jdk1.7.0_xx /usr/lib/jvm/ 
sudo ln -s jdk1.7.0_xx jdk1.7.0
# Register the jdk
sudo update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/jdk1.7.0/bin/javac 1 
sudo update-alternatives --install /usr/bin/java java /usr/lib/jvm/jdk1.7.0/bin/java 1 
sudo update-alternatives --install /usr/bin/javaws javaws /usr/lib/jvm/jdk1.7.0/bin/javaws 1 
# Set the default javas
sudo update-alternatives --config javac
sudo update-alternatives --config java
sudo update-alternatives --config javaws
```

#### Config Sublime text

Useful packages

  * Package Control
  * Terminal
  * Trimmer
  * Alignment
  * ConvertToUTF8
  * Pretty JSON
  * AngularJS

#### Install latest git

```bash
sudo add-apt-repository ppa:git-core/ppa
```

#### Custom Fonts

* [Edlo](http://erichamiter.com/Edlo/)
* Inconsolata: fonts-inconsolata

#### Copy to clipboard

```bash
pwd | xclip -sel clip
# Setup the alias
alias clip="xclip -sel clip"
# After that, copy can be:
pwd | clip

```

#### Setup Jekyll

``` bash
sudo apt-get install ruby ruby-dev make nodejs
sudo gem install rdiscount --no-rdoc --no-ri
sudo gem install redcarpet --no-rdoc --no-ri
```

#### Mount samba

1. Install the package

		sudo apt-get install cifs-utils

2. Setup the credential vi ~/.smbcredentials Enter your Windows username and password in the file:

		username=msusername
		password=mspassword

3. Update the permissions

		chmod 600 ~/.smbcredentials

4. Setup the fstab

		//servername/sharename /media/windowsshare cifs credentials=/home/ubuntuusername/.smbcredentials,uid=user,iocharset=utf8,sec=ntlm 0 0

#### Mount samba share manually

``` bash
mount.cifs //servername/sharename mountlocation/ -o credentials=/home/user/.smbcredentials,uid=userid,iocharset=utf8,sec=ntlm
mount.cifs //servername/sharename mountlocation/ -o user=username,password=passwd,uid=userid,iocharset=utf8,sec=ntlm
```


#### Setup the video card
Check the video card driver setting

```bash
inxi -Gx
```

Install the newest nvideo driver

```bash
sudo add-apt-repository ppa:xorg-edgers/ppa
sudo apt-get update
sudo apt-get install nvidia-423

sudo nvidia-xconfig
```

To make ThinkPad W520 work with Nvidia Descrete Graphic

```bash
# Edit /etc/default/grub to add nox2apic
GRUB_CMDLINE_LINUX_DEFAULT="nox2apic quiet splash"
# Update grupb
sudo update-grub2
```
