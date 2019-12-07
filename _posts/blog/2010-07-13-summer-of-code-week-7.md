---
title: 'Summer of Code &#8211; Week 7'
author: Ninad
layout: post
permalink: /blog/2010/07/summer-of-code-week-7/
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
Tasks completed in Week 7:

  * Converted the Insert page to Ajax.
  * Converted the Table Search page to Ajax.
  * Removed all remaining inline calls to confirmLink() and confirmAction() and modified the code so that jQueryUI's dialogs are used.
  * Fixed issues reported on the mailing list: 
      * The Ajax notification shown on the top of the page lingered at times, partly visible when it should have completely hidden.  Fixed it.
      * An empty notice division was generated whenever an SQL query was being retrieved over Ajax.  That div is no longer visible.

Tasks for Week 8:

  * Add newly created users and tables to their forms when on privileges and database pages respectively.
  * Begin modifications of inline editing of data retrieved from a table.  Create the necessary classes for inline editing and write jQuery scripts that will replace the HTML content with appropriate forms/input fields.  The PHP handling of the submissions will be covered in the next week.
  * Continue fixing the bugs reported on the developers mailing list.