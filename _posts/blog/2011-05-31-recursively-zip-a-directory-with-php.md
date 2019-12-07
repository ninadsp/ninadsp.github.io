---
title: Recursively Zip a directory with PHP
author: Ninad
layout: post
permalink: /blog/2011/05/recursively-zip-a-directory-with-php/
categories:
  - Blog
  - Hobbies
  - PHP/jQuery
tags:
  - archive
  - code snippet
  - how-to
  - PHP
  - zip
---
[Google's results][1] for code snippets to create a .zip archive with PHP gives quite a few results. However, none of the code examples can recursively compress a directory and replicate the same structure in the .zip archive. One [code snippet][2] from the PHP Manual's reference page for Zip functions comes pretty close, but the *RecursiveDirectoryIterator* never worked for me. The code always failed with an error about excessive recursion, with the script reaching the limit of 100 recursion levels.

Thankfully, after some more searching, I tried [another code snippet][3] from the same page, written by nheimann {at} gmx {dot} net.  With a little tweaking, the code worked perfectly. The class in the code snippet extends the [ZipArchive][4] class, and adds an **addDir()** public method. Example usage of this class is:

{% gist 6098996 flxziparchive_usage.php %}

The class in the PHP Manual's reference had a few missing variables. The correct code for the class is:

{% gist 6098996 FlxZipArchive.php %}

 [1]: https://encrypted.google.com/search?client=opera&rls=en&q=php+code+snippet+zip+directory&sourceid=opera&ie=utf-8&oe=utf-8&channel=suggest
 [2]: http://www.php.net/manual/en/ref.zip.php#80705
 [3]: http://www.php.net/manual/en/ref.zip.php#78940
 [4]: http://www.php.net/manual/en/intro.zip.php
