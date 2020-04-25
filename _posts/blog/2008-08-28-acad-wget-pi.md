---
title: 'ACAD - wget PI'
author: Ninad
layout: post
permalink: /blog/2008/08/acad-wget-pi/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - wget
---
Today, we'll have a look at one of my favourite download managers. Every Linux system includes this tool, *wget*. It's manpage describes it as the perfect tool to download on slow, unstable network connections. I second that, having used it on our LAN, which is notorious enough to not work when we need it the most, especially for our academic work. It works best as a background process, which means that you can start wget, send it to the background, and forget about it (for some time :smile: ). It will run in the background, periodically updating the log file, and complete your download(s) without interfering with your work. However, *do not expect lightning fast speeds from wget* as it cannot thread files into chunks and download parts simultaneously. Let's have a look at the basic usages of wget today. The rest will be covered in the next ACAD post.

The simplest invocation of wget is: {% gist 6098983 1.sh %}

With this command, wget will start downloading the file specified in the *url*, in the **foreground**, and notify you with a very verbose output of the download. The downloaded file will be saved in the **current working directory**. Now, let's try something more advanced: {% gist 6098983 2.sh %}

Here's what all the options mean:

  * **-t** . Wget will try at the most 15 times in case of failures. The default setting is 20 and can be set to infinity by using **0 or inf**. However, fatal errors like 404 and 503 will cause wget to die.
  * **-c** . It tells wget to continue a previous download if there is a partially downloaded copy of the same file in the working directory. This should be used whenever using more than 1 tries, as my experience shows that wget, for each new attempt, creates a new copy of the file to be downloaded.
  * **-o** . The file specified after this is used to store the log of the download in. If no file is specified here, wget defaults to the log file *wget-log*.
  * **-b** . This tells wget to work in the background, and you will return to the terminal, while wget happily continues it's work

Before using wget to download, don't forget to set the proxy servers either in your environment or in the */etc/wgetrc* file. This is the most basic use of wget to download a file from the internet. Tomorrow, we'll have a look at the real power of wget, it's ability to batch process downloads, and recursively download things from a server. Till then, happy downloading! :smile:
