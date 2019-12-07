---
title: 'ACAD &#8211; Monitoring Tools'
author: Ninad
layout: post
permalink: /blog/2008/10/acad-monitoring-tools/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - apachetop
  - applet
  - bmon
  - kicker
  - monitor
  - ps
  - tools
  - top
  - webalizer
---
A lot of us computer fans are stat freaks. We take pains to cover the minutest of details and follow them with a zeal. We always use the statistics to keep a watch on the health of our computer. I'll discuss some of the tools I use, today.

**Applet Monitoring Tools**:  
This is the first thing I always do on any computer I get my hands on. I will add the **System Monitoring Applets** to the **GNOME/KDE panels**. They are available on both, and help you keep a watch over the *CPU, RAM and Swap memory usage*. Being applets, they do not put too much of a load on the system, but are always clearly visible, no matter what you are doing. The GNOME applet also allows you to *monitor network and disk usage* values. One more applet that I am very fond of is the ftp server **FTP Monitoring applet** on Kicker. It keeps a tab on the number of connections to your *ftp server*.

**System Monitors**:  
The logical continuation of the above applets are the **GNOME System Monitor** and the **KDE Process Guard**. Both can be launched by just clicking on the respective applets. They are what Windows calls '*Task Managers*', and hence, can be used to monitor and control almost every application that is running on the system, given the fact that you have the privileges to do that. The KDE Process Guard goes one step beyond the GNOME System Monitor, and can be used to read information from almost any file in the */proc* filesystem.

**Command Line Tools**:  
**Bmon, Top, Apachetop and ps** are my most commonly used command line tools. Bmon (command '*bmon*') is a small, light utility that keeps a track of the bandwidth usage, and can also show the usage for different interfaces on your system. Top ( command '*top*') is one very popular tool used by all Linux System Administrators. It is a command-line version of the System Monitors discussed above, and is quite powerful, when configured the right way. '*ps*' is a command that will list all the running programs on your linux box, and is very useful in conjunction with '*grep*', the search tool. *Apachetop*, on the other hand, is a nice little application for monitoring the logs of Apache, the web server. However, this is not a part of the Apache package, and has to be installed seperately through Synaptic or apt-get.

**Miscellaneous**:  
One more application I love is '*Webalizer*'. This an advanced Web server log analyzer. It generates reports on a daily basis about the usage of the webserver, and provides various interesting details on the hits that your server gets.

This list of applications is by no means exhaustive. This is just a list of programs that I am used to and am comfortable with. There are lots of applications available in the repositories, and each one has his choice.

*P.S.*: Google is celebrating it's 10th birthday, with [this][1]. The searches that Google gives for January 2001 are really interesting. Use keywords like 'gmail', 'wikipedia' or 'ubuntu' to get interesting results! :smile:

 [1]: http://www.google.com/search2001.html
