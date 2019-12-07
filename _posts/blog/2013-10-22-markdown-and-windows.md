---
title: Markdown and Windows
author: Ninad
layout: post
permalink: /blog/2013/10/markdown-and-windows/
categories:
  - Blog
  - Uncategorized
tags:
  - documents
  - editing
  - markdown
  - markdownpad
  - sublime text
  - windows
---
Creating documents. Anyone who has ever taken up a salaried job knows that this is one of the most boring tasks ever. And, there have been way too many attempts to solve this problem. The IT world is filled with tools to ease this task. From the humble text files to cumbersome MS Word documents, there is a document format for every part of the spectrum.

My ideal document would be written with LaTeX, and shared as a PDF to preserve it's beautiful typography. However, creating a LaTeX document is not a job for the faint hearted. For some kinds of documents, it just is not worth the effort to make a LaTeX file, figure out how to generate tables or graphs and then coax LaTeX into giving you the perfect file.

HTML is another equally portable document format. But, to have a beautiful document again takes some effort. Thankfully, pseudo document formats like Markdown exist to make our life easier. Markdown, or MD, is simple enough to be edited in a generic text editor. Most of the MD parsers/converters also have sane defaults when it comes to typography and styling. Thus, it doesn't take a lot of effort to convert a raw MD file into something that can be easily presented to office management.

If you are in a *nix environment, getting MD to HTML converters is a walk in the park. Windows, on the other hand, is a messy jungle that someone like me hates to enter. But, enter I must, if I am to survive in the above mentioned salaried job. I searched far and wide, and I found two good offline MD to HTML converters.

### MarkdownPad

[https://markdownpad.com/](https://markdownpad.com/ "MarkdownPad")

Written by Evan Wondrasek, this is the best offline tool you can use to write Markdown documents on Windows. I used this for almost a year and a half, and it has developed into a nice, simple, clean editor. With live preview, export to HTML, export to PDF, intuitive keyboard shortcuts and a good set of styles, most users will be extremely happy. With version 2, the author has added some paid only features, and if your life depends on MD, the license cost is well worth it.

For a long time, MarkdownPad v1 fulfilled all my requirements. But then, I decided to evaluate SublimeText. And, I fell in love with ST2. So, the hunt began for a plugin that would work fine with ST2.

### Sublime Markdown Build

[https://github.com/erinata/SublimeMarkdownBuild](https://github.com/erinata/SublimeMarkdownBuild "SublimeMarkdownBuild on Github")

There are a lot of Sublime Text plugins available, to convert MD to HTML. However, they rely on your system having Python, or the markdown.py script being installed on your system. After some searching, I found Sublime Markdown Build, which uses the Python bundled in SublimeText. And, it works perfectly across Windows (office box) and Linux (home box). So, it fit my bill perfectly.

Now, to save up for the slightly steep license costs for ST.
