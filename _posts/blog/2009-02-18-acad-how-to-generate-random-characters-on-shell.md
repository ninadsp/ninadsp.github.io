---
title: 'ACAD - How to generate random characters on Shell'
author: Ninad
layout: post
permalink: /blog/2009/02/acad-how-to-generate-random-characters-on-shell/
categories:
  - Blog
  - Linux/Ubuntu
---
I was making a few files yesterday, which I needed to be filled with garbage.  As I was working in good old BaSH, I was not in a mood to go to either C or any other language, as i/o redirection would have been a little complicated.  [Google][1] came to the rescue, and I found this brilliant way:  
`~$: hexdump -n100 -e\"%u\" /dev/urandom > file.txt`  
Here's how it works:

  * **/dev/random** and **/dev/urandom** are the Linux Kernel's random byte generators.  The first is the better one, however it requires a lot of keyboard/mouse activity on the system to give a good output, and is only meant for use when security is of the essence.  This would include SSH key generations, and other cryptographic work.  For our purpose, urandom is sufficient.
  * **hexdump** will convert the random binary data that /dev/random gives, into various formats.  Here, we use the **-e** switch to convert it into ASCII characters (specified through **%u** quoted and escaped).  **-n100** limits the number of characters that the hexdump reads from */dev/urandom* to 100.  Check out the man page of hexdump for further options.
  * The last bit redirects the output to the file specified.

There you go!  A simple way to fill files with garbage.  One brilliant, but potentially harmfull use of this can be to pipe this output to netcat, and create a heavy traffic on your LAN, which is pure garbage.  Find out more if you wish to do that. :wink:

By the way, if you just need a random number, you can use the shell variable **$RANDOM** to give you a random number, each time it's accessed.  This can be useful to create pseudo-random lock files in */tmp* for a script that you might need locks in.

 [1]: http://google.co.in "Google"
