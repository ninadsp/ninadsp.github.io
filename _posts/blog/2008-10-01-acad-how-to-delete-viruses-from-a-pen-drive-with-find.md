---
title: 'ACAD &#8211; How to delete viruses from a pen drive with find'
author: Ninad
layout: post
permalink: /blog/2008/10/acad-how-to-delete-viruses-from-a-pen-drive-with-find/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - find
  - Linux/Ubuntu
  - rm
  - viruses
---
Pen drives or thumb drives, are the most susceptible to computer viruses (Windows based), and they are the most popular way today for a virus to spread. Being small, handy, and convenient because they run on USB, they are used on a large scale by everybody. Viruses which infect them, follow a particular pattern of infecting them.

Some '*benign*' viruses tend to affect only the root of the drive, and create an *Autorun.inf* or a *Autorun.exe* file in the root of the drive. However, most of the viruses, being viruses, try to affect each and every folder on that drive. The first type can be very easily dealt with. However, the second type can be a very difficult type to deal with, when you have a large pen drive, and a deep hierarchy of folders. Here's where the command line of Linux comes in handy. I use the following command to rid my drive of the viruses:

```bash
$ cd /media/disk
find . -regex *.exe -exec rm "{}" +
```

The above command works like this:

  * The first command changes my working folder to the pen drive. This could also be any other partition that has been affected by a virus.
  * The **find** command will print the names of all files in the specified directory, which is '**.**' or current working directory here.
  * The **-regex** option, as some of you might know, will search for the regular expression **.exe** in all the files.
  * The last option, **-exec** will execute the specified command on all the files which the previous options present. Here, we are using the **rm** command to delete the files. The `+` operator will catenate all the filenames and make it into a single command of **rm** with a long list of files.

This set of commands can be made more elaborate with a shell script to check the existence of the _Autorun_ files using file tests. I haven't tried to do that as of yet, but I'll infect my pen drive soon, just to get this thing working. :wink: Hope that this will make it a little easier for you to rid your and your friend's systems of viruses.

**P.S.**: The above set of commands will delete **ALL** files ending with *.exe* from your drives. I suggest not using this on anything other than thumb drives, and if you plan to use it on a hard disk partition, consider using the **-ok** option, instead of the **-exec** one. Make a back up of all your important .exe files from your drive before experimenting with this.
