---
title: A Shell Quirk
author: Ninad
layout: post
permalink: /blog/2009/02/a-shell-quirk/
categories:
  - Blog
  - Uncategorized
---
Here's a quirk that I noticed, while coding today.  Was writing a function to test if a directory exists, and to make the directory doesn't exist.  Shell offers the **test** command, used with an **if** statement, to solve this.  Here's what I wrote:  
{% gist 6098996 shell_quirk_1.sh %}
**[** *expression* **]** is a synonym for **[ test** *expression* **]**.  Interestingly, this peice of code did not work.  So, I had to make do with this:  
{% gist 6098996 shell_quirk_2.sh %}
Could someone tell me if it's a syntax/logic error that I have made?  Or is it a problem with the BaSH test command?
