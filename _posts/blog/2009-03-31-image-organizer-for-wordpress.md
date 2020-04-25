---
title: Image Organizer for WordPress
author: Ninad
layout: post
permalink: /blog/2009/03/image-organizer-for-wordpress/
categories:
  - Blog
  - Hobbies
tags:
  - application
  - gsoc
  - Wordpress
---
This is my revised application for Google Summer of Code at WordPress. Please feel free to post your comments/suggestions:

**Project Proposal**

My aim is to work on improving the user experience for images in WordPress. The idea has been suggested on the GSoC 2009 ideas page of WordPress as well as on [this][1] ideas page, by LSabin.

I hope to do this by developing a plugin that implements most of the functions as those found in [this Organizer][2] plugin, using JQuery and ImageMagick/GD, alongwith PHP. Hence, to summarize, I'll be implementing:

  1. **Batch/single image upload**: Take the current uploader (wp-admin/media-upload.php) as a base, and patch it/rewrite it to be suitable to this plugin. Primarily work at making it a batch uploader, and have asynchronous uploads (upload images one by one, while the user selects more images and sets their properties), as uploading all images in one go can fail on slower connections.
  2. Batch/single **image resizing, thumbnailing and adding of watermarks**: This could have 2 possible implementations.  
  2.1. First involves a higher load on the server : The interface sends a request to the WordPress server, which generates a low quality preview, which is displayed to the user, before he commits his changes.  
  2.2. The second implementation would use a JQuery plugin/function to generate accurate previews (Examples: [1][3] OR [2][4] ). After the user commits the change, the interface communicates with the server the required parameters.  
    In both the cases, after the user commits, the server processes the requests and saves the processed images.
  3. A **directory and image management module** that allows the user to copy/move/delete directories and images, simultaneously updating the posts to point to the newer locations. Provide hooks for including User Permissions.  Use the code of Organizer as a base and improve it to use the API from newer versions of WordPress i.e. update the code.
  4. Batch/single **image framing, collage/montages, sketch generation** using ImageMagick or GD : This too will be implemented by generating a preview from the server, after which the user commits. For the framing and sketch generation, the user will be able to play with the options, using JQuery sliders, and then get a preview. For the collage and montage, I hope to implement a UI where the images will be draggable and resizable (JQuery UI). *The collage and montage are an optional part of this point.*

As the interface will be implemented using JQuery and AJAX, the user will be provided with previews of the changes he is making, hence improving the overall user experience. As a result, even a user with minimal experience in processing images will be able to blog with ease, without worrying too much about the nitty gritty of image manipulation programs. Also, this will be a part of the WordPress interface, that he is so familiar with and comfortable in.

**Schedule of Deliverables**

  * **Pre-GSoC period (April 20-26):** Familiarize myself with JQuery UI and WordPress code. Read up developer documentation and understand the relevant filters, actions and functions.
  * **May 1-16:** College Comprehensive Exams.
  * **First week (May 23-30)**:Study some more WordPress code, paying specific attention to image handling functions from wp-includes/media.php, wp-admin/media-upload.php and Organizer plugin. Also, read up on making a plug in. Decide whether to use ImageMagick or to stay with GD, in consultation with the Mentors.
  * **Second & Third week (May 31- June 13)**: Figure out SVN and try out a few 'hello world' things first with it. Understand the PHP API of ImageMagick and relate that to the commands or Understand GD depending on the previous week's decision. Code #2
  * **Fourth week (June 14-20)**: Code #4 - the image framing and sketch-ify functions.
  * **Fifth & Sixth week (June 21- July 4)**: Code #1
  * **Seventh & Eighth week (July 5-18)**: Review, test and debug work done till now. Do various tests on the File Upload, and also on the Image Processing across platforms. Document the work done. Also, time for GSoC midterm evaluation.
  * **Ninth & Tenth week (July 19-August 1)******: Code #3
  * **Eleventh week onwards (August 2 ****Onwards. No new coding after August 10)**: Work on integrating all of the above as a single plugin, testing and debugging of the code. Clean up code. Document. Add collage/montage from #2 and inline help if time permits.
  * **August 17**: GSoC 'Pencils down'

**Open Source Development Experience**

Confirmed a bug on Launchpad.net related to the Ubuntu patched Linux kernel. Regular contributor to the [Ubuntu India mailing list][5] since last 3 months. Coded a site for a student activity that I am a part of, using PHP/MySQL/AJAX. Currently helping in the testing and design (graphics) of an online notice board for the internal network at our college, being developed by the Software Development and Education Technology Unit at BITS, Pilani.

**Work/Internship Experience**

None

**Academic Experience**

Studying M. Sc. (Tech.) Finance, 3rd Year

**Why WordPress?**

I have been a WordPress user for a year, even though I am not a regular blogger. The simple, clean interface and the extensibility of WordPress through it's various extensions simply amazes me. Having learnt PHP and JQuery and played with ImageMagick for sometime, I really hoped to get an opprtunity to give a helping hand to WordPress, and GSoC gives me the chance to start off. Also, I find that the answers to majority of the 5 questions posted on the [GSoC wiki][6] about selecting an organization, are a resounding yes.

*Template used : http://codex.wordpress.org/GSoC\_2009\_Application_Template*

*Last Edited : 15:40 AM, 3 April, IST*

 [1]: http://wordpress.org/extend/ideas/topic.php?id=74
 [2]: http://imthi.com/organizer/
 [3]: http://interface.eyecon.ro/demos/resize.html
 [4]: http://www.webmotionuk.co.uk/php-jquery-image-upload-and-crop-v11/
 [5]: https://lists.ubuntu.com/mailman/listinfo/ubuntu-in
 [6]: http://code.google.com/p/google-summer-of-code/wiki/AdviceforStudents
