---
author: Jiangtang Hu
title: 'Map and Reduce in MapReduce: a SAS Illustration'
excerpt:
layout: post
category:
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
post_format: [ ]
---
In [last post][1], I mentioned [Hadoop][2], the open source implementation of Google’s [MapReduce][3] for parallelized processing of big data. In this long National Holiday, I read the original Google paper, *[MapReduce: Simplified Data Processing on Large Clusters][4]* by Jeffrey Dean and Sanjay Ghemawat and got that the terminologies of “map” and “reduce” were basically borrowed from Lisp, an old functional language that I even didn’t play “hello world” with. For Python users, the idea of Map and Reduce is also very straightforward because the workhorse data structure in Python is just the list, a sequence of values that you can just imagine that they are the nodes(clusters, chunk servers, …) in a distributed system. 

MapReduce is a programming framework and really language independent, so SAS users can also get the basic idea from their daily programming practices and here is just a simple illustration using data step array (not array in Proc FCMP or matrix in IML). Data step array in SAS is fundamentally not a data structure but a convenient way of processing group of variables, but it can also be used to play some list operations like in Python and other rich data structure supporting languages(an editable version can be founded in [here][5]):

[![MapReduce][7]][7]

Follow code above, the programming task is to capitalize a string “Hadoop” (Line 2) and the “master” method is just to capitalize the string in buddle(Line 8): just use a master machine to processing the data.

Then we introduce the idea of “big data” that the string is too huge to one master machine, so “master method” failed. Now we distribute the task to thousands of low cost machines (workers, slaves, chunk servers,. . . in this case, the one dimensional array with size of 6, see Line 11), each machine produces parts of the job (each array element only capitalizes a single letter in sequence, see Line 12-14). Such distributing operation is called “map”. In a MapReduce system, a master machine is also needed to assign the maps and reduce.

How about “reduce”?  A “reduce” operation is also called “fold”—for example, in Line 17, the operation to combine all the separately values into a single value: combine results from multiple worker machines.

 [1]: http://www.jiangtanghu.com/blog/2011/09/14/analytical-valley/
 [2]: http://hadoop.apache.org/
 [3]: http://en.wikipedia.org/wiki/Mapreduce
 [4]: http://static.googleusercontent.com/external_content/untrusted_dlcp/labs.google.com/en//papers/mapreduce-osdi04.pdf
 [5]: http://jiangtanghu.com/docs/en/MapReduce.sas
 []: http://dl.dropbox.com/u/69732603/MapReduce.png