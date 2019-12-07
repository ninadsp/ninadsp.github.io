---
title: Upgrading to Lucid at the BITS Network
author: Ninad
layout: post
permalink: /blog/2010/05/upgrading-to-lucid-at-the-bits-network/
categories:
  - Blog
  - Hobbies
  - Linux/Ubuntu
tags:
  - how-to
  - karmic
  - Linux/Ubuntu
  - lucid
  - pilani
  - Ubuntu
  - upgrade process
---
Canonical recently released the latest version of Ubuntu, **Ubuntu 10.04 Lucid Lynx**.  It is an excellent upgrade to Ubuntu, with some nice features and UI/UX improvements on GNOME.  KDE too has had quite a few improvements, with the latest KDE4.4 SC being included in the final release.  Reviews of the distro can be found pretty easily on the net, as Lucid, a *Long Term Support release*, has been eagerly awaited.

Here's a quick post on how to upgrade to the latest version of Ubuntu, while on the BITS Pilani Network.  The reason for the need of a separate post is the weird network policies implemented here, with an honest attempt to prevent wastage of the band width for illegal downloads.  Without further ado, let's get our hands dirty and finish this task.  ***Read the entire post till the end, and only then, proceed with the task of actually upgrading your system.***

## <span style="color: #ff0000;">Warning: Not a task for the faint hearted.  Involves a fair use of the command line, and can lead to a highly unstable system if not completed properly.  Can lead to a completely fouled up upgrade.  Proceed at your own risk.</span>

The steps that we will follow have been outlined at [this][1] page on the Ubuntu Wiki.

  * **Set the correct proxy**.  BITSFOSS has a apt-cacher running on it, as most of you know.  Please use it for this upgrade, as you will get good speeds, and most probably, 90% of the debian files you need will already be cached there, during upgrades by other BITSians. `$ export http_proxy="http://bitsfoss:3142/"`
  * **Update the current install** of Karmic to the latest state `$ sudo aptitude update && sudo aptitude safe-upgrade`
  * This step is a very important step.  Please do it carefully, as your system can reach a no-return point after this.  We need to **update the package sources** by editing the *sources.lst* file and *sources.lst.d* folder.  As a caution, we first disable all third party sources by backing up the current sources.lst.d and making a new, empty folder. {% gist 6098996 lucid_upgrade_1.sh %}
  * Now, we need to update the current package sources to point to Lucid repositories instead of Karmic ones.  Do that with the following command : `$ sudo perl -p -i.ORIG -e 's/karmic/lucid/g' /etc/apt/sources.list`
  * Update the package sources so that your system has the information from the Lucid repos. `$ sudo aptitude update`
  * Update the base packages (dpkg, apt and aptitude). Do a **safe upgrade**, and then do a **full upgrade**. {% gist 6098996 lucid_upgrade_2.sh %}
  * The above step of safe upgrade and full upgrade might need to be repeated, till aptitude gives the message that no packages have been left for upgrading.  The total time required for this will be close to 3 hours, which includes some download time and a lot of installation/upgrade time for packages.  This time required will vary, depending upon the number of packages installed on your OS.  I have a wide variety of applications for both KDE and GNOME, and hence, required close to 3 hours.  Your upgrade might finish sooner, or later.
  * Once all the packages have been updated, reboot the system, and cross your fingers.  If the upgrade has been successful, you will be greeted with the brand new, beautiful themes of the Ayatana project, and Lucid will be running on your system.
  * After you have tested that all the basic things are running fine, you can re-enable the third party repositories by copying the files from the backed up *sources.lst.d* folder to the new one, and editing them to point to the Lucid repos.

While going through the above process, close down all applications other than the bare basic necessary, as the upgrade process affects a lot of applications, and can cause strange crashes if too many applications are running, damaging your data.  Also, taking proper backup of your data before embarking on an upgrade is a must.  Even though the upgrade process has been improved over the last 2 years, there are still quirky configurations of hardware, which can lead to issues.  Hence, secure your data before doing an upgrade.

While doing this upgrade, I faced a bug, which was a show-stopper to the entire upgrade process.  It has been [documented][2] at Launchpad and also been discussed at [this mailing list][3].  If you face errors with a libatk and libgtk conflicting with some packages, please follow the steps outlined at both the places.  The steps have been mentioned for libatk, the same steps apply for libgtk.  The fix has been committed, but the packages had not been updated when I upgraded my system (30-April-2010).  As far as I know, the packages have still not been upgraded in the repos.  Also, there has been a bug reported about memory leaks in Xorg (or the Kernel, I'm not sure if I understood the bug report correctly), which leads to a hung system once every day or two.  The patch that caused the regression has been located, and efforts are on to fix this issue upstream, instead of just fixing it in the Ubuntu repos.  The only way to reboot your system is to use the *MagicSysRq* keys.  Google for the Ubuntugeek tutorial on how to use these keys once you have upgraded.

Hope all you guys get upgraded to the all new, beautiful Lucid.  I am really excited at the [directions Ubuntu is taking][4], and the next release, the Maverick Meerkat is expected to shake quite a few of our conceptions about the desktop that we see today.

P.S.: Best of Luck for the rest of the Compres and have a great Summer Holiday! :smile:

 [1]: https://help.ubuntu.com/community/Upgrades#The%20Debian%20way%20of%20upgrading "The Debian way of upgrading"
 [2]: https://bugs.launchpad.net/ubuntu/+source/atk1.0/+bug/547244 "Lanchpad Bug report"
 [3]: http://www.mail-archive.com/ubuntu-bugs@lists.ubuntu.com/msg2234515.html "Mailing List discussion of the bug"
 [4]: http://www.markshuttleworth.com/archives/333 "Windicators"
