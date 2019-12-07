---
title: How to tweet using your own PHP script
author: Ninad
layout: post
permalink: /blog/2009/08/how-to-tweet-using-your-own-php-script-2/
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
In the last post, we had a look at the HTML and jQuery code which will be used to post tweets from a user to his Twitter profile. Today, we spend some time on the back end, the actual PHP code. As I have mentioned before, this is a sample code, and hence involves very little validation. When writing code for production/personal use, please include necessary validations in it.

The code for the *twitter_ajax.php* file is:  
{% gist 6098996 twitter_ajax.php %}

Here's what this script does:

  * The first if condition checks that the PHP script is being called through an AJAX request. It is a parameter that we have set in the jQuery code.
  * Next up, all the **POST** variables are stored into PHP variables, with the proper names.
  * Now, we construct the authentication string, which is a string containing the username and password, separated by a colon. This is the format that cURL uses, while accessing sites that require [**Basic Authentication**][1]. So, we prepare the string as per it's requirements.
  * After this, we create an array that will hold the data to be posted to Twitter, i.e., the tweet. The key to be used is '**status**', as cURL will later *urlencode* this into a 'key=value' form.
  * Then, we declare all the settings for cURL, which we want to use. To find out about more values that can be used here, visit the PHP Online Documentation for 'curl_setopt'.
  * The important thing to note here, is the **CURLOPT_RETURNTRANSFER** setting, which stores the response in a string, for use later. Also, **CURLOPT_POST** tell cURL that the request is a POST request, and it is to be made to the **CURLOPT_URL** url. **CURLOPT\_SSL\_VERIFYPEER** is set to false to disable SSL verification.
  * Now, it is time to **initiate** the cURL session. Then, we **set the options** for cURL, and **execute** the request. The response is stored in $data, and we **end** the cURL session.
  * The last bit that remains, is sending the data back to our page, which made the AJAX request. We first *set the appropriate headers*, so that jQuery will correctly read the response. And now, we print out the response. I have used a *die()* statement here, but instead, you could use a combination of *echo* and *exit* as well.

As we already know, the jQuery will then process the JSON object, and show the user the posted tweet. To summarize, the steps involved in posting the tweet are:

  1. The user opens the page (twitter.html), and fills up the form with his Twitter credentials and the content of the tweet.
  2. He submits the content, which is now validated by jQuery. If it is satisfied with the validation, it will make an AJAX call to twitter_ajax.php.
  3. The PHP script does server side validation, and then constructs the request. It then executes the request, and prints out the response from the Twitter API endpoint.
  4. The jQuery now reads the output of the PHP script, extracts the relevant details, and inserts them into the response div. In case there is an error, it must notify the user.

And that does it! Do spend some time with the Twitter API. Some links I referred to:

  1. [Twitter API Wiki][2]
  2. [API Page for status/update][3]
  3. [An example of cURL with Twitter][4]

 [1]: http://en.wikipedia.org/wiki/Basic_authentication
 [2]: http://apiwiki.twitter.com/
 [3]: http://apiwiki.twitter.com/Twitter-REST-API-Method%3A-statuses update
 [4]: http://www.sakana.fr/blog/2007/03/18/scripting-twitter-with-curl/
