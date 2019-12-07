---
title: 'The Summer of Code &#8211; Week 2'
author: Ninad
layout: post
permalink: /blog/2010/06/the-summer-of-code-week-2/
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
Tasks for Week 2 of the Google Summer of Code, and their status:

  * **Refactor functions from the list created** : Some functions from the list are yet to be refactored, as I am trying to understand where and how they've been used.  Netbeans, Firebug and *git grep* have been really useful in figuring out how things work.  Also, some functions from *js/common.js* are implemented so well, that I believe jQuery's implementation might add unnecessary layers of abstraction and thus affect execution.
  * **jQuery helper functions to modify the header, footer, server links (etc.) and to show notifications for an Ajax request** :  The notification needs to be styled, and the function should be improved so that only the latest notification is shown, instead of the multiple notifications being shown currently.  Also, the *PMA_ajaxInsertResponse* function (written last week) can be used to update the header, footer and server links divisions.
  * **Build wrappers around jQueryUI's dialog() method** : 
      * Wrote a function which does the same work as *confirm()*, asks the user a question with jQueryUI's dialog, then makes an Ajax call at a given url and executes a callback function when the Ajax request completes successfully.
      * I did not find any action/situation (yet) where I need just an alert box, and not ask for a confirmation and hence, have not yet written a function for it.
      * As for dialog boxes for the form, I am not sure if a standard jQuery function will be sufficient, as each form will require different handling.  If I do come across similarities in the handling of forms, I'll write a function which can be re-used.
  * **Ajaxify the &#8220;Add a User&#8221; action on the Server Privileges page** :  The dialog is constructed by making an Ajax call and retrieving the new user form.  The submission of the form is yet to be handled.  There are issues about repetition of some HTML ids, which is confusing jQuery, will fix them soon.

Tasks for Week 3:

  * Continue re-factoring  the existing JavaScript functions to use jQuery code and replace the inline JavaScript calls to those functions with jQuery scripts that attach events to the form/button elements.
  * Handle the submission of the form for the &#8220;Add a User&#8221; action.
  * For all the actions affected while refactoring confirm* functions, modify the PHP code to produce standard output, which the *PMA_confirm()* function can understand as success/failure of the request, making it more robust.
  * Style the notifications and improve the notification function.