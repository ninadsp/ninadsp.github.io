---
title: 'ACAD - bash tips'
author: Ninad
layout: post
permalink: /blog/2008/09/acad-bash-tips/
categories:
  - Blog
  - Linux/Ubuntu
tags:
  - ACAD
  - Shell Script
---
We get back to the most powerful tool on Linux, and my favourite, the Shell. Specifically, we will have a look at some of the features that the Bourne Again Shell (bash) has to offer for command line users. Some of these features are also supported by other shells. A lot of these tricks are common place for power users, and I hope that they will be very useful for newer users.

* bash supports **command completion**. What this means is that you almost never have to type more than 4 characters to get to the right command. Type in the first 2 characters of your command and press the '*tab*' key twice. The shell will list all the possible completions of your command. Type in the next couple of characters till the number of possibilities become one, and press '*tab*' once, the shell will happily complete the command. This feature is also useful when typing out long filenames. Follow the same procedure to get to the correct file.
* Output redirection is another fantastic feature offered by all the shells. We just have to type in a chain of commands separated by a `|` (a *pipe*, found along with the `\`), to form a '*pipeline*'. Lets have a look at an example: {% gist 6098996 bash_tips_1.sh %}
This command will print UbuntuCodeofConduct-1.0.1.txt, send it's output to `grep`, which will print the lines containing 'Ubuntu', which are then piped to `wc` which will count the number of lines in it as the option **l** is specified to it.
* Pipelines will simply run the commands given. However, if you wish that the commands will run with a given condition, then we can use *lists*. Here, the commands to be run are separated by **;** , **&#038;** , **&#038;&#038;** and `||`. The function of &#038;&#038; and `||` is the same as that in C language, i.e., AND and OR logic respectively.
* **Command Substitution** is another useful tool. Here, you substitute the output of a command in the middle of another command. It is done by enclosing the command in `` ` `` (a backtick). Note, this is not a single quote. It is the character found on the same key as the '~' (tilde). An example that I have seen often is: `` $ apt-get install linux-headers-`uname -r` `` The output of `uname -r` will be substituted to get the proper package name, linux-headers-2.6.24.16-generic for my system.
* One more useful tool in the bash arsenal is **command aliases**. To put in simple, but inaccurate words, we are creating keyboard shortcuts for commands that we commonly use on the shell. Custom bash aliases are defined in the `~/.bash_aliases` file while default settings are in the `~/.bashrc` file (atleast in Ubuntu). Some of them in my file are: {% gist 6098996 bash_tips_2.sh %}

Hope that after reading this post, you are a slightly better shell user than before. If you find anything wrong, in any of my posts before, or after this, please feel free to drop a comment and correct me. I too am a noob as many of you are. :smile:
