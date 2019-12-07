---
title: 'ACAD &#8211; Amarok tips'
author: Ninad
layout: post
permalink: /blog/2008/08/acad-amarok-tips/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - Amarok
---
Amarok is the best audio player available on Linux, as those of you who have used it will agree. I personally rate it the best audio player available right now, better than iTunes, Winamp, and miles ahead of Windows Media Player. We'll have a look at some tips and tricks that will help you 'Rediscover Your Music'.

  * Scrolling over the Amarok Icon in the system tray will change the volume of Amarok. Holding *Shift* will scroll through the current track, while *Ctrl* will change tracks. Drag and drop a song to the icon and Amarok asks you whether you wish to Append it to Playlist, Play or Queue. Also, the amount by which the Amarok icon is filled indicates the percentage of track length completed.
  * Amarok, like the rest of KDE applications, has lots of Global Shortcuts. *Meta + X* will Play/Pause your music. *Meta + V* will stop your music. *Meta + Z* will go to the previous track. *Meta + B* will go to the next track. Also, these Global Keyboard Shortcuts can be customised to suit your tastes, just like most of the other KDE Applications can.
  * If you wish to enqueue a song already in your playlist, just press *Ctrl* and right click on the song.
  * Amarok has a very powerful *dcop* server interface. Here are some simple commands for the Player Function:  
    {% gist 6098996 amarok_tips.sh %}

  * Amarok has a very useful Lyrics Browser that searches on the internet for the lyrics of the song being currently played. Also, the Wiki Browser will get Artist, Title and Track Information from Wikipedia.
  * Typing a name in the search bar and pressing *Enter* will play the first song in the search result.
  * Amarok's *Cover Manager* will get the covers for all the Albums in your collection by searching for it on the Amazon database. Most of the covers downloaded are correct, and requires little manual intervention to complete the cover collection.

To find out more abut the dcop function calls available with Amarok, check out Amarok's help file. For those interested in building a collection above 1500 tracks, I suggest the use of a MySQL or PostgreSQL database to build your library. Though slightly slower than the SQLite database when being built, they are more reliable and are very fast when it comes to read and search queries. My collection of about 7000+ tracks runs happily in Amarok that has been playing for atleast 3 days as of now, without a hitch. And the search is lightning fast too. :smile:

And yeah, Amarok can also be used as a MP3/other file types tag editor. All you have to do is click on the relevant tag for the file, and retype it, just like renaming a file. I have correctly tagged more than half of my collection with Amarok, in batch processing mode. However, the batch processing mode isn't as fast as that of dedicated tag editors.

Amarok has lots of small but really useful features that will help you in 'Rediscovering Your Music'. I will surely have missed a lot of such things. Do find them and enjoy your music! :smile:

*Source for some tips is the Amarok Help*
