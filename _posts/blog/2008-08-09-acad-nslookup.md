---
title: 'ACAD - nslookup'
author: Ninad
layout: post
permalink: /blog/2008/08/acad-nslookup/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - nslookup
---
As I promised yesterday, here's a neat little tool to query the DNS servers, `nslookup`. This is primarily used to check the DNS for the IP address of a particular domain name. However, a simpler use is to check if the DNS server at IPC is working or not. The command is run in its simplest form on the command prompt of both Windows and Linux as

`$ nslookup www.example.com`

The output is the IP address of the site given. Here is an example for the query `$ nslookup www.google.com`

{% gist 6098996 nslookup_1.sh %}

As you can see from this example, Google maintains four IP addresses for the international site, and these could quite well be just masks that we are looking at. Behind these IP addresses, there could well be server farms of hundreds of servers, working 24 hours a day to give us the brilliant performance that we have come to expect of Google. One more thing that we can notice here is that the DNS service runs on the port 53. This is the standard port for this service

One can also do a reverse query on the DNS by supplying the IP address of a site to know the name of the website. For example, `$ nslookup 172.24.2.82` to get the result that this is the IP address at which the bitsmail01 server is located.

The examples you have seen above are of the non-interactive mode of nslookup. The interactive mode can be evoked in the Linux command prompt by `$ nslookup` or `$ nslookup - [IP address of the DNS to be queried]`, the '-'; indicating that further input is to be taken from stdin.

The man page of nslookup lists a few options that can be used along with the command, and are not mostly needed. The default values are sufficient. However for people really interested in extracting information from the DNS for a particular task should have a look at `dig` as it is a more flexible and powerful tool to query DNS. A batch processing mode, missing in nslookup, is also available in dig. I will try to write about dig once i get the hang of it and have experimented with it. For now, nslookup is sufficient and it has served me faithfully, in my experiments on our LAN.

Till tomorrow, then, Safe Computing! :smile:

P.S. : For those who are new to blog and forum articles, the '$' or '#' used by post writers in the commands refers to the command prompt and is not to be typed as a part of the command.
