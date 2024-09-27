---
title: Old Pi Gets a New Life
author: Ninad
layout: post
permalink: /blog/2024/09/old-pi-gets-a-new-life/
categories: [Blog]
tags: [Tech, Linux, raspberrypi]
---

I'd love to tell you the story of a project I've been pecking away at, for the past few days. It's a long, winding path, so I recommend brewing a cup of your favourite potion before you start reading the rest of the story. For the folks in a hurry, the TL;DR: is to just jump to the code snippets at the bottom!

## Why even do this?
I purchased a Raspberry Pi (Model 1 B) way back in 2013 to play with it. Over the years, I used it as a machine to host tiny projects, usually open source ones. Most of the time, it acted as a DNS ad-blocker on my network, and did a great job at it because it sports an ethernet port, consumes very little power, and works great if it is running a small set of applications. Some time in 2018-19, I was trying to run the [MagicMirror project](https://github.com/MichMich/MagicMirror/) and noticed that it took _minutes_ to just run an `npm install`. There are Many Reasons :tm: for why this was such a bad experience (slow processor, the crazy NodeJS ecosystem, a slow SD card, to name a few), but I decided to relegate the Pi to background duty, with DNS ad-blocking being it's sole purpose.

Come 2020, Covid happens, and I use some of the work-from-home setup budget to buy a good router (the Ubiquiti Edgerouter-X was a great deal while it lasted). It was definitely much better than the white labelled routers that ISPs sell, and it allowed me to customise the DNS server to take on the ad-blocking duties. Once this became reliable enough, the Pi had no purpose, and I decided to shut it down and throw it in the drawer.

I couple of years ago, I moved to a new house, which had a bunch of cameras hooked up to a Hikvision Network Video Recorder ([this model](https://www.hikvisionindia.com/product-detail/ds-7b08huhi-k1)). The NVR sits in a closet downstairs, and the display attached to it is mostly turned off, as there's no one there to monitor it. Whenever I've needed to monitor live feeds from the camera, I ended up using the HikConnect app on my mobile phone. This works great if I just want to check on a small thing, but it is fiddly, and I need to keep my phone handy. After spending an inordinate amount of time window shopping long cables on Amazon, I did not feel like committing to a) spending a bunch of money on unknown cable brands and b) ripping open some wiring conduits, or leaving wires hanging through this relatively new house. After some spelunking on the internet, I found documentation and forum posts where people streamed from the NVR over  over [RTSP](https://en.wikipedia.org/wiki/Real-Time_Streaming_Protocol). Eventually, I realised I could set up the Raspberry Pi at some place in the house where everyone can easily check in on what's happening outside the house, and I pulled it out of the drawer.

## The setup
I purchased a [Waveshare 4" LCD/Touchscreen display](https://www.amazon.in/gp/product/B0BRDDQNWY/) that can connect to the Raspberry Pi, and hooked it up to the Raspberry Pi. I then installed a fresh copy of the Raspbian OS, and I got the Lite edition as I'm usually comfortable enough with Linux that I can install whatever I need. The Pi booted, and I went ahead to install a bunch of different applications. The speed of processing reminded me once again that the Pi is a 10+ year old board with a very limited compute capacity even for it's time (every time there's a kernel update, and dpkg needs to go in and rebuild a bunch of things in `/boot` for it, I feel like the thing has hung). But, I also realised that after the initial setup, I will not need to fiddle too much with it, and hence, decided to swallow the goat and just proceed. I ended up installing some quality of life packages, and some stuff absolutely necessary for the project. See below for the final list of packages!

I initially started to follow the [camplayer](https://github.com/raspicamplayer/camplayer/) project, but realised that `omxplayer` is no longer supported on recent Debian/Raspbian versions. I backtracked, and then started looking at instructions on how to display video streams on Raspberry Pis. There's a bunch of blog posts and some Github Gists and repos that help with this. I barked up a few more trees, and eventually settled down on the simplest approach of allowing the OS user to log in at boot, start an X Server, and spin up VLC with the right video stream. It was relatively easy to get till this point, and I was encouraged by what I'd done so far. However, stuff always breaks when computers are involved. An old Raspberry Pi, a barebones X Server and Video streams are each individually capable of weird behaviours, and here I was, trying to work on the intersection of these 3 tricky things.

## The bumps along the path
1. I spent quite a few hours to get LightDM to automatically log in to a display, but it would always get stuck on the log in screen (the process seems to be called a `greeter`). No matter what configurations I tried, and how many times I rebooted, it would never land up on the desktop. So, I abandoned this path.
2. I used `raspi-config` (with the magic `sudo` word ofcourse), and followed [these](https://raspberrypi.stackexchange.com/a/76275) steps to automatically log in with the default user. This ensured that a `bash` shell process will always be started whenever the boot process of the Pi has completed.
3. Next up, I used the `.bash_profile` file/script to test if a display is actively connected, and I'm on the first terminal, and fired up our old friend, `startx`! This worked if I connected a keyboard directly to the Pi and interactively did it. But, it would fail intermittently when I did it as part of the boot process, and would fail with a `Connection Refused` error during `xinit`. After searching online, I learnt that this is not a rare error, but the contexts (OSes, preceding error messages, etc) are very different, and none of the solutions were relevant to my error. As it was failing intermittently, I pulled out the oldest tool in the box, `sleep 60`, and the X server started without fail every time after that. Since then, I experimented a little, and found that 30 seconds works, but a lower sleep window is not reliable.
4. Now that I could get the Pi to boot to X server and start the VLC process successfully (my guinea pig was the Blender Big Bunny file), I dove deep into making VLC composite multiple video feeds into a single stream (the Proper Term for this seems to be a `mosaic` of streams). At different points of time in the day, different camera feeds are interesting, and a single feed is usually not very useful if situational awareness is the goal. I followed tutorials to build `.vlm` files (see [this](https://wiki.videolan.org/Documentation:Streaming_HowTo/VLM/)) from the official VLC wiki, as well as blogposts, but the poor first generation Raspberry Pi could not keep up with 4 streams. I then poked around in the Hikvision Admin panel interface, as well as the RTSP URLs, and found out that channel '0' is a stream that the NVR itself composites and sends out. It is not exactly the feed I wanted, but something is better than nothing.
	1. Aside: Channels 1-8 are allocated to cameras that are directly connected over coax/analog cables to the NVR box. Channels 9 and above are assigned to any network cameras that you've added to the box. 
	2. For each camera, stream 1 is the main stream, while stream 2 is the sub stream. For my cameras, the sub stream does not have anything, but maybe your camera has something useful?
	3. The final format that you want to keep is: `rtsp://<username>:<password>@<NVR-IP-Address>/Streaming/channels/X0Y` where `X` is the Camera number, and Y is the stream number for that camera
5. Things looked great at this point, except that the display only showed a small part of the content that X server was rendering. And, it's orientation was off by 90 degrees. The way to fix this was by running a couple of `xrandr` commands in `.xinitrc` to explicitly set the framebuffer to 480x800 pixels (the size supported by the display), and then rotating it by 90 degrees. This looked right, and I started working on something else. In a little while, the display went blank, and I had to reboot the machine (I did not have any other alternative input sources connected at this point of time, and the touchscreen hasn't been configured). A little while later, I realised that this was happening consistently, and used the `xrandr -q` output to confirm my suspiscions. A screensaver was starting up, and the display was going to sleep. Thankfully, all these were features that could be turned off with a few more `xrandr` commands!
8. At this point in time, the Raspberry Pi booted, started up X and then VLC, and then played the combined stream from the NVR. Now, I wanted to control the VLC instance. This turned out to be trickier than I expected. I initially pulled out VLC's extended/advanced help, and followed the instructions on it. But, no matter what I tried, VLC would not activate the [remote control interface](https://wiki.videolan.org/Documentation:Modules/rc/).  I even went all the way to the VLC source code (on Github) and searched for the module, to figure out what I might be doing wrong. Like with many things software, a water break later, I realised that I was passing `rc` as the value to the `extraintf` parameter, but VLC was expecting it to be `oldrc` :facepalm:. Once VLC started with that, I could successfully play/pause/stop the existing stream over a local Unix socket file.
9. All this while, I had been starting VLC with a single RTSP stream's URL, and was hoping to use the remote control interface to enqueue the other one, and just switch over to that on a schedule. But, the `play` and `enqueue` commands never actually queued up the RTSP stream, and never returned an error. I suspect it has something to do with the username/password format of the URL, and I should open up the source code for this one to figure it out. For now, I decided to generate a playlist file (`.xspf`) on my local machine, and just copied it over to the Raspberry Pi. This works well enough for me!
10. The last piece of the puzzle for me, was to write up a cron script that would run regularly (I chose 5 minutes), query the currently running track, and see if it was time to switch to the other track. Parsing the current track is a precarious `grep` and `cut` pipeline, but until it breaks, I'm not gonna build anything better.
After this long and winding journey, I finally achieved my goal. And, you, my dear, patient reader, have almost come to the end of the story! We'll pick up some pieces that fell off along the way.

## What's next?
As you've realised by now, I've spent more than enough time for what was supposed to be a 2 day project (obligatory [xkcd](https://xkcd.com/1319/)). I do have a bunch of issues, but I'm gonna stop here, and come back to it when there's more time for this, or something breaks (are you ready to bet on the latter?).

I don't like the `sleep` hack, because it ends up spending a bunch of time after every reboot. I'd love to figure out what the underlying readiness condition is, and test for that instead of a dumb waiting period. And, maybe running a series of `xrandr` commands isn't the best way to deal with it. I should learn the `Xorg.conf` syntax at some point of time. The touchscreen bit of the display doesn't work, and I'm currently running VLC in full screen, no decoration mode. But, if I do get the input working (which depends on a working `Xorg.conf` again), I'd love to show the usual play/pause/next/previous controls on the screen.

Lastly, If I can't find any way to customise the content of the composite stream from the NVR, and I get really annoyed by the default setup, I'll probably just spin up another VLC (or ffmpeg) process on a more powerful machine running at home, and have that deal with the compositing. At that point of time, the Pi's VLC will just remain as a dumb display, and a lot of the logic can be shifted into something more elegant. Also, this opens up the possibility that I can have VLC on my phone fetch the same stream!

## TL;DR:

I have an Ansible playbook managing/configuring the Raspberry Pi. But, for the scope of portability (and the playbook having local IPs, user names, etc), I'm sharing the bits that matter. Feel free to copy these over, and use whatever tool you prefer (docker? nix? chef?) to manage the configurations.  The packages I installed atop a vanilla Raspbian Lite installation are:

```
* neovim
* tmux
* zsh
* curl
* wget
* ca-certificates
* vlc
* xinit
```

The `.bash_profile` file is:

```
if [ -z "$DISPLAY" ] && [ $(tty) = "/dev/tty1" ]; then
	sleep 30;
	startx
fi
```

And, the `.xinitrc` file contains:

```
#!/bin/bash
xrandr --fb 480x800
xrandr --output HDMI-1 --rotate right
xset s off
xset s noblank
xset -dpms
unclutter &
exec cvlc --no-audio --fullscreen --no-osd --extraintf oldrc \
	--rc-unix /path/to/vlc.sock --file-logging \
	--logfile /path/to/vlc.log --logmode text \
	--log-verbose 2 --loop /path/to/playlist.xspf
```

Lastly, the control script, invoked by cron:

```
#!/usr/bin/env bash

# Get current time
current_hour=$(date +"%H");

# Get currently running track

current_stream=$(echo "status" | nc -U /path/to/vlc.sock -q 4 | grep input | grep <NVR-IP-Address> | cut -d/ -f6 | tr -d '()')

if [ $current_hour -ge 16 ]; then
  if [ "$current_stream" == "001" ]; then
    exit
  fi
  VLC_COMMAND="goto 1"
elif [ $current_hour -ge 13 ]; then
  if [ "$current_stream" == "901" ]; then
    exit
  fi
  VLC_COMMAND="goto 2"
fi

# Run a cvlc remote interface to vlc.sock and send the command
echo $VLC_COMMAND | nc -U /path/to/vlc.sock -q 4
```
