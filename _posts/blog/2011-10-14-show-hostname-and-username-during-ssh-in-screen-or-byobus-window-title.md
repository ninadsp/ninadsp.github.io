---
title: "Show hostname and username during ssh in screen or byobu's window title"
author: Ninad
layout: post
permalink: /blog/2011/10/show-hostname-and-username-during-ssh-in-screen-or-byobus-window-title/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - byobu
  - hostname
  - how-to
  - screen
  - Shell Script
  - ssh
  - username
---
At work, I have to access multiple test servers over ssh.  Most users of screen/byobu would follow the examples [here](http://aperiodic.net/screen/title_examples "Screen Wiki - Title Examples") to set the current screen window's title to show the username and hostname of the remote host.  However, all the steps involve either figuring out the slightly cryptic syntax for the *hardstatus* and *caption* commands of screen, or modifying the prompts on the shells at the remote host.  Most of the servers I connect to, being test machines, are regularly cleaned.  Hence, I cannot rely on safely keeping my configuration files on those machines.

So, I set out to search for a hack that would let me play around with configuration files on the local machine and not rely on the values reported by the remote shell.  After a little Googling, I came across [this](http://www.tenshu.net/p/screenssh.html "Screen SSH script") blog post.  The post links to a bash script which relies on the ssh client to execute it on a successful connection.  The ssh client passes along a few parameters to the script, which it processes, and then, echoes the proper escape character sequence along with the hostname.  Screen dutifully catches the command and sets the window title to the hostname.

I made a few changes to the script before using it at office.  The script uses the *%n* escape character substitution of the LocalCommand option of ssh.  *%n* is known to have bugs in some versions of the OpenSSH client, and hence, the author had included a work around for the affected versions.  I have instead, replaced *%n* with *%h*, which works reliably on all versions of  the client.  I also added the username to the screen title by adding the *%r* substitution.

My version of the script is:

{% gist 6098449 screen_ssh.sh %}

To use this script, add the following options to your *~/.ssh/config* file:

{% gist 6098449 ssh_config %}

**P.S.:** This script is still a work in progress.  The window's title does not update when you log out of a session.  It only updates when you start a new ssh connection.  If I find a trick to reset the window's title, I will add it here.

*Update on 22 October*: Instead of trying to find a hook that I could attach a script to at the log out, I have instead bound the *title* command to a key so that I can use a keyboard shortcut to reset the title to a fixed one.  I've added the following code to my *~/.screenrc*  

{% gist 6098449 screenrc %}

Thus, when I hit *Ctrl+A, T*, the title of the window is set to 'bash'.  Works for me, YMMV.
