---
title: 'MySQL &#8211; Moving datadir'
author: Ninad
layout: post
permalink: /blog/2011/11/mysql-moving-datadir/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - apparmor
  - aws
  - ebs
  - ec2
  - how-to
  - mysql
  - note to self
  - tips
---
For the last few hours, I had been piddling around with the folder hierarchy on the host that runs this blog. I use an Amazon EBS backed instance for this job. I started off with a simple setup, where I had all the data on one single EBS volume, which included all the MySQL databases along with the webroot. If I borked this setup, there was no way I could painlessly restart a new instance and have the website up and running within half an hour. Switching the web root directories for Apache is pretty easy, and I had already done that a few times. However, I had never tried switching the data directory for MySQL before. I always used the default location in Ubuntu, */var/lib/mysql*. I also had to consider the space issue. ThinkUp's database turns into a beast if you've been running it for a few months. With my paranoid backup policy, there was a high chance I would run out of space on the root EBS volume pretty soon.

I decided to move the data directory to a dedicated EBS volume. I Googled for the procedure to do that, and came across multiple blog posts, which explained the same thing ( [1](http://kaliphonia.com/content/linux/how-to-move-mysql-datadir-to-another-drive) and [2](http://rajshekhar.net/blog/archives/90-Moving-the-MySQLs-datadir-directory..html) ). The steps are roughly the same, but they missed one important step. InnoDB database files need special attention. Here are the steps that worked for me:

  * Stop the MySQL server: {% gist 6098434 step-1.sh %}
    
  * Prepare the new location for the data directory. In my case, it meant creating a new EBS volume, attaching it to an instance, formatting it to ext3 and then mounting it to */mnt/data*.
  * Replicate the entire MySQL data directory to the new location. This includes the folders for each of your databases as well as the ibdata\* and ib_logfile\* files. Being a Ubuntu instance, I also had a Debian specific file in the folder. Choose a tool of your choice. I rsync'd the two locations with {% gist 6098434 step-3.sh %}
  * Ensure that the */mnt/data/mysql* folder is owned by the *mysql* user and group and has the correct permissions. Rsync normally takes care of this.
  * Open */etc/mysql/my.cnf* and update the datadir variable to point to the new location: {% gist 6098434 step-5.sh %}
  * Update the AppArmor profile for MySQL. Edit */etc/apparmor.d/usr.sbin.mysqld* and modify every line beginning with */var/lib/mysql* to */mnt/data/mysql* .
  * Reload AppArmod profiles with {% gist 6098434 step-7.sh %}
  * Start the MySQL server: {% gist 6098434 step-8.sh %}
    
This set of steps worked for me. YMMV, check the log files in */var/log/mysql/* if it refuses to start at the last step.
