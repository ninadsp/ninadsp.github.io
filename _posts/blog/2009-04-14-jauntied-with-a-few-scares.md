---
title: Jauntied, with a few scares!
author: Ninad
layout: post
permalink: /blog/2009/04/jauntied-with-a-few-scares/
categories:
  - Blog
  - Hobbies
  - Linux/Ubuntu
---
This is the story of my laptop's upgrade from Ubuntu Intrepid Ibex to [Ubuntu Jaunty Jackalope][1] (currently beta) It started a few days ago, when I got hold of an alternate ISO for Jaunty beta, thanks to a fantastic downloader on our campus. (For those not familiar with the BITSian net, we are not supposed to download files > 20 MB and also the speeds are painfully slow.)  The ISO was dutifully mounted to the system and the upgrade started:  
{% gist 6098996 jauntied.sh %}
It asks me whether I want to include the latest packages from the Ubuntu repositories.  After a 'Yes', it downloads all the new package lists (which takes upto an hour).  The package lists sources are modified, newer package lists are downloaded, the upgrader calculates the size of downloads, and confirms it.  Now begins the tough game of waiting.  Downloading almost 1200 MB of packages at speeds that can range from 398 B/s (anytime between 1900 to 0300) to 60 kB/s (0500).  The result is that the connection breaks many times, and the entire upgrade process starts from step 1.  After struggling with the net for about 4 days, I finally have all the packages downloaded to my disk, and the actual upgrade starts.

After this, the computer runs at full steam for the next 2 hours, replacing, installing, removing and configuring various packages.  All this while, it prints a lot of gibberrish to the terminal screen, telling the world what it is doing.  This is when one notices the amazing simplicity and power of the Debian packaging system.  The magic of a few text files describing the entire tree of dependencies and a program understanding and processing all this into a meaningful suite of programs is just overwhelming.  Once in a while, a small screen pops up, telling me that I have changed a configuration file, and whether the installer should keep it or replace it with a newer version.  This is dispensed with quickly by doing a side by side comparison of the files.  When it completes it's job, the upgrader asks whether I want to keep the system running, or should it reboot the system.  I was surprised, that the entire process got over with just one error with a package, which I was able to fix with a dpkg command when the upgrade got over.  Now is the time for surprises.

The computer shuts down and starts up again.  The GRUB menu comes up, and shows me Jaunty (saying that it's a development version, making things loud and clear at the start).  The system boots up normally, and I reach the login screen of GDM.  The login screen of Ubuntu Studio is jaw dropper.  I login, and this is where some of the troubles start.  Konsole absolutely refused to respond, and Plasma, the desktop of KDE4 was behaving very wierdly.  None of the widgets from my earlier install were visible.  So, I logout and go to GNOME, my failsafe option.  Konsole stayed the same, and Gnome Terminal too joined the fray.  However, it did help a little by displaying an error &#8220;There was an error creating the child process for this terminal&#8221;.

The terminal, one of the most important parts of any *nix system, had become completely inaccessible.  And I for one, rely a lot on the terminal, to do most of my System Administration work. The Update Manager of Ubuntu, which sits in the Gnome panel, and one that I rarely use, too gave me the same error when checked it for updates.  Googling around pointed me to two places, one a Launchpad Bug about SSH errors, and another error on a forum.  The solution was to add a line to /etc/fstab, so I tried doing the same process by issuing a command, using one of the terminals in the Ctrl+Alt+F1-F6 range.  But, it did not work.  So, I added the line to fstab, and rebooted.  Issue fixed, the terminal started happily.  Next up, I set about checking all the configuration files for the LAMP stack, my firewall, and started Desktop Effects again.  Even with an ATI onboard, I had absolutely no problems, thanks to the open source radeon driver, which has been doing service on this machine for quite some time.  With a working desktop, Ubuntu Jaunty was running on my system.  It's been almost 2 days now, and it's running with no hiccups.  Psi did trouble me a little, but recompiling it to Jaunty fixed it, and I am back to the stable system that I had a week ago.

Overall, Jaunty is brilliant.  The boot speed has improved quite a bit, which was one of the targets of Jaunty Jackalope.  It is surprisingly stable for a beta version of Ubuntu, and it is one of the most stable Non LTS versions I have seen in Ubuntu since I've started using it.  There is only one thing that saddens me.  Amarok 1.4 series is no longer available in the repositories of Ubuntu since Jaunty, and I'll miss it.  Amarok 2 still needs some work, and is slightly unstable with my playlist of 7000+ songs.  Also, the UI of Amarok 2 is not upto the same mark as Amarok 1.4 series.  Hope it improves soon.  This entire story taught me how to report [a bug][2] on Launchpad, with help from a couple of great guys on the #ubuntu channel at Freenode, for which I am eternally greatful.

As of writing, there are 9 days to go for the final release of Jaunty! :smile: Leaving you with a screenshot of the Ubuntu Studio GDM screen. (Credits to whoever has made the image, I have just uploaded it and it is not my creation.  This pic is a part of the ubntustudio-gdm-theme)

<div id="attachment_327" style="width: 310px" class="wp-caption aligncenter">
  <a href="{{ site.baseurl }}/images/2011/03/background.jpg"><img class="size-medium wp-image-327" title="background" src="{{ site.baseurl }}/images/2011/03/background-300x187.jpg" alt="Ubuntu GDM Theme" width="300" height="187" /></a>
  
  <p class="wp-caption-text">
    Ubuntu GDM Theme
  </p>
</div>

<p style="text-align: center;">
  &nbsp;
</p>

 [1]: http://www.ubuntu.com/testing/jaunty/beta
 [2]: https://bugs.launchpad.net/ubuntu/+source/gnome-terminal/+bug/360160
