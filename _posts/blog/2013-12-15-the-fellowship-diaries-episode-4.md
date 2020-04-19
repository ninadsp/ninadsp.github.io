---
title: 'The Fellowship Diaries - Episode 4'
author: Ninad
layout: post
permalink: /blog/2013/12/the-fellowship-diaries-episode-4/
categories:
  - Blog
  - SAP
tags:
  - fellowship
  - HANA
  - hasso plattner institute
  - SAP
  - SAP Innovation Center
---
If you have been following the posts from [the Fellowship Diaries][1], you would remember the primary purpose for this entire circus was to learn. With about 2 weeks remaining for the fellowship to end, it makes sense to take stock of the things I have learnt in the past few months.

# Toolkit Expansion

During the first half of the fellowship, we spent quite some time collecting ideas, reading about everything under the sun and brainstorming it. In the second half, I have been helping out with some tooling for a benchmark. Both the phases have had me playing at the systems level for the first time, so my toolkit has had a few new tools added:

  * **gdb**: I've done a bit of C programming in college for assignments. But, my programming experience was too limited at that point of time to try using a debugger and detect what the error was. Also, the programs were simple enough that adding a print statement and recompiling it was simple and dirt cheap. However, during the fellowship, we had to study the query execution path in HANA, and find out what data points are available for us to work. I rolled up my sleeves, read up Beej's excellent [introduction to GDB](http://beej.us/guide/bggdb/ "Beej's Guide to GDB"), and poked around inside the working machine.
  * **C++**: Along with debugging the query execution, came the need to read the relevant source code. HANA is mostly written in C++, and I slowly started to grok the syntax. When I have time some day, I'd like to spend more time and learn C++ from the ground up.
  * **Python**: The benchmark was originally available as a Python script. We decided to continue building on top of it and make some tooling to test different ideas and their performance against HANA's normal behaviour. With this script/project, I finally got something tangible to do in Python, and I learnt how to use it. I'd spent a few weeks learning the syntax a couple of years ago, but the lack of a project meant I did not really learn it back then.
  * **Antlr**: We wanted to analyse the benchmark, and figure out what data the SQL queries were accessing. The most feasible option at that point of time was to parse the SQL queries ourselves, and then carry out our analysis. One of the colleagues at the ICP had already implemented a basic SQL grammar and used [Antlr](http://www.antlr3.org "Antlr 3") to generate lexers and parsers. I used the grammar, improved it to fit our requirements, and used the generated classes in the Python script.
  * **HANA**: At the risk of being called Captain Obvious, I learnt quite a bit about the different components of the database. I finally got an opportunity to translate all the theoretical learning from the openHPI course to the real world implementation. I also spent quite some time understanding statistics that the server stores, and I think I now understand some of them.

The next post in the series will most probably be the last one. I plan to write it after returning to Bangalore, and sleeping over a few drafts.

 [1]: http://ninad.pundaliks.in/blog/the-fellowship-diaries/ "The Fellowship Diaries"
