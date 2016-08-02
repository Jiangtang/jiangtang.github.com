---
id: 381
title: 'Map and Reduce in MapReduce: a SAS Illustration'
date: 2011-10-04T21:31:18+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/10/04/map-and-reduce-in-mapreduce-a-sas-illustration/
permalink: /2011/10/04/map-and-reduce-in-mapreduce-a-sas-illustration/
categories:
  - data mining
  - Database
  - SAS
tags:
  - Array
  - Hadoop
  - Lisp
  - List
  - MapReduce
  - Python
  - SAS
---
In <a href="http://www.jiangtanghu.com/blog/2011/09/14/analytical-valley/" target="_blank">last post</a>, I mentioned [Hadoop](http://hadoop.apache.org/), the open source implementation of Google’s <a href="http://en.wikipedia.org/wiki/Mapreduce" target="_blank">MapReduce</a> for parallelized processing of big data. In this long National Holiday, I read the original Google paper, _<a href="http://static.googleusercontent.com/external_content/untrusted_dlcp/labs.google.com/en//papers/mapreduce-osdi04.pdf" target="_blank">MapReduce: Simplified Data Processing on Large Clusters</a>_ by Jeffrey Dean and Sanjay Ghemawat and got that the terminologies of “map” and “reduce” were basically borrowed from Lisp, an old functional language that I even didn’t play “hello world” with. For Python users, the idea of Map and Reduce is also very straightforward because the workhorse data structure in Python is just the list, a sequence of values that you can just imagine that they are the nodes(clusters, chunk servers, …) in a distributed system. 

MapReduce is a programming framework and really language independent, so SAS users can also get the basic idea from their daily programming practices and here is just a simple illustration using data step array (not array in Proc FCMP or matrix in IML). Data step array in SAS is fundamentally not a data structure but a convenient way of processing group of variables, but it can also be used to play some list operations like in Python and other rich data structure supporting languages(an editable version can be founded in <a href="http://jiangtanghu.com/docs/en/MapReduce.sas" target="_blank">here</a>):

[<img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; margin-left: 0px; border-left-width: 0px; margin-right: 0px" title="MapReduce" border="0" alt="MapReduce" align="left" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/10/MapReduce_thumb.png" width="506" height="535" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/10/MapReduce.png)

Follow code above, the programming task is to capitalize a string “Hadoop” (Line 2) and the “master” method is just to capitalize the string in buddle(Line 8): just use a master machine to processing the data.

Then we introduce the idea of “big data” that the string is too huge to one master machine, so “master method” failed. Now we distribute the task to thousands of low cost machines (workers, slaves, chunk servers,. . . in this case, the one dimensional array with size of 6, see Line 11), each machine produces parts of the job (each array element only capitalizes a single letter in sequence, see Line 12-14). Such distributing operation is called “<font color="#ff0000">map</font>”. In a MapReduce system, a master machine is also needed to assign the maps and reduce.

How about “<font color="#ff0000">reduce</font>”?&#160; A “reduce” operation is also called “fold”—for example, in Line 17, the operation to combine all the separately values into a single value: combine results from multiple worker machines.