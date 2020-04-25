---
title: 'Summer of Code - Week 12'
author: Ninad
layout: post
permalink: /blog/2010/08/summer-of-code-week-12/
categories:
  - Blog
  - Hobbies
  - PHP/jQuery
  - phpMyAdmin
tags:
  - gsoc
  - gsoc2010
  - jQuery
  - PHP
  - phpMyAdmin
  - pma-gsoc
---
And, it's finally over! :open_mouth:  My round up of the Google Summer of Code experience will have to wait a little, as I want to spend time compiling the exact changes I made, as against the ones I set out to do at the beginning.  However, here's my slightly delayed weekly report for the last week of GSoC.

  * Completed the documentation for the PHP files that I changed.  Added PHPDoc compatible comments for the newly added variables and functions.  Also added comments for the newly added/suppressed output for an Ajax request.  A quick grep for the variable $GLOBALS['is\_ajax\_request'] will point you to most of the files that have been changed over the summer.
  * Added documentation to the JavaScript files that I modified and created.  Most of the logic flow was already part of the comments, but the comments about the functions and variables were not JSDoc-Toolkit compatible.  Though I am having issues with getting JSDoc-Toolkit to capture the documentation in the jQuery namespace, in my recent experiments, I could get it to parse the variables and anonymous functions in two JS files.
  * Fixed a few minor bugs and typos that I noticed during the documentation.

I did not take out time to write the Wiki pages as I had planned for the last week.  After reading the [discussion][1] between Martynas and others on the mailing list, I'm considering putting some of the documentation in the Documentation.html page, and the detailed information on the Wiki, in the Devel category.

 [1]: http://sourceforge.net/mailarchive/forum.php?thread_name=4C670DD7.3040103%40gmail.com&forum_name=phpmyadmin-devel
