---
title: AJAXify the phpMyAdmin Interface
author: Ninad
layout: post
permalink: /blog/2010/04/pma-gsoc-proposal/
categories:
  - Blog
  - phpMyAdmin
tags:
  - gsoc
  - gsoc2010
  - jQuery
  - PHP
  - phpMyAdmin
  - pma-gsoc
---
This is my proposal for the *Google Summer of Code 2010* at *phpMyAdmin*, and it has been selected among the six project proposals to participate in GSoC 2010.  The mentor for the project is [Marc Delisle][1] (lem9).  During the project, the actual implementation of this project will most probably change, and things may not go exactly as per this plan.  But, I will do my best to stick to this plan, and incorporate all the feedback that the community will provide.  The time that I've spent till now in the community, while participating in the mailing lists, has been good, and I am looking forward to a good summer, filled with lots of learning and also some good coding.  :smile:

### **Synopsis :**

The current interface of phpMyAdmin makes extensive use of frames, to reduce the bandwidth consumption and hence, improve speeds by just downloading the necessary content.  However, the use of frames is not enough to improve speeds on really slow internet connections or slow host servers (I've faced that issue often, as the internet connection provided at my college is not very fast :worried: ).  Today, major browsers support the AJAX functionality and many users have come to expect it from a good web application on account of it's usability aspect and the performance enhancement it provides on slow connections.

This project aims to modify parts of phpMyAdmin's interface so that browsers with JavaScript enabled can effectively use AJAX.  Due to the vastness of this task, during the Google Summer of Code, I plan to complete the necessary ground work of creating generic functions, example PHP and jQuery code and implement the AJAX functionality in some pages of phpMyAdmin.  Wherever necessary, jQueryUI components and jQuery plugins will be used to simplify the tasks while not compromising on the robustness of the application.

### Benefits to the users (like me and you) :

  * A fresher, updated interface.  (Don't we all love to have some bling?)
  * Reduced traffic between the web server and the client and hence, faster responses by the application.  (Finally, work will be done faster, and I'll spend lesser time for the page to load and I can sleep earlier!)
  * Ease of use increases as features like Inline Editing of SQL queries and Data stored in the Database are added and existing features like Managing User Privileges, Managing Databases and other such actions are modified for AJAX.  (For the point and click fellas :smile: )
  * Also, the use of jQueryUI components increases the user friendliness of the application as compared to the use of plain JavaScript alerts.  (Again, some more bling)
  * Improved reliability on slow connections.  (Lesser chances that I will now loose the last edit I made, due to a network failure.  I can wait for the network to improve, and resubmit that change by clicking the 'Save' button again.)
  * For users who need to access the internet through browsers where JavaScript is unavailable, or is disabled due to security concerns, the old interface will still work without any changes in behaviour.

### Project Details :

phpMyAdmin, written in PHP, has been around since 1998 and has a strong library of functions, which simplify a lot of the tasks and free up the programmer from the mundane tasks.  Thus, there are a lot of functions that prepare and sanitize the user input and make it easy to handle large output sets from the database.  During this project for adding AJAX functionality to the user interface, the behaviour of these functions will be modified.  Thus, they will present only the necessary output during an AJAX request, but will still present the complete output when a normal page request is made.  jQuery scripts will be created for the different pages, which will attach actions to different events and DOM elements, confirm some of the actions from the user, perform the AJAX requests, and replace the data being displayed on the page when output is provided by the web server.

For an example, consider the job of Adding a New User on the Database privileges page.  The user (Admin) wishes to add a new user (Client1) for a database, and grant certain privileges.

  * Admin clicks on the link at the bottom of the page 'Add a new User'.  jQuery prevents the default action, of loading a new page by making a request, and instead opens up a jQueryUI dialog and disables other actions on the page using the blockUI plugin or something similar.
  * It loads a list of available databases from the server and lets Admin select different databases where Client1 will be granted privileges. 
      * In case Admin does not have the Grant Privilege (that should not happen to the Server Administrator :smile: ), the dialog will display an error and stop the process from continuing.
  * Provided that our Admin has the necessary rights, s/he now selects the database(s), the required set of privileges and enters a username and a password (or generates a random password).
  * Next, the Admin submits the details, and jQuery takes over the request again.  It posts the data to the server, and waits for phpMyAdmin to process the request.
  * Once phpMyAdmin has completed it's job on the server, it sends a response (success/failure) to the browser and jQuery reads it.  It displays the result to the user and closes the dialog. Job Done! :smile:
  * It updates the table and appends the newly created user.

In case Admin is on a really old browser, or has access to only a text based browser without JavaScript, the interface would be the current one, as jQuery would not have kicked in and attached all the actions to the different HTML elements on the page.  And in the end, Client1 would have received his database privileges.  
A few tests were carried out, and it shows that even if the initial page load time and bandwidth consumed increases due to the inclusion of JavaScript files, the consecutive page loads are faster and require lesser bandwidth.   [Screen shot 1][2] of Firebug's Net console shows phpMyAdmin being used to view the contents of a table, where the entire frame is reloaded on every page request.   [Screen shot 2][3] shows a patched version of the same snapshot of phpMyAdmin, which makes AJAX requests and retrieves only the necessary sections of the page.  In both the cases, the same table and the same set of rows was viewed.  As can be seen, each request without AJAX consumes 8 kB while the requests with AJAX consumes 6 kB (25% savings).  This difference will be more noticeable for requests where an entire page is loaded in response to a simple action like deleting an entry from the database, when just a 'success/failure' message is sufficient.

### Deliverables :

  1. PHP functions that check for the presence of an AJAX request and accordingly, set some variables in the execution environment of the current script.
  2. Functions that will wrap the output in well formed XML, so that jQuery can correctly parse the response and insert the right content at the right location in the page.
  3. jQuery helper functions/plugins to manipulate major divisions on a phpMyAdmin page, as well as some properties like page title, content in the other (navigation) frame.
  4. Prepare sample PHP and jQuery code using the code developed till now, which can be used to modify an existing action from it's current form to that necessary for an AJAX request.  Will be used as a model to modify other pages/actions by community members.
  5. Actual conversion of some pages/actions to AJAX.

### Project Schedule :

  * **Community Bonding Period** : Understand the codebase better, get used to the project's coding style by bug-fixing. Be a more active participant on the developer and community mailing list.  Get a better hang of jQuery UI.
  * **First week (May 24-30)**: Write deliverables 1 and 2.  Start creating a list of tasks that can be done for deliverable 3, in consultation with the community.
  * **Second & Third week (May 31- June 13)** : Write deliverable 3.
  * **Fourth week (June 14-20)**: Write deliverable 4.  Convert the Privileges page (*server_privileges.php*) to AJAX as the sample.
  * **Fifth & Sixth week (June 21- July 4)** : Convert the SQL pages (*db_sql.php* and *tbl_sql.php*) to AJAX &#8211; the pages where user enters an SQL query and the output of the query is returned as a table.  Fix the paginate_table patch submitted on the Sourceforge patch tracker to work on all pages, including *db_sql* and *tbl_sql*.
  * **Seventh week (July 5-11)** : Insert page (*tbl_change.php*).
  * **Eighth & Ninth week (July 12-25)** : Inline Editing of data returned from a table.  Will affect *libraries/display\_tbl\_lib.php* and other related files.
  * **Tenth week (July 26-August 1)**: Basic actions like Creating a Database, Table, Changing Passwords and other actions on the Operations page (*db_operations.php *and *tbl_operations.php*).
  * **Eleventh week (August 2-8)** : Test across different browsers and platforms to ensure that the changes work as expected on most platforms.
  * **Twelfth week (August 9-15)**: Suggested Pencils Down date is here!  Check the entire code for crappy and incomplete documentation/comments, improve it.
  * **August 16 **: GSoC 'Pencils down'

For staying in touch with the mentors, I hope to rely primarily on the mailing list as most of the development work for phpMyAdmin happens over there, and not the IRC channels.  As a result, timezone differences will not be a major obstacle and should not cause unnecessary delays in this schedule.

### Time :

  * From beginning of Summer of Code (May 24) to 7th July : ~50 hours a week. (8 hours a day, 6 days a week)
  * From 8th July onwards : 35 hours a week.  (Reason: I have a compulsory 6 month internship as part of my college degree, which starts in the first week of July and cannot be delayed.  However, the first 2-3 weeks (rest of July) are mostly training activities.  Also, I am structuring the project in such a way that I will not have too heavy a work load in August, till GSoC Pencils Down date)

### Bio :

I'm a 21 year old student at Birla Institute of Technology and Science, Pilani (popularly known as BITS, Pilani in India).  My hobbies include Music (mostly listen to music, also play the Tabla and the Harmonium), [Photography][4] (love clicking photos of flowers and live dance/drama performances) and processing them and Astronomy, other than programming and tweaking code.

### Experiences :

Internship with [HelpHub][5], a web start-up that provides a platform for Non-Government (non-profit) Organizations and Corporates to interact.  Implemented OAuth services of Twitter and Google and also implemented services using the Google Calendar and Google Documents APIs.  Also, used jQuery extensively and a little bit of jQueryUI.

Completed Data Processing (an introduction to Oracle SQL) as a structured course and Network Programming (in C) and Object Oriented Programming (through Java) courses as electives and currently studying an Advanced PHP (non-academic) course that focuses on object oriented PHP, the use of frameworks, web services and writing simple web applications with security in picture.

### Open source :

Confirmed a [bug][6] at Launchpad.  Intermittent contributor to the [Ubuntu-India Mailing Lis][7]t.  Assisted in organizing [OSScamp][8], an unconference in the technical festival at my institute.

Was introduced to Open Source two and a half years ago by a friend who uses Ubuntu.  Since then, I have completely switched over to Linux, used and maintained applications like WordPress and Gallery for college activities.  Learnt PHP and Bash scripting on the way.

### phpMyAdmin contributions :

Created a [patch][9] to paginate results of a table query, my first ever code contribution to an Open Source project and phpMyAdmin.

 [1]: http://infomarc.info/ "Marc Delisle's home page"
 [2]: http://ninadpundalik.co.cc/images/without_ajax.png "phpMyAdmin without AJAX" (dead link)
 [3]: http://ninadpundalik.co.cc/images/with_ajax.png "phpMyAdmin with AJAX" (dead link)
 [4]: http://flickr.com/photos/ninadsp "My Flickr Photostream"
 [5]: http://www.helphub.in "HelpHub Homepage"
 [6]: https://bugs.launchpad.net/ubuntu/+source/insserv/+bug/321927 "Bug at Launchpad"
 [7]: https://lists.ubuntu.com/mailman/listinfo/ubuntu-in "Ubuntu India Mailing List page"
 [8]: http://pilani.osscamp.in/ "OSScamp Pilani page"
 [9]: https://sourceforge.net/tracker/?func=detail&aid=2981401&group_id=23067&atid=377410 "Paginate Table Patch at Sourceforge"
