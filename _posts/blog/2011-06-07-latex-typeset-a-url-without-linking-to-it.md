---
title: 'LaTeX - Typeset a URL without linking to it'
author: Ninad
layout: post
permalink: /blog/2011/06/latex-typeset-a-url-without-linking-to-it/
categories:
  - Blog
  - Uncategorized
tags:
  - how-to
  - LaTeX
  - note to self
  - typesetting
---
While creating a report in LaTeX, I wanted to typeset the following link. but not actually create a link in the generated PDF, as it is an example, and will not work:

`http://www.example.com/index.php?type=bakery&#038;cost=1000&#038;city=123`

Using \url{} was out of question as it does not provide the flexibility to set a title to the link.  When I tried using \href{} with an empty title, it gave a nice little error and the latex file did not compile.  Also, I did not want to take the effort of using the typewriter font face and manually typesetting the URL so that it correctly split at the end of the line.  The Wikibook did not provide any tricks, and a quick search on the TeX StackExchange did not give any useful results.

So, I searched for the manual for the \hyperref package.  There, I found that I could use the \nolinkurl{} command to do exactly what I wanted.  So, my problem was solved by putting the following snippet in my file.

`\nolinkurl{http://www.example.com/index.php?type=bakery&#038;cost=1000&#038;city=123}`
