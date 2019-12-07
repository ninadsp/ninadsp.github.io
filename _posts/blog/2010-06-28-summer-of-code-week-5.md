---
title: 'Summer of Code &#8211; Week 5'
author: Ninad
layout: post
permalink: /blog/2010/06/summer-of-code-week-5/
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
Tasks done in Week 5:

  * **Modify the behaviour of all SQL pages so that the result of the query is retrieved via Ajax and displayed on the same page**:  A rudimentary script has been written to do this task, and hooked in on the Server, Database and Table SQL pages.  Fixed some jQuery conflicts with document.write() to get this working properly.
  * **Fix issues reported on the development list**: 
      * Use localized strings for messages in jQueryUI dialog using gettext.
      * Fixed bug noticed in PMA_ajaxResponse().
      * Fixed the bug due to which the database did not reload on renaming the database.
      * jQueryUI dialogs were not closed and removed correctly.  Fixed this.
      * Show the SQL query too when renaming a databse.  Modified PMA_showMessage() so that it will do this work.
      * Hooked in the validation function for Add a New User form.

Tasks for Week 6:

  * Complete the conversion to Ajax for the SQL pages and also paginate the results.
  * Test changes made till now, continue fixing bugs reported on the mailing list.
  * Figure out how to localize the jQueryUI Dialog buttons and make the necessary changes.
  * If time permits, modify the Database and Table Search pages.  This makes use of a logic similar to the SQL pages, and hence, should re-use the code written in this week.
