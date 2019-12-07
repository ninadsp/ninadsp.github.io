---
title: 'ACAD &#8211; OpenDNS.com'
author: Ninad
layout: post
permalink: /blog/2008/08/acad-opendnscom/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - Linux/Ubuntu
---
All of you who think that ACAD is about academics, please stop reading here&#8230; ACAD is A Command A Day, where I will post tips and tricks on using Linux, and Ubuntu in particular. Some of the information that you will see here can be found on the man pages of the commands, however, I will attempt to simplify it and not do a straight copy-paste.

Today, we will have a look at a service offered on the internet, [Open DNS][1]. It is a free Domain Name Server service, that provides DNS resolution services. DNS, as it's name suggests, relates the domain names (names of web-sites) to the actual IP addresses of the server on which the site is hosted. The IP addresses are computer readable and the computer then connects to the site to download the pages of the site. You might have noticed that if the DNS at our IPC (172.24.2.71) is not working, we are unable to access new sites while we can continue to browse sites that we have already visited and the pages are open in the browser. The DNS server is known to have a spotty performance and does go down a lot of times, especially at the beginning of the semester, just like it happened sometime ago, today.

Here's where the utility of OpenDNS comes in. It can be used as an alternate DNS and it will act as the backup for our IPC DNS. To use it as a secondary DNS is very simple. Just follow the steps given here:

**For Windows Users:**

  * Open Control Panel and go to Network Connections.
  * Right click on the LAN connection that you are using, and Select properties
  * A window will open up and you will see a list of protocols supported. Click on the TCP/IP protocol and click the 'Configure' Button.
  * On the bottom half of the second window that opens up, you should see the option 'Automatically Set DNS Server' option selected. Select the '*Manual*' option and enter **172.24.2.71** as the Primary DNS.
  * In the Secondary DNS field, enter the IP address of the OpenDNS server, either **208.67.222.222** or **208.67.220.220**. If you want to add both, you can click on the 'Advanced' button and add the three of them, and set priorities.
  * Please do not set the OpenDNS server as your Primary DNS&#8230; It will cause unnecessary traffic between your computer and the server, and the IPC server is on LAN, so it will be comparatively faster.

**For Linux Users:**

  * Open vim or your favourite text editor with Super User/Root permissions. Open the file ~~/etc/resolv.conf~~. *Please read the P.S. to follow the correct procedure.*
  * Append the line `nameserver [ip address of the DNS]`. The IP addresses are **208.67.222.222** and **208.67.220.220**.
  * The order in which you add the servers to the file is the order in which the servers are queried. The point made for Windows users about responsibly setting the order is also valid over here.

Tomorrow, I'll continue this topic and take up a basic DNS querying tool, `nslookup`, available on both the Windows and Linux command line.

**P.S.**: The method given above to add the DNS servers to the Linux configuration is not the correct one. It does not work as every time Network Manager connects to a network, like on a reboot, it will overwrite the `resolv.conf` file. The correct file to edit is `/etc/dhcp3/dhclient.conf`. This file is read by Network Manager while creating the resolv.conf. Add the following line as it is, after the `#prepend domain-name-servers 127.0.0.1;` line. `append domain-name-servers 208.67.222.222;`

The **append** directive will ensure that OpenDNS becomes your secondary DNS. If you wish to make it primary, use the **prepend** directive instead. While using this, make sure that the `prepend domain-name-servers 127.0.0.1;` is commented. Or you will have conflicts.

 [1]: http://www.opendns.com "OpenDNS"
