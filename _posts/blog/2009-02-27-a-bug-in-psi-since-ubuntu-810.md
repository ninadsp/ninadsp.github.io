---
title: A Bug in Psi since Ubuntu 8.10
author: Ninad
layout: post
permalink: /blog/2009/02/a-bug-in-psi-since-ubuntu-810/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - encryption
  - gpg
  - intrepid
  - key
  - Psi
  - Ubuntu/Linux
---
[Here's][1] a bug that I came across, when I was trying to enable GnuPG encryption in Psi today.

I'd configured my older install of Psi (on an earlier install of Ubuntu) to use my gpg key, but had later changed the setting back to using it without a key, as I was tired of entering the passphrase everytime.  Today, a renewed interest in cryptography prompted me to understand the working of the gpg system, and hence, was trying to add my key again to Psi.  However, it seemed that this experiment was destined to fail.  Google spewed results of various blogs and also the [Psi-wiki][2].  After following each step, I was still unsuccessful in enabling the gpg key.  The 'Select Key' button stayed obstinately grey.

Almost when I was about to give up, Google showed me the Launchpad bug.  A few minutes later, with 'libqca2-plugin-gnupg' installed, and after restarting Psi, we were back in business.  Now, I am not exactly sure I understood the circumstances of the bug, but my guess is that it happened when the Ubuntu cryptography architecture moved to QCA2.  Whatever it was, gpg support in Psi was broken, without any notification in either Psi or Ubuntu sites documenting this.  So, for the sake of documentation, all those who wish to use Psi on Ubuntu 8.04 or higher, please check if you need to install '**libqca2-plugin-ossl**' and '**libqca2-plugin-gnupg**' when you find that you are unable to use a gpg key.

 [1]: https://bugs.launchpad.net/ubuntu/+source/psi/+bug/212813
 [2]: http://psi-im.org/wiki/Encryption