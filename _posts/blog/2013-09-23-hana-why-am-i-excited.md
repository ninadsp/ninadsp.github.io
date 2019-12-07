---
title: 'HANA &#8211; Why am I Excited'
author: Ninad
layout: post
permalink: /blog/2013/09/hana-why-am-i-excited/
categories:
  - Blog
  - SAP
tags:
  - HANA
  - SAP
---
Much has been written (and said) about the speed gains that [main directives](https://twitter.com/ni_nad/status/273652841942491137 "SAP HANA" href="http://saphana.com" target="_blank">SAP HANA</a> will bring to applications, and the resulting changes it'll bring to business processes. I'm excited by the impact it'll have on how our company makes the world run better. But, the thing that caught my imagination is the simplification it is expected to bring to an enterprise developer's (and administrator's) life. Given that this is one of the <a title="Vishal Sikka's principles for SAP Development, paraphrased") for development of SAP products, but not one emphasised enough, I decided to spend some time understanding it.

*Note*: The effects predicted as well as concerns noted are in the context of SAP applications running on top of SAP HANA. Although they will also apply to general applications that will run atop HANA, the historical assumptions I have implicitly included may not apply for them. Opinions are mine, will not reflect what the company says.

#### Changes Proposed:

([source](http://books.google.co.in/books?id=YDB2lf9PZKwC "In-Memory Data Management book by Hasso Plattner and Alexander Zeier"))

  * **Columnar storage**: Databases have been storing data in [columnar format](http://en.wikipedia.org/wiki/Column-oriented_DBMS "Wikipedia on Column oriented DBMS"), instead of row based storage for a few years. That every table is assigned to the columnar engine by default is thus not spectacularly new. But, this choice, combined with those discussed next, have a major impact.
  * **Compression**: Most of the columnar databases have supported [some form of compression](http://en.wikipedia.org/wiki/Columnar_database#Compression "Wikipedia on Compression in Columnar datbabases"), and even some row storage database engines have done so. Again, not new, move on.
  * **No Aggregates**: This is a major design choice for a database that is being designed ground up to support OLTP as well as OLAP workloads in the same instance. Combined with the former two (Columnar storage and Compression), this aims at reducing the database footprint and giving end users results based on live data.
  * **No application level caching**: Combined with the previous three, this is another choice made to provide end users with real time data. However, this is more of a suggestion, and developers are obviously free to choose.
  * **Code push-down to the Database**: Different database vendors have supported different extensions to SQL, supporting some form of code push-down to the database. This was not advocated by SAP for a long time, due to multiple reasons. Chief among them being a choice to support the common subset of features supported by all databases for SAP applications, and not bother too much with the vendor specific features.
  * **An Eclipse based IDE**: This has been around for some time, and the timing just coincided with that of HANA. SAP has now decided to deliver a range of plugins/builds which will do everything, from system administration, to development for a range of SAP products. ([source](https://tools.hana.ondemand.com/ "Eclipse tools by SAP"))

</facts>

#### Effects Predicted:

  1. The number of tables in the system reduces: This is a direct outcome of the choice of not having aggregates. A large number of tables were used for storing intermediate results required by various reports. I see these consequences:
      1.  The complexity of maintenance reduces: If the only table I have to update during a financial transaction is the basic accounting document, and not update multiple ledgers, my code is a lot simpler and hence, less prone to errors.
      2.  The steepness of the learning curve for a new developer reduces
  2. There is just 1 true source of information as we now have the same database serving OLTP and OLAP application systems.
      1. It ends the era of byte pushing across multiple systems in the same landscape to a large extent. We no longer have to develop, test and monitor costly ETL jobs or run complex replication systems.
      2.  This also reduces the unnecessary redundancy of data that IT landscapes have been forced to deal with for the past few years.
  3. Caching complexity is completely removed from the kernel. The ABAP (Netweaver) Application Servers had complex caching/buffering mechanisms in place to mask the performance impact of the overloaded databases. This should not be necessary any more.
      1. Will this lead to a reduced kernel size? I really hope it does. However, the folks at the kernel teams have been adding a lot of new features recently. Will these two events balance each other out is a question only time can answer.
      2. My experience with web development has proved that caching always leads to weird bugs, which cannot be easily replicated. The standard solution for these bugs is to clear the caches and try again. Not really a bright one, right? If caching is removed or reduced, we shall see lesser such bugs.
  4. The move to Eclipse means that SAP has finally made some peace with the open source community, after struggling with its efforts with MySQL/MaxDB et al. A decent give and take relationship might just have begun, and I hope it can be replicated for other projects like UI5
      1. Moving to Open Source platforms reduces the learning curve for developers who come from a non-SAP background.
      2. However, the learning curve might increase for administrators, who are used to product specific tools

#### Possible Concerns:

All is not shiny and bright though.

  * With code push-down, a lot of the calculations are moved to the database. Version tracking of all the stored procedures and consistency of data structures with the application logic will be a challenge. This could lead to a tight coupling of code and data, especially when combined with the push to improve the application server (XS engine) in HANA.
  * Concentrating all the data in a single system/cluster makes the availability of this system all the more critical. As far as I have understood, the high availability and disaster recovery concepts in HANA are a little different from what most system administrators are traditionally used to. Properly understanding and planning the setup is crucial.
  * If the communication around the versions of the database, the features and APIs in the XS engine and other relevant things is not clear, I fear a [dependency hell](http://en.wikipedia.org/wiki/Dependency_hell "Wikipedia on Dependency Hell"). Combined with the tight coupling of data and code mentioned above, this might just lead to data corruption if the developers and system administrators are not careful enough.
  * As of today, there is a tight coupling to the hardware and Operating Systems that are certified to run HANA. If the company plans to support HANA on anything other than large enterprise servers, I am guessing it will be a painful task. I'm looking at commodity servers of the kinds used by Google/Facebook, or boxes made by combining graphics processors with [CUDA](http://en.wikipedia.org/wiki/CUDA "Wikipedia on CUDA"). There are very good reasons for why large enterprise servers were chosen, but, I would still like to note this concern.
  * <del>Eclipse is still a container for ABAP, mostly. If the life of a developer has to be made really easy, it must not remain just a shell.</del> *Edit: This opinion had been based on a short demo I saw during Bangalore TechEd 2012. I downloaded the latest edition of ABAP DevTools today, and in the few minutes I played with it, I can safely say that things have changed a lot. I'll leave this for another post.*
  * Release upgrades are a major lifecycle maintenance task for most of SAP software. As far as I understand, there has not been a lot of optimization done in this area from both, the database and the tooling side. As this topic is very relevant for my day to day work, I'm putting it out as a concern. I have no solutions yet on this topic though.

To conclude, I would like to emphasize that choosing SAP HANA is not going to be a magical silver bullet that will resolve all the problems we face in the enterprise software world. It solves some of them really well, and brings some of it's own problems to the table. As a developer or system administrator who will use SAP HANA, it is our job to properly understand the software, and make the correct choices. At the same time, there are some kinks that need to be ironed out in HANA. For the past 2 years, SAP has put all of its resources in improving the database and making it a viable platform for enterprise grade software. I look forward to the changes in the industry (not just the IT industry) and how this will impact the world.
