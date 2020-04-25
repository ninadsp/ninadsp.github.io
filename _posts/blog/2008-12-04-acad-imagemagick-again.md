---
title: 'ACAD - ImageMagick again!'
author: Ninad
layout: post
permalink: /blog/2008/12/acad-imagemagick-again/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - designs
  - ImageMagick
  - Linux/Ubuntu
  - Shell Script
---
Here are the results of a *vetti* afternoon after a pathetic (read Optimisation Techniques) comprehensive exam:

<div id="attachment_324" style="width: 234px" class="wp-caption aligncenter">
  <a href="{{ site.baseurl }}/images/2011/03/poloroid_spread.gif"><img class="size-full wp-image-324" title="poloroid_spread" src="{{ site.baseurl }}/images/2011/03/poloroid_spread.gif" alt="Polaroid" width="224" height="296" /></a>

  <p class="wp-caption-text">
    Polaroid of images
  </p>
</div>

*ImageMagick simply rocks!!!* Here's the source code for the whole thing:  
Shell script to generate the image with the number on it  

{% gist 6098996 imagemagick_1.sh %}

### Code to put them all together into a single file with the polaroid-like frame around it:

{% gist 6098996 imagemagick_2.sh %}

The second half is a complete rip-off from [here.](http://www.imagemagick.org/Usage/thumbnails/ "Imagemagick Examples") The first script is also based on the examples from ImageMagick.  The examples are awesome!

The sole reason behind me spending my entire afternoon educating myself (i.e. not studying):  I wanted a series of snaps to be put up on my Gtalk account.  Everyone on my list, do watch out for *the Compre Countdown*! :stuck_out_tongue_winking_eye:
