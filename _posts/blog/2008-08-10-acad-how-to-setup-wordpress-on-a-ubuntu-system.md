---
title: 'ACAD - How to setup WordPress on a Ubuntu system'
author: Ninad
layout: post
permalink: /blog/2008/08/acad-how-to-setup-wordpress-on-a-ubuntu-system/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - Wordpress
---
Today, we'll have a look at how to install a **WordPress blog** on a freshly installed Ubuntu system. The procedure will be similar for most of the other Linux Operating Systems, with only the references to the package manager and a few other basic directories differing. In Windows too, it can be done very easily, if you know the right softwares. I'll mention the ones that I know. Installing WordPress occurs in two steps, Setting up a LAMP/WAMP server, and installing WordPress.

**Step 1 : Setting up a LAMP/WAMP Server:**

  * Open Synaptic Package Manager from *System > Administration*. Click on *Edit* and select *Mark Packages by Task*. From the box that appears, select *LAMP Server* and click 'OK'. Complete the installation by clicking 'Apply', accepting the changes, and let Synaptic download and install the required packages.
  * On a Windows System, get hold of the latest stable version of the *XAMPP* server or any other software that will install WAMP for you. Run the Setup. You might have to restart the Computer. I have never seen a WAMP system being setup, so I have no idea about the details. Please refer to forums and how-to's on the net for further help.

**Step 2 : Install WordPress:**

  * Go to the [WordPress][1] site, and get the latest stable version of WP. As of writing, the latest stable release is WP 2.6. Windows users, download the .zip (1.2 MB), Linux users download the tarball (1MB).
  * After downloading the tarball/.zip, untar/unzip it to a location on your system where you want to store all your websites. The default location for Linux is the Apache root, */var/www/*. However, you can setup the WP directory anywhere and post a link to it from the Apache directory. Windows users, please do the same thing in your Apache root.
  * The link to the blog location can be done in two ways: making a symbolic link to the location of the WP folder from the Apache root, or the second, more elegant way is to use Aliases in the Apache configuration.
    * Here's how you make the sym-link: {% gist 6099125 1.sh %}
    * To add the Alias to the Apache, open `/etc/apache2/apache.conf` (or the equivalent in other OS's) in your favourite editor. Ubuntu users, if you are not working in root, follow these steps: {% gist 6099125 2.sh %}
    * Enter the password as asked. Scroll to the bottom of the file, where you will see space for entering Aliases. Insert the following line: {% gist 6099125 apache.conf %} Note the trailing '/' at the end of the Alias path.
  * Next step is setting up the database for the blog. We are using a MySQL database here, for which WP is optimised.
    * Open command prompt and enter: `$ mysql -p`. You will be asked the password if you set up a password for the MySQL login.
    * Next, {% gist 6099125 3.sql %}. The `wordpress@localhost` refers to the username for the database, and the next one refers to the password for the database. Replace them with words of your choice.
  * Open *wordpress/wp-config-sample.php* in a text editor of your choice. Replace the strings as instructed. Put the dbname as *wordpress* and the username and password that you used in the earlier step. Leave the host and rest of the strings alone. Save the file as *wp-config.php*.
  * Now, open *http://your.ip.address/blog/wp-admin/install.php* in a web browser. WordPress will automatically install itself and give you a login account. Note down the password and login with the information. Change the password to a convenient one and fill up the rest of the information.
  * That's It! You are done! :smile: If you have doubts about the installation, you can visit this for more information.

Happy Blogging!

 [1]: http://wordpress.org/download/ "WP download page"
