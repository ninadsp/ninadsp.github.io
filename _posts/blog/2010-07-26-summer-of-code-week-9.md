---
title: 'Summer of Code - Week 9'
author: Ninad
layout: post
permalink: /blog/2010/07/summer-of-code-week-9/
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
Damn!  It's already the end of Week 9!  The Google Summer of Code has only 3 more weeks to go, and it feels as if it was just yesterday that I started working on phpMyAdmin.

Here's what happened last week:

  * Fixed the issue that caused an empty notification divisions on the top of the page during an Ajax request.  Used jQuery's .clearQueue() to dequeue all the previous animations when showing a new message, thus preventing it from showing a blank div after the content had been cleared.
  * Improved the behaviour for adding a new user, adding a table and deleting users.  The tables are now sorted, so the new user/table that is appended to the table is now in the correct alphabetical order.  Also, on deleting users, the classes of the remaining rows are re-adjusted so the table retains the uniform look of alternating dark and light rows, handled through CSS.
  * Newly copied users are appended to the list of users, just like newly created users.  Also, when a user's privileges are updated in the dialog, the table of users is updated with the latest privileges.
  * Saving of inline editing has been completed.  Any changes made during inline editing are now posted back to the server, and the table of results shows the latest value for the edited rows.  However, the edited values of relational fields and transformed fields need improvement.  Currently, the new value of the field is just shown over there.  It does not undergo transformation, or if it's a foreign key, it does not link to an SQL query that shows the foreign table with the key's row.

I still have not worked on the CSS rules for the Ajax notification, something that I wanted to do last week but could not, as inline editing has been quite complicated.

Tasks for Week 10:

The schedule says that I will be working on basic actions like Changing the Password and actions on the Database/Table Operations page.  However, inline editing still is not complete and some of the tasks for week 10 have been accomplished in the previous weeks.  Hence, after discussing with my mentor Marc Delisle, we've decided to complete and test inline editing as much as we can before GSoC ends, so that it can be rolled out in one of the coming versions.  Thus, this week, I'll be concentrating on improving the handling inline editing of all the transformations that phpMyAdmin supports.  Once that is done, I'll move on to the other tasks, as per availability of time.
