---
title: $(document).ready fails on Internet Explorer 6
author: Ninad
layout: post
permalink: /blog/2009/08/document-ready-fails-on-internet-explorer-6/
categories:
  - Blog
  - PHP/jQuery
tags:
  - cross browser compatibility
  - document.ready
  - internet explorer
  - javascript
  - jQuery
---
I have been interning at a company for the past few weeks, where I worked on jQuery. It's a Javascript framework, and one of the primary reasons for using it was to not to worry about browser incompatibility issues. I happily coded away, testing my code in Firefox, Opera and Chrome as I went along. Internet Explorer compatibility was a very important issue for us, as our target audience had a large set of users who would still be using sucky IE6, and some more would be using IE7. But, compliance with IE was something we all took up very late into the project.

Two days back, we opened up the site in Internet Explorer, and to our horror, jQuery absolutely refused to work, leaving the pages in an almost unusable state. Being the great product that it is, Microsoft had not provided any sort of an error console, and any amount of coaxing IE6 would do no good. We ran the jQuery test suite, and it gave a perfect score, leaving us absolutely clueless. So, out of desperation, we tried a simple trick, and put in an alert() call just inside the $(document).ready() function. To our dismay, we did not see an alert pop up, no matter how many times we refreshed the page.

Googling gave us a very cryptic solution. A couple of forum and blog posts claimed, that putting all the jQuery code at the end of the bottom of the HTML page, just above the body close tag, made the code work. We tried it out, and this voodo fix seemed to work. This means, that both Internet Explorer 6 and 7 do not fire the 'ready' event at all. By putting all the jQuery code at the end of the HTML body, we ensure that all the DOM elements to which jQuery queues actions, are loaded. And then, we just put the jQuery code without putting it in the $(document).ready() anonymous function.

Hope this helps someone, and save him/her a lot of frustration. :smile:
