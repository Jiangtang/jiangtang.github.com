---
id: 1396
title: 'SAS MapReduce: A Quick Followup by DS2'
date: 2015-09-04T14:01:30+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1396
permalink: /2015/09/04/sas-mapreduce-a-quick-followup-by-ds2/
category: SAS
tags:
  - DS2
  - MapReduce
  - SAS
---
<font size="2">(</font><a href="https://support.sas.com/documentation/cdl/en/proc/67916/HTML/default/viewer.htm#n0ox2hnyx7twb2n13200g5hqqsmy.htm" target="_blank"><font size="2">DS2</font></a> <font size="2">would be the king!) Years ago I made up </font><a href="http://www.jiangtanghu.com/blog/2011/10/04/map-and-reduce-in-mapreduce-a-sas-illustration/" target="_blank"><font size="2">a piece of SAS code to demonstrate the basic idea of Map-Reduce</font></a><font size="2">. Now this idea can be best implemented by this piece of workable program with </font><a href="https://support.sas.com/documentation/cdl/en/proc/67916/HTML/default/viewer.htm#n0ox2hnyx7twb2n13200g5hqqsmy.htm" target="_blank"><font size="2">PROC DS2</font></a> <font size="2">(tested in SAS 9.4 TS1M2, Win7):</font>

> <font size="2" face="Courier New">PROC DS2;</font>
> 
> <font size="2" face="Courier New">/* create some data &#8211;*/ <br />data input_data / overwrite = yes; <br />dcl double d; <br />method init(); <br />&#160;&#160; dcl int i; <br />&#160;&#160; do i = 1 to 10000000; <br />&#160;&#160;&#160;&#160;&#160; /*&#8211; create some money values &#8211;*/ <br />&#160;&#160;&#160;&#160;&#160; d = round( (ranuni(123) * 10 ), .01 ); <br />&#160;&#160;&#160;&#160;&#160; output; <br />&#160;&#160; end; <br />end; <br />enddata; <br />run;</font>
> 
> <font size="2" face="Courier New">/*&#8211; count the rows in multiple threads &#8211;*/ <br /><strong>thread</strong> <font color="#ff0000">map</font> / overwrite = yes; <br />dcl double c s; <br />keep c s; <br />method run(); <br />&#160;&#160; set input_data; <br />&#160;&#160; /*&#8211; the more compuation here, the more benefit &#8211;*/ <br />&#160;&#160; c + 1; <br />&#160;&#160; s + d; <br />end; <br />method term(); <br />&#160;&#160; output; <br />&#160;&#160; put s= c=; <br />end; <br />endthread; <br />run;</font>
> 
> <font size="2" face="Courier New">/*&#8211; blend the results into one total &#8211;*/ <br />data <font color="#ff0000">reduce</font> / overwrite = yes; <br />dcl thread map m; <br />dcl double totc tots; <br />keep totc tots; <br />method run(); <br />&#160;&#160; set from m <font color="#ff0000">threads=4</font>; <br />&#160;&#160; totc + c; <br />&#160;&#160; tots + s; <br />end; <br />method term(); <br />&#160;&#160; output; <br />end; <br />enddata; <br />run; <br />quit;</font>
> 
> <font size="2" face="Courier New">proc print data=reduce; run; <br /></font>

<font size="2">Notice the option of “<font color="#ff0000">threads=4</font>”. You can specify the thread as any number you want (the number of slaves..).</font>

<font size="2">Thanks </font><a href="https://www.linkedin.com/pub/robert-ray/29/814/b73" target="_blank"><font size="2">Robert Ray</font></a> <font size="2">of SAS Institute to kindly allow me to post his code.</font>