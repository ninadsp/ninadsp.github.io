---
title: 'ACAD &#8211; How healthy is my computer?'
author: Ninad
layout: post
permalink: /blog/2008/08/acad-how-healthy-is-my-computer/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
---
Today, we'll have a look at some commands that will report your system's vital statistics. First and foremost, we'll see how long has your computer been on. Here's a sample from my system: {% gist 6098996 uptime.sh %}

Another tool to find out the time when the system was last booted is: {% gist 6098996 who_1.sh %}

The command **who** shows a list of people already logged in to your Linux/Unix system and what terminal are they logged in from. {% gist 6098996 who_2.sh %}

One very useful utility, which is infact a command line system monitor, is **top**. Use '*?*' to see the keyboard shortcuts, and '*q*' to quit. To know your RAM's usage, you can also use the following command, instead of opening *top* to search for that.  {% gist 6098996 free_1.sh %}


The *-m* switch shows all the usage values in Megabytes, instead of the default Kilobytes. To check your hard disk for free space:  {% gist 6098996 df_1.sh %}


I already have given you a shell script to check your computer's temperature, as reported by the mother board's sensor in this post. Hope I get answers from ACAD readers for the challenge of the previous post. Catch the answer in tomorrow's post of ACAD! :smile:
