---
title: 'ACAD - wget PII'
author: Ninad
layout: post
permalink: /blog/2008/08/acad-wget-pii/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - linux
  - wget
---
Continuing from the last episode of ACAD, we'll try to understand the very powerful and versatile downloading tool, wget. As you might have seen from the examples we looked at yesterday, it is not possible to download more the one link at a time in wget. This can be taken care of by specifiying a list of all the links in a simple *.txt* file, as follows: {% gist 6098983 Sample.txt %}

{% gist 6098983 3.sh %}

In most cases, the list of links has a common 'base url' i.e., you will be downloading all files from *www.site1.com/downloads/public/*. You can simplify your work by using the **-B [url]** switch.

If you wish to download an entire section of a website, say for mirroring, use the **-r** switch to recursively download files. Here's an example that I use once every month to mirror the NASA Astronomy Picture of the Day Archive: {% gist 6098983 4.sh %}

This is what the rest of the options do:

  * **-r** . This is the recursive option.
  * **-l 3** . This sets the recursive levels to 3. It can also be set to *inf* to make a perfect mirror.
  * **-k** . This option will tell wget to scan through every html file that it downloads and change the HTML references to point to the files stored on the hard disk. This is a must if you wish to browse the site in Offline Mode, by just clicking on the links.
  * **-p** . Downloads all the page requisites like css, images, flash, etc.

If you wish mirroring to happen automatically, you can include the above command in your *crontab*. One more very useful option, that I used to the fullest last semester was the '**--retry-connrefused**'. When the IPC was trying to cut short the large number of downloads by automatically breaking connections every few seconds, I was happily downloading things at atleast 50 kbps, thanks to this option! :smile: :smile: Play along with the command, read it's man pages. There's a lot more to learn about this simple but very powerful tool! :smile:
