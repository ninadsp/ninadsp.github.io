---
title: BCB Twitter Streaming is up on Github
author: Ninad
layout: post
permalink: /blog/2013/05/bcb-twitter-streaming-is-up-on-github/
categories:
  - Blog
  - Bangalore
tags:
  - bangalore
  - barcamp
  - javascript
  - node.js
  - twitter
---
TL;DR: <https://github.com/ninadsp/bcb-twitter-streaming>

[<img class="aligncenter size-medium wp-image-394" alt="Barcamp Bangalore 11 Schedule" src="{{ site.baseurl }}/images/2013/05/IMG_9345-300x200.jpg" width="300" height="200" />][1]

 [Barcamps](http://en.wikipedia.org/wiki/Barcamp "Barcamp on Wikipedia") have traditionally created their schedules with Post-it notes and chart paper. This is a very enticing idea, and is extremely simple to implement. However, this has a few logistical implications. [Barcamp Bangalore](http://barcampbangalore.org "Barcamp Bangalore") had been struggling with the following:

  * The schedule is available at only one location. If the venue is considerably large, or involves a lot of walking around, then it's tiring for all attendees.
  * When the schedule is being created in the morning, there is way too much crowding around the board. Some speakers even missed out on putting their sessions because they couldn't get to the board on time.
  * Once the schedule was created, it was often uploaded to Twitter, or other similar media and then shared lazily among the crowd. As the picture above shows, it wasn't always the complete schedule.
  * If the schedule changed, or someone decided to host an impromptu/Birds of a Feather session, there was no easy way to announce it.
  * A fair number of attendees were unhappy that sessions on the same/similar topics happened in parallel. People missed out on sessions that interested them.

This topic came up in the BCB 11 feedback session, and me and Aman Manglik put in our two cents with everyone else. As with most other events, we left it at that, and went back home. BCB12 planning started, and we decided to go and meet the people behind the scenes (If you don't already know them, they're pretty cool fellows. Amit Khare a.k.a. Daaku, Sathya, Saurabh Minni, Mixdev a.k.a. Arun Vijayan and a few more). We brainstormed (*a lot!*), and finally decided to move the whole scheduling from the humble chart paper to the mighty web. Everyone in the team had their own tasks, so me and Aman decided to pick this up and give it a shot. We finalised our feature set to:

  * Pick up session information from the Barcamp site. This information would be used as an indicator (actually, the sole indicator) while generating a schedule.
  * Mark the first N (36) speakers and their sessions who turn up for registration.
  * Try to schedule all sessions in such a way that there would be minimum clashes for all the attendees involved.
  * Let us manually modify the schedule in extreme cases, or if speakers agree on a mutual swap.
  * Show this schedule on multiple screens/projectors at the venue. The page might also be used by attendees and accessed from their laptops/phones.
  * Announce impromptu sessions as well as any other relevant information for the event.
  * BCB11 had a screen (or two) showing tweets about the event. We had to do something about this too.

I took up the front-end, Aman took up the back-end. The result of this was a bare bones [schedule generator](https://github.com/amanmanglik/BCB-Platform) written by Aman, which fed this information to Saurabh's [Barcamp Bangalore Android App](https://github.com/the100rabh/Barcamp-Bangalore-Android-App) as well as my schedule display. I chose to use node.js and hacked together a set of pages which displayed the schedule, and the announcements and twitter updates on another page. The result:

<img class="size-medium wp-image-395 alignnone" style="margin-left: 20px; margin-right: 20px;" alt="Schedule page" src="{{ site.baseurl }}/images/2013/05/IMG_9769-300x200.jpg" width="300" height="200" />[<img class="size-medium wp-image-396 alignnone" style="margin-left: 20px; margin-right: 20px;" alt="Twitter updates and announcements" src="{{ site.baseurl }}/images/2013/05/IMG_9814-300x200.jpg" width="300" height="200" />][2]

The poor thing broke right when it was most needed, on BCB12's morning, right after the schedule was generated. I had to restart the node.js server to get it back up on it's feet, all thanks to me missing out an edge case while using arrays :/. Thankfully, the server did not stutter later, and everything worked fine for the rest of the day.

With BCB13, I had some more time to work on the code. By this time, I had a better understanding of node.js as well as a few other concepts. I almost completely re-wrote the server side code and removed most of the delays caused by reading and writing of files (yes, I store the schedule and announcements locally in a JSON). I also had to pull out the underlying library and replace it with another one compatible with Twitter's API v 1.1. The date of deprecation of the 1.0 API was dangerously close to BCB13's date and I did not want to take any risks. I spent some time adding support for media entities, added handlebars.js for templating, let moment.js do all the heavy lifting for time and some more fine tuning. The schedule page did not receive as much attention, as it worked fine. Express.js, socket.io, jmpress.js and jQuery still remain a part of the project, and I may keep it that way for the foreseeable future.

My current TODO list for this project includes the following ideas, in no particular order:

  * Refactor and modularise the code. As of now, my entire server side code resides in a single file. I would prefer to have the entire code split up into node modules so that it becomes a little more manageable.
  * As of now, the schedule page is hard-wired to show an event with 6 sessions/rooms and 6 time slots and some additional slots for introduction, feedback, lunch and Techlash. In it's current state, it isn't very flexible and adaptable. If anyone else has to use it, s/he needs to make a lot of changes. I would prefer that this be based on some parameters in the configuration file.
  * The usability on mobile devices (phones and tablets) is pathetic. The schedule page has a fixed width and height (optimised for the projector resolution available). This has to change and it should be easily viewable on smaller screens without a headache.
  * This one is pretty obvious if you look through the code. I have used pretty basic security in securing the admin pages. I still am learning how authentication and node.js fit together.
  * As of now, all error logging happens directly to the node.js server's console (stdout to be specific). Worked fine for me, but will not work for everyone. Log files are a must.
  * Just like the schedule page is hard-wired, all the branding (CSS and images) is very BCB13 specific. Not a very good idea if I'm uploading the code to Github, right?
  * Twitter has some pretty stringent UI guidelines as to how tweets should be displayed. Considering that I was just displaying tweets, and not letting any user interact with them, I did not follow the guidelines to the tee. I would be very unhappy if Twitter decides to shut down my screens in the middle of a future Barcamp just because of this reason.

Time for bouquets and brickbats. If you attended either of BCB12 or 13, and saw these screens, tell us what you think about them please?

 [1]: {{ site.baseurl }}/images/2013/05/IMG_9345.jpg
 [2]: {{ site.baseurl }}/images/2013/05/IMG_9814.jpg
