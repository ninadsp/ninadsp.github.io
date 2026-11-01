---
title: Replacing the battery on a 2013 MacBook Pro
author: Ninad
permalink: /blog/2026/11/battery-swap-mbp-a1502/
tags:
  - repairs
  - macbook
  - homelab
categories:
  - Blog
---

The first ever laptop that I purchased with my own money was a 2013 13" MacBook Pro. I had a good run with macOS on it, and Apple eventually dropped support for the hardware. The machine was still good (except for me breaking it's display very early on), so once I bought a newer machine, I converted it into a headless MacBook (or as some people call it, a slabtop) and installed Ubuntu Linux on it. The laptop stuck around as a toy machine, and eventually it's battery started to show its age. It would not hold its charge for long. More importantly though, the metal body of the machine started to feel odd, and it took me a few weeks to realise that it might have a swollen battery. After procrastinating for a while, I finally ordered a replacement battery on Amazon.

The battery arrived earlier this week and I opened up the iFixit [guide to replace the battery](https://www.ifixit.com/Guide/MacBook+Pro+13-Inch+Retina+Display+Late+2013+Battery+Replacement/27316). I have opened the machine before to remove the display, so I had the right screw driver and knew what to expect. As soon as the thing was opened, it was very clear that the battery was the problem. 13 years is a good (heck, great!) service life for a battery though. I was mostly worried about the adhesive that holds the battery in place, and how I would take it out, especially now that the battery is swollen. I did not purchase any adhesive removal solution either. After looking around in the house, I remembered that we have a [steel measuring scale](https://www.amazon.in/Stainless-Steel-Ruler-Inch-Foot/dp/B0FPRB1PBD) (many Indian houses have one and they last forever 
!). After nervously and carefully using the scale to separate the battery from the rest of the body, I finally heaved a sigh of relief. Installing the new battery was a piece of cake compared to extracting the old one, and I finally had the laptop closed down again. I finished this surgery earlier today and the machine is being charged for its first full cycle.

I'm contemplating what to do with the machine now that it is back to a working condition. I could hook it up to my semi smart TV (it has a YouTube app, but not many others), so I could run Jellyfin on the laptop and hook it up to the TV. I've already got DNS ad blocking running on the network, and my router acts as a tailscale node, giving me external access to my home network, the basic things are done. I might even get back to tinkering with FreeBSD! What are some interesting ideas for an old machine (without a working display) that you have seen?