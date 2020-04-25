---
title: 'ACAD - locate files on your Linux system'
author: Ninad
layout: post
permalink: /blog/2008/08/acad-locate-files-on-your-linux-system/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - crontab
  - locate
---
Windows has the Search function to find files on your hard disk.  But we all know that it is quite a PITA, and really slow (especially on XP), to search for the file.  Linux too has a similar program to help you search for files stored on your system.  It's name is '*locate*' and it is a command line utility available on every Linux system.

The simplest use of locate is: {% gist 6099062 1.sh %}

You will get a list of all the locations where a filename has the expression we entered. Some of the options that you can use with locate are as follows:

  * -b . Tells locate to search for basenames only. For e.g., the basename of */home/user/dir/test.txt* is *test.txt*. This is useful when you do not want entire directories to be listed when the *expression* is a part of the directory name.
  * -c . Print the count instead of names of files found.
  * -i . Makes locate case-insensitive.
  * -l *LIMIT* . Limits the number of results to *LIMIT*.
  * -r . Tells locate that the *expression* supplied is a Regular Expression.
  * -w . Tells locate to search for the whole name of a file, as opposed to the basename.

The above use is a very basic example. Most of the times, we need to also include the file types, which can also be included in the expression. But, I prefer using grep at such times. Here's how: {% gist 6099062 2.sh %}

You can further pipe the output to filter it to your liking. Locate uses a database to index files, and scans it to search for the files. To update the database, in case you have recently added a large folder and you want to search for a file in it, run the following command: {% gist 6099062 3.sh %}

Advanced users can edit their crontab to automatically update their mlocate database by following these steps (The first command is optional. Ubuntu sets the default editor to nano, while I prefer vim): {% gist 6099062 4.sh %}

Append the following lines to the crontab: {% gist 6099062 5.sh %}

That's it for today! Hope it becomes easier to search for things on your disk&#8230; :smile:

**EDIT**: The crontab addition is not necessary&#8230; There is an entry for updatedb in the system crontab by default, and it updates the database once in 24 hours.
