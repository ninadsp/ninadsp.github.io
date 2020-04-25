---
title: 'The Summer of Code - Week 1'
author: Ninad
layout: post
permalink: /blog/2010/05/the-summer-of-code-week-1/
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
Week 1 of the Google Summer of Code is over and time is moving pretty fast.  Tasks completed this week:

  * Defined a global variable which will be checked for every Ajax request, and the output of pages will be modified depending on it.  Modified the files that generate the headers and the footers of a phpMyAdmin page, as well as some other files to suppress unwanted output in an Ajax request.
  * Wrote and tested a jQuery function to insert different HTML divisions from an Ajax response to the appropriate places on the page.
  * Created a list of JavaScript functions that can be refactored with jQuery methods.  Also created a list of major and minor tasks for each deliverable.  The entire list is now available [at the phpMyAdmin wiki][1], and is available for editing and feedback.
  * Ajaxify the 'Reload Privileges' action on the Server Privileges page, and test every change made till now.

A task that I have **not** completed from the last week's schedule is to write a PHP function, which will be used in tandem with the jQuery function mentioned above, to separate the various sections of the HTML output (e.g, profiling results, results table of an SQL query, the related print/bookmarking links).  As the client side code is now ready, I'll write the function this week.

Tasks for the next week are:

  * Refactor the functions in the list created this week.
  * jQuery helper functions to modify the header, footer, server links (etc.) divisions as well as to show notifications for an Ajax request (Processing request/Failed/Successful/Custom messages).
  * Build a wrapper(s) around jQueryUI's dialog() method, and standardize some dialog boxes (a simple confirmation box, a form dialog, an alert dialog and more as necessary).
  * Ajaxify the 'Add a User' action on the Server Privileges page and test the dialog box wrapper(s).

My schedule says that I will not be converting any pages/actions to Ajax before week 4, but I can't help trying out the changes I'm making and actually using them. :smile:

 [1]: http://wiki.phpmyadmin.net/pma/AJAXify_Interface
