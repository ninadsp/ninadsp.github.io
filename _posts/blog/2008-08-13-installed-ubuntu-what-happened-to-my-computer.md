---
title: 'Installed Ubuntu&#8230; What happened to my computer???'
author: Ninad
layout: post
permalink: /blog/2008/08/installed-ubuntu-what-happened-to-my-computer/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - Ubuntu
---
Ever since Ubuntu started shipping free CD's of it's Operating System, and Fedora in magazines like Digit, a lot of people on campus have installed Linux on their systems, in an attempt to use it. Now, that is great news for the Open Source and Linux community. This should lead to the development of a large number of applets and applications from our campus, as we have some of the best brains, right? However, this has not happened. When people install Ubuntu and do not find the 'Start' button that they are so used to, or many other common applications like the Internet Explorer (an application that I try to avoid as far as I can), IPMsg and DC++, they get frustrated and format the Ubuntu partition, just to find out that the GRUB loader is now clueless and the system doesn't boot!

Many a times, people can avoid this scary experience, by first trying out Linux through a Live CD, and if they find themselves comfortable, install it. They should remember that **Linux is not Windows**. Everyday tasks are done more differently, many a times more efficiently. Also, people should not keep unreal expectations from any Linux operating system, as first of all, it is an Operating System, and second, they don't have corporate biggies like Microsoft backing them. It is a bunch of programmers who are out there, enjoying coding and making applications. If you do get to the point of actually installing a Linux OS, here are a few tips that could help you and keep you from getting lost in the plethora of choices. I shall speak about Ubuntu, the Linux OS that I am most familiar with. However, the inherent nature of Linux makes these instructions generic. This is not an exhaustive list, and everyone is expected to help me improve this list of to-do's:

Before starting of with anything, set the Proxy for your system by going to *System > Preferences > Network Proxy*. Also, set Synaptic's proxy by going to *System > Administration > Synaptic Package Manager*. Then, go to *Settings > Preferences* and enter the correct value in the *Network* tab.

  * First thing that you need to do after setting up Linux is to get the latest package list, which should be done by going to *Applications > Add/Remove Programs* and clicking on *Reload*. This updates the information about the latest versions of various packages on your system.
  * Next up, comes the installation of a few basic packages that everyone requires. Ubuntu 8.04 includes '**ntfs-3g**' by default, hence there is no need to install separate drivers for NTFS partitions. **Ubuntu Restricted Extras** is a very useful meta-package that will include the proprietary MP3 and avi codecs, some MS fonts, Java environment and Flash plugin for Firefox.
  * The above will take care of most of the basic codecs for ensuring your entertainment. However, the audio and video players that come pre-installed with Ubuntu can only satisfy you so much. I recommend installing **Amarok** for those used to the iTunes interface, and **XMMS Music Player** for those happy with the Winamp interface. Amarok has better collection and playlist handling capabilities.
  * The recommended video player is **Kaffeine**, which runs on the same xine backend as Amarok. However, for those who wish, **VLC** is also available.
  * Now, go forward and install **linuxdcpp**, the port of the well known DC++ on Windows. Other DC clients are available, however, this is the most user friendly. Don't forget to install **Wine** to enable you to run Windows programs (including CS!) on Linux. Use the Windows IPMsg through Wine. A debian setup for IPMsg is being worked on by me, which may take time.
  * Optional applications are Opera (web browser) and Psi (Jabber client) as well as Akregator (RSS Feed Reader).

The above steps will give you a Ubuntu setup that will be able to help you do most of the routine tasks that BITSians expect from a computer, i.e., listen to music, watch movies/serials, connect to the net and LAN, and partly gaming too. Any suggestions regarding this post are welcome.

Edit: This post is meant to be a listing of the major applications that we need. The installation process is different, and everyone should learn for themselves, for in it is the opportunity to learn Linux and that is where the joy of using Linux is&#8230; Kindly make a few attempts to install yourself, Google for errors, and then ask others for help. If you plan to ask me for help, install sshd with '`sudo apt-get install openssh-server`' and then buzz me. I am too lazy to come to your hostel room.
