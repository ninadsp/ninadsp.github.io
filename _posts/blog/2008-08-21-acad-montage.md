---
title: 'ACAD - montage'
author: Ninad
layout: post
permalink: /blog/2008/08/acad-montage/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - ImageMagick
  - montage
---
Well, here goes the post on montage, as I had promised yesterday. Before we have a look at montage, we'll have a look at **ImageMagick**. It is a suite of image editing tools, that can do almost anything to over a **100(!!!)** different types of bitmap images. It is most popular for it's ability to batch process files, support for a scripting language and hence has found it's way to many sites that require some sort of image editing. You can see ImageMagick at work at the Photography Club Gallery.

The command *montage* is used to compose several images into a single image. It also accepts options to put a border around the frame, give each image it's title, and some generic ImageMagick options like back ground colour, shadow, etc. Here's how I made the composite image: {% gist 6098996 montage_1.sh %}

The files that Psi caches are kept in the '*/home/user/.psi/avatars*' folder. The next command tells montage the following things:

  * The *background* of the composed image is the colour #9DAABA. It is a standard format for describing the RGB colour space with hexadecimal values. Don't forget to escape the value with quotes (double or single) otherwise, the shell doesn't pass the value on to montage, instead, it tries to interpret it, and you won't get the expected result.
  * The next option tells montage to put a *frame* of width 10 pixels around every image.
  * The *mattecolor* option gives the frame #FFFFFF (white) colour.
  * The last option puts a *shadow* to the image. You can specify the opacity as well as the direction in which the shadow falls.
  * The next part '\*' tells montage to use all the images in the current folder while making the composite image
  * The last part is the name and location where montage has to store it's output image.

Other options that are available with montage include:

  * Give a border of specified colour to each image.
  * Give captions to the image.
  * Blur images used. This is a generic ImageMagick option, as most of these options are.
  * Annotate images with coments
  * To know more about the options, check out the documentation of ImageMagick. The above information is not at all exhaustive. Infact, it is a very little part of the command that I have understood.


*Note:* Being an image editing tool, one should use these tools carefully. As all the images used in the above example were really small (96&#215;96 pixels), it wasn't too much of sweat for the computer. It took about a minute and a half of almost 50%+ processor usage and a decent amount of RAM and Swap memory. Be careful while batch processing large files. It can wreak havoc on your system. I tried something foolish once but thankfully, I stopped the montage process before it could use up my entire RAM and Swap. They are jobs best left for powerful servers.
