---
title: 'Summer of Code - Week 10'
author: Ninad
layout: post
permalink: /blog/2010/08/summer-of-code-week-10/
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
Things have been a little slow the last week, thanks to preparations for a small family function today.  But, I did get a decent amount of time to work on the code last week.  Here's what the git commit log says:

  * Inline editing now supports handling of ENUM field types.
  * Almost completed inline editing support for relational key fields.  Just need to add support for current session settings of relational field display as key or column.  Currently, the display as key option has been implemented.  Also, included support for the $cfg['ForeignKeyMaxLimit'] setting while retrieving possible foreign key values.
  * Transformed fields with mimetype text/plain are handled correctly.
  * Fixed the bug noticed by Marc Delise, where field comments were being taken as part of the field name for inline editing.
  * Ajaxified the Create Database action on the Server Databases page.  However, the newly created database is not yet appended to the list of databases.

Tasks for next week:

  * Complete inline editing support for image/\* and application/\* mimetype transformations in jQuery scripts.
  * Add a new anchor for inline editing with jQuery on page load for each row, and remove the current inline editing action from the 'Edit' anchor.
  * Create Database action on the main page is not yet ajaxified, complete it and test it.
  * Ajaxify 'Change Password'.
  * Complete pending tasks.  This includes the long overdue CSS rules for the Notification division.
  * A couple of validation functions have not been hooked in correctly on some forms.
  * And, last but not the least, fix bugs that everyone on the mailing list so kindly points out!

Phew, that's a long list of tasks for next week.  See ya!  :smile:
