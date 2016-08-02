---
author: Jiangtang Hu
title: 'An Analytical Valley: Big Data and Data Scientists (and SAS Programmers)'
excerpt:
layout: post
category:
  - Database
  - Industry Review
  - SAS
tags:
  - Big Data
  - data mining
  - SAS
  - SQL
post_format: [ ]
---
[![hadoop][2]][2]

[Tom Davenport][2] reported an observation that [Silicon Valley is becoming more analytical][3] since companies in the Valley such as Google, Facebook, eBay, LinkedLn all have strong presences in analytics. Besides such predominant companies, I’d also like to add Yahoo to the list although Yahoo is no longer in its peak. Yahoo is the largest sponsor and contributor of [Hadoop][4], an open source framework for distributed processing of so called “big data”. When taking a look at the outstanding [Facebook data team][5] or [LinkedIn data team][6], we can see that Hadoop is also one of the most overwhelmingly successful technical factors. Such Valley companies themselves are the huge consumers of big data and have strong incentives to develop analytical solutions beyond their high technology product pipelines.

Analytical staffs in LinkedLn also helps a lot to promote the widely usage of the term “data scientist”. They identify themselves as data scientists and that’s really cool. Now more and more statisticians are also very glad to accept this brand new title. According to a [survey in JSM][7] (2011, Miami), more than 85% (164) statisticians there considered themselves “data scientists”. 

McKinsey also released a report this May [on big data][8] and the huge gap of qualified analytical talents. You know when a management consulting firm begins to talk something technical, it is no longer a fashion to follow the discussion of the concept. To embrace the challenge of big data, one or the team needs multidiscipline background—basically speaking, computer science and statistics (and data mining or machine learning is just an interdisciplinary subject of them). Here is an ambitious list on “How do I become a data scientist”:

> <http://www.quora.com/Educational-Resources/How-do-I-become-a-data-scientist>

For these learning plans, just feel the meaning and don’t take it too seriously. Check yourself and set up your own priority. 

### Notes for SAS Programmers

For SAS programmers, I read an exciting post besides High Performance Computing that [SAS will also play with Hadoop][9] by introducing some functionality in SAS/Access and SAS Data Integration Studio.

For SAS programmers with no IT background, it is not a good idea to jump into algorithms and data structures and other hard core computer courses immediately. Instead I recommend to take the full advantages of SAS language and system itself to dive into computer world gradually:

> 1. Learn and practice and practice [SAS Proc SQL][10] which is compliant with the [SQL-92][11] standard. SQL is the common language in database world and SAS Proc SQL can help you switch smoothly to Oracle SQL, Teradata SQL, MySql SQL and other SQL implementations although there are some non-critical [differences][12] in details.
> 
> 2. Dig into the operating system specific documentation of SAS, for example in SAS 9.3,  *[SAS 9.3 Companion for Windows][13]* or *[SAS 9.3 Companion for UNIX Environments][14]* or others depending the OS you are working on. They are the critical important documentations but unfortunately often missed in SAS programmers’  reading list. 
> 
> Such docs will help SAS programmers to deal with the machines and expose to the wide computer world in a way that a SAS programmer can understand. You can’t expect to be an expert on computer via such docs, but at least you can communicate fluently with internal IT staff. 
> 
> 3. Then you get all the confidences to play with computer and can switch to any other topics interested in [the list above][15]!

 []: http://dl.dropbox.com/u/69732603/hadoop.jpg
 [2]: http://blogs.sas.com/content/sascom/author/tomdavenport
 [3]: http://blogs.sas.com/content/sascom/2011/09/13/is-silicone-valley-becoming-more-analytical/
 [4]: http://hadoop.apache.org/
 [5]: www.facebook.com/data
 [6]: http://sna-projects.com/sna/
 [7]: http://blog.revolutionanalytics.com/2011/08/statisticians-at-jsm-consider-themselves-data-scientists.html
 [8]: http://www.mckinsey.com/mgi/publications/big_data/pdfs/MGI_big_data_full_report.pdf
 [9]: http://blogs.sas.com/content/datamanagement/2011/08/29/sas-hadoop-and-big-data
 [10]: http://support.sas.com/documentation/cdl/en/sqlproc/63043/HTML/default/viewer.htm#titlepage.htm
 [11]: http://en.wikipedia.org/wiki/SQL-92
 [12]: http://www.jiangtanghu.com/blog/2009/12/04/work-with-oracle-a-quick-sheet-for-sas-programmers-2/
 [13]: http://support.sas.com/documentation/cdl/en/hostwin/63047/HTML/default/viewer.htm#titlepage.htm
 [14]: http://support.sas.com/documentation/cdl/en/hostunx/63053/HTML/default/viewer.htm#titlepage.htm
 [15]: http://www.quora.com/Educational-Resources/How-do-I-become-a-data-scientist