---
title: 'Summer of Code &#8211; Week 4'
author: Ninad
layout: post
permalink: /blog/2010/06/summer-of-code-week-4/
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
*Due to some issues at my hosting service, this blog post is appearing almost a week late. I am extremely sorry for the trouble caused.*

Tasks done in Week 4:

  * Improved the PMA_ajaxShowMessage() function.  Now, multiple messages won't be shown at the same time.
  * Ajaxified Rename Database, Copy Database and Change Database Charset actions on db_operations.php
  * Ajaxified Flush Privileges, Revoke User, Export Privileges actions.
  * Wrote a PHP wrapper function for generating JSON responses in an Ajax request.
  * Ajaxified Drop Column, Add Primary Key actions on tbl_structure.php.
  * Asked the phpMyAdmin developers mailing list to provide testing feedback on changes made till now.

Tasks for Week 5:

  * Modify all SQL pages where the user enters an SQL query and retrieve the result via Ajax.
  * Fix issues reported while testing by the developer mailing list.
