---
title: How to install Amarok 1.4 on Jaunty
author: Ninad
layout: post
permalink: /blog/2009/07/how-to-install-amarok-1-4-on-jaunty/
categories:
  - Blog
  - Hobbies
  - Linux/Ubuntu
tags:
  - ACAD
  - Amarok
  - Linux/Ubuntu
---
This is for all those Amarok 1.4 fans out there, who miss it, and are stuck with Amarok 2.x in (K)Ubuntu Jaunty.  A few days ago, I was reading a <a href="http://www.reddit.com/r/linux/comments/84zux/who_else_feels_amarok2_is_a_huge_dissapointment/" target="_blank">discussion on Reddit</a>, about the general frustration of users with Amarok 2.x, and I came across this jewel.

<a href="https://launchpad.net/~bogdanb" target="_blank">A noble soul</a> has taken the efforts to package the Amarok 1.4 sources for Jaunty, and put them up at his Launchpad PPA Archives.   The instructions to add a PPA can be found very easily on Launchpad, but here they are, just for your reference:

  * Add the repository to your sources list.  You can do this by two methods:

  * Add the following line to your apt sources list from a text editor: {% gist 6098996 amarok_jaunty_ppa.txt %}
  * OR, Add each of the above lines individually to the '*Third Party Software*' in *System* > *Administration* > *Software Sources*, or *Settings* > *Repositories* in Synaptic

  * Add the GPG key used to sign the package to your apt. `sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys AE74AE63`
  * Update your package list, and install the **amarok14** package.  It'll automatically uninstall any amarok2.* packages installed on your system.
