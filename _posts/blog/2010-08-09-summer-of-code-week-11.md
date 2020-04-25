---
title: 'Summer Of Code - Week 11'
author: Ninad
layout: post
permalink: /blog/2010/08/summer-of-code-week-11/
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
Ah! It's already the 9th of August over here. This means that we have come to the end of the coding period of the Google Summer of Code and work on documentation starts. A peek at the git commit log shows that I have covered most of the tasks I set out to do for this week:

  * Ajaxified the Change Password and Create Database actions on the main page.
  * Moved the code that sorted a table (of users/databases/tables) into a jQuery function, which is called after a new row has been appended to the table.
  * Added jQuery code that appends a new anchor to each row for inline editing.  It will be executed on a browser only if JavaScript is supported and hence, will leave most of the previous code untouched.
  * Completed the CSS rules for the Ajax notification.  The notification div is now properly centered and also has rules in the Darkblue/orange theme.
  * Fields with mimetype application, blob fields and images are now handled correctly in inline editing.
  * While testing inline editing, I realised that NULL fields were not handled properly.  Added a couple of checks that corrected the behaviour.

I could not complete the hooking in of some validation functions, as I had planned to.  However, I will do this as soon as I complete the documentation work that I have to do this week.

Things to do in the last week of the Google Summer of Code:

  * Document, document and document! 
      * Add JS-Doc compatible comments for all the newly written functions and jQuery scripts, and improve it from the very basic comments necessary for me to understand the code into proper documentation.
      * Document the newly added variables and code blocks in PHP as well.
  * If possible, I would like to add a page on the phpMyAdmin Wiki that explains what should be done to convert an existing action to Ajax using the functions that were developed over the summer.

The coming week might be the end of the Google Summer of Code, but I'm hoping that it will be just the first step in a long journey with phpMyAdmin.  In the next few weeks, it will be good to see some of the code getting merged into the upstream code, the main phpMyAdmin repository.  I hope that we don't cause too much trouble to the phpMyAdmin mentors when they review and merge our code! :smile:
