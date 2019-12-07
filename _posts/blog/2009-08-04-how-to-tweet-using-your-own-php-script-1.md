---
title: 'How to Tweet using your own PHP script &#8211; 1'
author: Ninad
layout: post
permalink: /blog/2009/08/how-to-tweet-using-your-own-php-script-1/
categories:
  - Blog
  - Hobbies
  - PHP/jQuery
tags:
  - ACAD
  - how-to
  - jQuery
  - json
  - PHP
  - tweet
  - twitter
---
Twitter is the darling for many folks on the internet these days.  The sheer simplicity of Twitter is what makes it so endearing.  This simplicity is observed not only in it's UI and UX, but also in it's brilliant API.  With one of the most [well documented APIs](http://apiwiki.twitter.com/ "Twitter API Wiki") I have seen to date, for a web service, it is pretty easy to fiddle with Twitter.

In this 2 part post, we will have a look at a small PHP script which posts tweets for a given user.  I have used [<strong>jQuery</strong>](http://jquery.com "Jquery Home") along with the **cURL library** to post the tweets.  This is just an example, and hence has almost no validation.  Ensure that all the requirements given on the Twitter API wiki are met, when writing your own code.

The **HTML code** for this, which i'll keep in the **twitter.html** file, is:  
{% gist 6098996 twitter.html %}

This is pretty simple HTML code. We have a form that takes in the users Twitter *username*, *password*, and the *text* for the tweet. The textarea has a maximum length of 140 characters, which should also be validated by the JavaScript and PHP. Twitter expects the clients to validate this.

The **tweet.js** file contains the following **jQuery** code:
{% gist 6098996 tweet.js %}

As you can clearly see, this is one of the two main parts of our how to. It makes an *AJAX request* to our twitter_ajax.php script, with the username, password and text as **POST** parameters. On a successful response from our AJAX script, it *constructs the HTML* to be inserted into the 'response' div, and then *inserts* it into that.

In the next post, we'll have a look at the PHP back-end (*twitter_ajax.php*) of this how-to, where cURL will do all the hard work of actually posting our tweet to Twitter.
