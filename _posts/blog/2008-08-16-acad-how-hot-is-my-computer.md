---
title: 'ACAD &#8211;  How Hot is my Computer???'
author: Ninad
layout: post
permalink: /blog/2008/08/acad-how-hot-is-my-computer/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - Shell Script
---
Today, I'll give you a small script that will give the temperature of your CPU at a given time.  This is a very simple shell script, which contains a command to display the temperature of the CPU.  Here's what you have to do&#8230;

  * Open a file in your favourite text editor. I shall use vim and name the file as *.cpu_temp*. The command will therefore be `vim .cpu_temp`
  * Add the following lines to the file: {% gist 6098996 cpu_temp.sh %}
  * Save the file and make it executable. It can be done using the command `chmod ugo+x .cpu_temp`
  * Execute the shell script from the command prompt by entering `./.cpu_temp`. Remember **./a.out**???

That's It! You now have a small utility that will print the temperature of the CPU to the screen whenever you run it. Isn't shell scripting simple? :smile:

Now, let's have a look at what all went into the shell script:

  * The first line, **#!/bin/bash** is the most important part of a shell script. It identifies the file as a shell script and that the above file is to be run in the BASH shell. Other shells will have similar lines.
  * The next line is a simple **cat** command that reads the */proc* file system, which is a virtual file system, that stores all the statistics about the computer and running processes. All data collected by the various sensors on the mother board are stored here.
  * The last line is to tell the shell that the file executed successfully.
  * Every line is delimited by a '**;**', while single line comments are to be marked with a '**#**' at the beginning of the line.

Later on, we will look at more complex shell scripts, throughout the course of ACAD, where you will meet programming constructs that will remind you of C. Have fun with the /proc file system, there is a lot to learn in it. :smile:
