---
title: 'ACAD - Psi 0.12 on Ubuntu'
author: Ninad
layout: post
permalink: /blog/2008/09/acad-psi-012-on-ubuntu/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - Compile
  - Psi
---
Here's what I was up to yesterday the entire night&#8230; I compiled the latest stable version of *Psi*, a Jabber client, just like Pidgin and Kopete. The latest stable release is **Psi 0.12** and it's source can be downloaded from [here][1]. I prefer Psi over the rest because it is as cross-platform as cross-platform can get. It is identical in functionality on Linux, Mac and Windows XP/Vista, and even the looks are comparable. I also like the iconsets that can be downloaded for Psi and it's sounds are delightful, unlike the dull sounds of Pidgin. :smile:

Now, the Ubuntu repository currently has the **0.11 dev-3** version. The debian package for version 12 has not been included in the Ubuntu repo's as of yet, even though it is now a part of the Debian Sid's repo's. The .deb can be found [here][2]. This will greatly simplify the installation process. All you will have to do is download the debian package from the appropriate mirror and install it using `dpkg -i [package name]`.

However, old-school Linux users prefer to *compile software from source*. Also, there is another reason to try compile Psi from source. People who have heard of the [Jingle project][3] will probably understand this. According to [this][4] source, it is possible to enable Jingle support in Psi while compiling it, and can hence be used to make calls to Google Talk users. Sadly, yours truly read the wiki page after he had compiled Psi 0.12. As of now, this project is on the back-burner, thanks to the brilliant exam schedules. :wink:

As most people who have used linux for sometime know, compiling is a simple three step process, where the user does not have much to do, except running the `configure` file, running `make` and then `make install`. However, for Psi, you have to take additional care, to ensure that all the dependencies are satisfied before compiling, thanks to the dependency on *Qt4*, which is not as prevelant as Qt3 is, on most systems. Here's a list of packages that you will need to install before compiling, all available in the Ubuntu repositories (source is [this][5] in the Debian Repo's.):

  * **debhelper** : Common tools to build/compile on debian based systems.
  * **libqt4-dev** : Don't forget the 'dev' ending for this and the next package. It is essential while compiling. If installing from the debian package, use the *libqt4* package only.
  * **libqca2-dev** : Same instructions as above.
  * **libxss-dev, libaspell-dev, zlib1g-dev, libsm-dev** : I am not sure if these are necessary for the debian package. But, they are a must for the compilation.

After having installed the above dependencies from synaptic or using the command line, it is a cakewalk to get Psi 0.12 running on your system. Here's what you do:

```bash
$ tar -xzvf psi-0.12.tar.gz
$ cd psi-0.12/
$ ./configure
$ make
$ make install
```

Congratulations! You now have Psi 0.12 installed on your system. The `./configure` step will create a decent amount of garbage on the screen. Ignore it as long as the configuration is successful. The `make` step will create tons of garbage on the screen, and will last atleast 3 minutes, depending on your system configuration, using a decent amount of processor. So don't get scared and press Ctrl+C in the middle of the steps. :smile:

Here's what you get in Psi 0.12 as improvements over the earlier version:

  * Search in Psi 'roster' (contact list) is improved, and it acts like a filter now, unlike the 'jump to' feature that it had before
  * A new config file, which can now be configured through Psi itself, as against the earlier versions, where you had to hand edit the file. This means, no hidden settings in Psi anymore!
  * Better support for multiple instances of Psi running together.

Anyone interested in helping out with the Jingle support in Psi, please leave a comment. I'll be glad for all the help that can come. :smile: Think about it. Linux users will be able to voice chat with Google Talk as well as other Jabber users, something that they have been denied for a long time&#8230; (There are quite a few other clients that have been working hard to integrate libjingle. However, I prefer experimenting with Psi as it's support is the best among them all.)

 [1]: http://psi-im.org/download/ "Psi Downloads"
 [2]: http://packages.debian.org/sid/i386/psi/download "Psi in Debian Sid"
 [3]: http://en.wikipedia.org/wiki/Libjingle "Jingle on Wiki"
 [4]: http://psi-im.org/wiki/Jingle_branch "Psi Wiki on LibJingle"
 [5]: http://packages.debian.org/source/unstable/psi
