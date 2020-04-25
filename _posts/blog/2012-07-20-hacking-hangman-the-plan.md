---
title: 'Hacking Hangman - The plan'
author: Ninad
layout: post
permalink: /blog/2012/07/hacking-hangman-the-plan/
categories:
  - Blog
  - Uncategorized
tags:
  - hacking
  - hangman
  - mongodb
  - python
  - shell
---
[Hangman](http://en.wikipedia.org/wiki/Hangman_(game)), the game, has always put me in a quandary. Me and my friends have always played the movie titles variant of the game. I can never accept the fact that I would start my guesses of the alphabets randomly. So, the other day, I cooked up a lean, mean plan to fight the game.

I'm going to take IMDb's amazing [dump](http://www.imdb.com/interfaces) of data, write a script that will analyse the movies, and do a simple character count. The alphabet with the largest count, wins. Simple, isn't it?

Future plans involve using some more data from IMDb, and running the script against the top X number of movies, make a Bollywood edition, and include the movie's ratings in the recipe.

Follow the hangman hacking on [github](https://github.com/ninadsp/hangman-hacking)
