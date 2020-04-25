---
title: PHP, __FILE__ and symlinks
author: Ninad
layout: post
permalink: /blog/2013/07/php-__file__-and-symlinks/
categories:
  - Blog
  - PHP/jQuery
tags:
  - PHP
  - Wordpress
---
I've made this mistake so many times, that I have to note it down somewhere and not make it again.

**Problem:** I play with WordPress on and off, and use git (+Github) for version control. I clone the repository to my home directory, where I keep all my repositories, and then symlink the repository from the WordPress's plugin directory. However, all the functions that are used to derive the path to the plugin directory rely on the \_\_FILE\_\_ [magical constant](http://php.net/manual/en/language.constants.predefined.php "PHP Manual for Magical Constants"). The \_\_FILE\_\_ constant always resolves to the absolute path, which leads to a 404 error (if you're loading JS scripts), or worse, failed includes.

**Solution:** Clone the git repository directly to the plugin folder goddamnit!

Reference: [StackOverflow Answer](http://stackoverflow.com/questions/3221771/how-do-you-get-php-symlinks-and-file-to-work-together-nicely)
