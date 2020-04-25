---
title: 'Summer of Code - Week 8'
author: Ninad
layout: post
permalink: /blog/2010/07/summer-of-code-week-8/
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
Tasks completed in Week 8:

  * Append newly created users to the list of existing users on the server privileges page and a newly created table to the list of tables on the database structure page:  **Completed**.  However, the newly created user/table are appended to the table, and hence, they are not placed according to their correct alphabetical order.  This is something that can be improved.
  * Start the ajaxification of inline editing of data retrieved from a table:  As expected, this is among the toughest tasks in my entire Summer of Code.  When I began work on this, I did not know about phpMyAdmin's Transformation feature, and it took me some time to figure out how to handle transformed and truncated data fields.  Also, relational fields might take some extra work to process.  The jQuery scripts for handling this are at a very basic stage, and the next week will be spent in coding the Ajax calls and handling the PHP side of this task.  There is a possibility that this task might extend beyond the two weeks allotted to this, but week 10 has simpler tasks scheduled, so I should be able to complete this feature well.
  * Fixing bugs mentioned on the phpmyadmin-devel list: 
      * Index not defined error for **$GLOBALS['cell\_align\_left']**, reported by Marc and Dieter has been fixed.  During an Ajax call, one of the files that generates the HTML head is not included, which was leaving this variable undefined.  Put in a check in the *PMA_showMessage()* function, where the error was being thrown.
      * Dieter suggested that I update the links/initials for paginating the users list shown on top, both when a new user is added and when the last user with a particular initial is dropped.  Completed this feature.
      * Also, pagination of user's list was facing caching issues, as Marc noticed.  Added a random variable that prevents this from happening.
  * Modified the *PMA_mysqlDie()* function to support Ajax requests and improved the error handling on *sql.php* and *Table Search* pages, a few conditions were not covered properly in the last week's code.

Tasks for Week 9:

  * Last week, I mentioned that I had fixed the bug that caused the empty notifications shown at times during an Ajax request.  It seems that I had caught only one of the reasons causing the bug, there's another condition that I'm trying to fix.
  * **Complete inline editing ajaxification**: Handle the transformed values as well as truncated and relational values.  Modify PHP code for the submission of the Ajax request.
  * Continue testing for bugs and fix them.
  * Find/figure out a better CSS styling for the notification division.  It does not stay centered when the length of the notification's message is more than 2 words.  Also, add similar styling rules to the Darkblue/orange theme.

And yes, yesterday, I received the mail confirming that I passed the mid-term evaluations for the Google Summer of Code! :smile:
