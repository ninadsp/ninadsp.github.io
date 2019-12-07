---
title: 'Summer of Code &#8211; Week 3'
author: Ninad
layout: post
permalink: /blog/2010/06/summer-of-code-week-3/
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
*Due to some issues at my hosting service, this blog post is appearing almost 2 weeks late.  I am extremely sorry for the trouble caused.*

Tasks for Week 3 and their status:

  * **Refactor JavaScript functions**:  Except for 4-5 calls to *confirmLink()*, and *confirmAction()* and *checkSqlQuery()*, all other functions listed on the wiki page have been re-factored with jQuery.  The corresponding inline calls to those functions have been removed and jQuery scripts written to handle the features.
  * **Handle submission of the &#8220;Add a User&#8221; form**:  Work in progress.  Testing the changes made, will be completed soon.
  * **Write a PHP function that standardizes response for an Ajax request**: Pending.
  * **Style the Ajax notifications div**: Pending.
  * Ajaxified Drop Table and Truncate Table actions on *db_structure.php*.

Tasks for Week 4:

Deliverable 4: Convert the Server Privileges page (*server_privileges.php*) to Ajax.  This includes the following work

  * **Add** a new user
  * **Revoke** a user
  * **Edit** privileges
  * **Export** privileges
  * **Paginate table of users**
  * **Flush Privileges**
