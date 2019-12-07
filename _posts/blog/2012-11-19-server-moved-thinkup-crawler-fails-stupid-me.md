---
title: Server moved, ThinkUp crawler fails. Stupid me
author: Ninad
excerpt: php5-curl must be installed for the ThinkUp Crawler to run
layout: post
permalink: /blog/2012/11/server-moved-thinkup-crawler-fails-stupid-me/
categories:
  - Blog
  - Linux/Ubuntu
  - PHP/jQuery
tags:
  - crawler
  - curl
  - PHP
  - thinkup
---
I had to move the server over the weekend. As my requirement is a basic LAMP server, I've never bothered to figure out how to create an AMI. Also, I don't have to change things around too often, so I don't really need it.

So, I've moved the server, my MySQL and Apache are all running fine, the blog is up and running, and ThinkUp does not complain about incorrect permissions for the data folder. To check up on things, I run the crawl.php script. It executes, shows an output for the first two lines, and then dies:

```
  2012-11-17 18:15:03 | 4.1MB | SUCCESS| ni_nad | TwitterPlugin::crawl,106 | Starting to collect data for ni_nad on Twitter.
  2012-11-17 18:15:03 | 4.5MB | INFO   | ni_nad | TwitterAPIAccessorOAuth::__construct,111 | Errors to tolerate: 100
```

There is absolutely no error in the Apache logs, nor does switching the Developer log setting in ThinkUp on help. I'm struggling with the problem for nearly half an hour, and it strikes me. I had not installed the *php5-curl* extension. One *apt-get install*command later, the crawler runs perfectly fine.

Lesson learnt - Boot the old laptop and check the list of packages installed on a fresh Ubuntu EC2 image that you'd created long ago. Or, move it to the cloud where you can check it easily.
