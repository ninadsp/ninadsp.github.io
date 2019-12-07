---
title: LG LXU800 Dialer on Ubuntu Jaunty
author: Ninad
layout: post
permalink: /blog/2009/05/lg-lxu800-dialer-on-ubuntu-jaunty/
categories:
  - Blog
  - Hobbies
  - Linux/Ubuntu
tags:
  - ACAD
  - bmon
  - dialer
  - jaunty
  - lg
  - Linux/Ubuntu
  - lxu800
  - poff
  - pon
  - pppconfig
  - ps
  - reliance
  - usbserial
  - wvdial
---
It' s been a few days since I've reached home.  One of the first things I did after getting back home, was to setup up a net connection with my laptop.  Recently, the folks at home had to replace the Huawei Data Card (a PCMCIA slot based dialer) that Reliance offers, with the LG LXU 800 USB dialer.

With full confidence, I plugged in the dialer, and ran **'sudo wvdialconf'**, expecting Ubuntu to give me the  excellent hardware support that it has always given.  However, to my surprise, let alone wvdialconf detecting the USB dialer, even **lsusb** was stumped by this new dialer from Reliance.  The only output that lsusb gave for the device was it's Vendor ID and Product ID, without any of the usual details like the name of the product and all.  Initial results with Google were very disappointing, and it was only after trying  out various combinations, Google pointed me to [this Ubuntu Wiki][1] page.   As the instructions on that page show, the default drivers loaded in the Ubuntu Jaunty kernel cannot recognize the dialer correctly, and hence are unable to create the necessary device nodes for it.  Run the following command, to load the proper driver with the correct parameters :  

` $ sudo modprobe usbserial vendor='0xeab' product='0x9357'`

  
The above command will insert the '**usbserial**' driver, and ask it to claim the dialer, which has a Vendor ID **0xeab** and Product ID **0x9357**.  The instructions on that page say that the dialer can then be configured with wvdialconf.  I was able to successfully generate the configuration file for wvdial, but it seems that the *Init* strings that it set for the dialer, don't work.  I also tried the settings given at the Ubuntu Wiki page,  but they did not work for me. Note: This command will have to be run every time the system reboots.  Or, you can add the above options to the */etc/modprobe.conf* or the */etc/modprobe.d/* directory, to load the module at boot time.

After trying a few random guesses on the Init strings, I gave up on wvdial, and tried using pppd, the Point to Point Protocol  daemon directly.  The following commands were run as root, by using '**sudo -i**' to access the root shell.  

`$ pppconfig`

  * The command gives an ncurses based interface.  On the first page, select '**Create a New Connection**'
  * Enter a **Name** for the connection, which you can easily identify.  I used reliance_lg.
  * For the next stage, unless you are absolutely sure that the DNS servers of the ISP are on static IP addresses, it would be better to use the **Dynamic DNS** option.
  * Reliance uses the **CHAP protocol**, which I had found out while using the Huawei Data Card.  Check with your ISP if in doubt.
  * Enter your **username**.  For the Reliance connection, it is usually the phone number of the connection.
  * Next, enter your **password**.  This is the same as the phone number/username.  Sad on Reliance's part, as I don't think we can change the password.
  * The next step is to set the modem port speed.  Leave it at **115200**, as it works well with this dialer.
  * **Tone** dialing is the next setting.
  * Set **'#777&#8242;** as the dialing number.
  * Select '**Yes**', to try to see if pppconfig automatically detects the port for your dialer modem.  It should correctly set it to **/dev/ttyUSB0**.  In case it doesn't, you can manually set it.  (/dev/ttyUSB0 will be the device node assigned to the dialer.  You can check if it exists as per the instructions on the Ubuntu Wiki page)
  * pppconfig asks you to confirm the settings before saving them.  You can just say 'Finished', or go into Advanced Options and play with things like Idle Timeout.  Save the settings after you are done with this.

These steps successfully configure the dialer.  Now, the last bit, dis/connecting to the internet with the dialer.

  * To connect, run the command `sudo pon <name of the connection>`.
  * You can check if the connection has been successfully made, by using `pppstats` or any network activity monitoring tool like `bmon`.  Also, the green indicator on the USB will light up.
  * To disconnect, run the command `sudo poff <name of the connection>`.  This command may not entirely kill pppd, as I've noticed a few times.  Before unplugging the dialer, check if any pppd process is still running by `ps -A | grep pppd` In case one is running, use pkill or kill to kill the process before disconnecting the dialer.

That does it!  If anyone can find the right Init strings for wvdial, please leave a comment.

P.S.: I've been terribly irregular on this blog.  The coming months are a lot less busy, and I promise to blog more often, and on things other than Ubuntu. :smile:

 [1]: https://help.ubuntu.com/community/DialupModemHowto/LXU800
