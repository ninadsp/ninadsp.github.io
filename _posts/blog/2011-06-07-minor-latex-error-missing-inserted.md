---
title: 'Minor LaTeX error &#8211; Missing $ inserted'
author: Ninad
layout: post
permalink: /blog/2011/06/minor-latex-error-missing-inserted/
categories:
  - Blog
  - Uncategorized
tags:
  - error
  - LaTeX
  - note to self
---
While creating a document in LaTeX today, I came across this strange error: '**Missing $ inserted&#8230;**'.  I checked the syntax everywhere, but could not figure out what was wrong.  I checked the LaTeX WikiBook's page on [Errors and Warnings][1], which lists the common errors, but still could not find it.  A quick Google search however led me to [this](http://randomtech.blogspot.com/2004/11/latex-error-missing-inserted.html) short blogpost, which explains that this is an error generated when the math mode is active, or there is an unescaped underscore.  The latter was the case for my file, and escaping it fixed the error in a jiffy!

Blogged for future reference for self.

 [1]: http://en.wikibooks.org/wiki/LaTeX/Errors_and_Warnings
