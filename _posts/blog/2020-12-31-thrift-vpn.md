---
title: Introducing Thrift VPN
author: Ninad
layout: post
permalink: /blog/2020/12/thrift-vpn/
categories:
  - Blog
tags:
  - Tech
---
The other day, I was looking at AWS's Spot Instance [pricing](https://aws.amazon.com/ec2/spot/pricing/) for different types of instances and noticed an interesting thing. A `t3a.nano` can be rented for as low as 0.0009 $/hour out of the Mumbai region, which comes out to approximately 50 INR per month. Even if we account for all the bandwidth costs that could add up, this turns out to be be less than 150 INR a month for a VPN box that you own and run yourself, which is among the cheapest rates one can find.

I've previously hosted [OpenVPN](https://openvpn.net/) on VPSes provided by different cloud service providers, and the lowest I could achieve was about 300 INR, which seems super wasteful for running just one or two services. This is at least 50% cheaper and seemed like an interesting opportunity to explore.

The primary reason my last VPN installation was junked wasn't the cost factor though. The certs that were used by the server and the clients had a one year validity, which expired right in the middle of some family emergencies. I never got around to regenerating the certs/keys and redistributing them to everyone at home. This meant I was looking for something that would work a lot more seamlessly. I was also not very fond of the OpenVPN apps available in the Android Play store.

This left me with a few options:

- [Nebula](https://github.com/slackhq/nebula/)
- [Zero Tier](https://www.zerotier.com/)
- [Tailscale](https://www.tailscale.com/)
- [tinc](https://tinc-vpn.org/)
- [Wireguard](https://www.wireguard.com/)

## Picking a tool

Nebula is a daily workhorse for me at work (Slack). None of my team's services would be possible without Nebula, and I'm somewhat comfortable with troubleshooting when things break. It's pretty good at traversing disparate networks and handling P2P traffic. However, running Nebula requires a bunch of associated infrastructure (which is provisioned and operated by a dedicated team at work) like a lighthouse (ideally, 3 is the minimum to handle instance failures, network blips and detecting malicious nodes in the network), and managing a Certificate Authority. The CA's role is to validate identities of the nodes in the network by some means of attestation and then handing out certificates for those identities. The folks behind Nebula have also recently published apps for iOS and Android, which is good news. I personally haven't run/used Nebula as a VPN service yet. It isn't rocket science, the OS just needs to allow packet forwarding for the packets that come from the nebula interface, but I've just not done it. As a result, Nebula was not on the final list.

Tailscale and Zerotier both provide some slick clients that can be installed across most OSes normal humans tend to use. However, as of today, they expect you to connect to one or more of their endpoints to perform the initial discovery/handshake. Tailscale mentions that they will eventually open source the entire stack, but that isn't true today. I wanted to run the whole thing myself, so these options were discarded. 

Tinc was another option that I considered, but discarded because the primary use case seems to be to act as a network mesh. As of today, tinc doesn't have a ton of choices for mobile applications. There's one app on the Android Play Store, and it's expensive (I'd end up purchasing multipe copies for everyone in my family and the costs will add up). In addition, the configuration for tinc definitely seemed better than the hassle that OpenVPN puts us through, but it was still not very intuitive. The best thing I liked here was that we no longer needed to rely on a certificate authority or any sort, and identity of nodes depended on standard pulic/private key pairs generated with an RSA algorithm.

Wireguard seems to be the choice that satisfies my requirements the best. Like tinc and nebula, it is good at handling nodes behind firewalls, and can do NAT hole punching where required. Unlike nebula, it does not have to depend upon a certificate authority, and it works on public/private key pairs. The documentation also explicitly mentions that the protocol supports roaming IP addresses, which was not something I'd seen in the choices above. There are first party as well as third party applications available for a wide range of consumer operating systems, which makes this pretty easy for me to set up on devices owned by my family members. The last thing that sold me on Wireguard was a note on one of the recent Android app updates, that it now includes support for Tasker. I've been using Taskfer for so long that I now take it's presence for granted.

## How to Spot though?

Running the VPN on an on-demand instance in Mumbai would cost about 0.003 $ per hour, or a little above 2 USD per month, which comes down to about 150 INR. I could either choose Mumbai, or Singapore as latencies to any other regions would be bad. My OpenVPN instance used to run in Northern Europe, and I used to have reasonable latency when I used it over a wired connection. However, the experience used to be pretty bad for cellular/phone networks. Which leaves me with these two regions. Of these, Mumbai is currently about half the prices as Singapore, and I'm currently interested in a secure connection till a major network hub only. I want to prevent the ISP snooping on my traffic. I don't want to worry about any advanced and/or persistent actors snooping on my traffic right now, I don't think I have the skills to prevent that.

Wireguard's configuration files are pretty simple. It is a bunch of `ini` files that contain information about the server's private/public keys, and the public keys for the various clients that are supposed to connect to it with some metadata about them. As long as I can get this configuration in place on a new machine, I am OK with AWS killing a spot machine, and then an auto scaling group bringing up another one for me. This can be achieved by creating a base Amazon Machine Image with Hashicorp's [Packer](https://www.packer.io/), providing a list of client public keys in the Auto Scaling Group's launch template and fetching the server's private key (that was previously generated on a different machine) via AWS's Systems Manager via a [cloud-init](https://cloudinit.readthedocs.io/en/latest/) script. One major limitation here is that it requires provisionign a new machine whenever a client is added/removed, but my current list of clients is expected to be fairly stable.

I could have used [this project](https://github.com/jmhale/terraform-aws-wireguard) by James Hale, but I wanted to build something that would work well with AWS VPC. Another thing I wanted to do differently was to use a different base AMI. Given that I'll be running this on an instance type that has super low memory, I wanted to pick a base distribution that had a very low footprint, as well as one that needed the least amount of hands on maintenance activity. I considered Debian and FreeBSD, and finally endeed up using Debian 10/Buster. Ubuntu's minimal images are also a pretty good bet, but I've always wanted to play around with these two distros. The terraform module by James is pretty good though, so I looked at it when stuck at specific issues.

## How to make it even cheaper?

All of this is pretty good for running a pretty cheap VPN. However, the typical Indian mentality was making me think about ways to make this even cheaper. James's terraform module has options to either use Elastic IPs or a full blown load balancer. Spinning up an instance in a public subnet in a VPC always gives us a free public IP address that is attached to the instance. This can change whenever our instance is killed, either due to issues with the underlying hardware, or due to changes in spot pricing. This is fine though, if I can tweak the cloud-init script to make an API call to my DNS provider and update a record to point to the current IP address. Lastly, there are some cheap TLDs out there (`.xyz` costs a dollar a year if you pick a domain with just numbers). Compared to Route53, this turns out a little cheaper and I don't need the Industrial Strength that AWS will provide for DNS. 

## Show me the code!

This project was spinning on the backburner for quite a while, but I eventually got time due to the Christmas/Holiday shutdown at office to get it to a usable state. The [thrift-vpn](https://github.com/ninadsp/thrift-vpn) project is available on Github and I have been using this for the past week or so on my mobile devices and personal laptop.

I'll spend time over the next few weeks tuning the firewall on the instance a little more, add an optional local `dnsmasq` installation (with support for DNS ad-blocking built in) and maybe sprinkle a bit of `fail2ban` to keep the tiny machine from being overwhelmed by random probes across the internet. Given enough time, I might explore running this on one of the Graviton instances, and I suspect this will work pretty well. In the meanwhile, I welcome feedback and tests from y'all to improve the user experience of this project further.
