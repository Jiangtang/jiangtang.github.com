---
id: 721
title: 'Statistical Notes (5): Confidence Intervals for Difference Between Independent Binomial Proportions Using SAS'
date: 2012-09-23T21:23:59+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=721
permalink: /2012/09/23/statistical-notes-5-confidence-intervals-for-difference-between-independent-binomial-proportions-using-sas/
categories:
  - SAS
  - statistics
tags:
  - Binomial proportion inverval
  - Confidence Interval
  - PROC FREQ
  - R
  - SAS
  - statistics
---
> <font size="1">A guy notices a bunch of targets scattered over a barn wall, and in the center of each, in the "bulls-eye," is a bullet hole. "Wow," he says to the farmer, "that&#8217;s pretty good shooting. How&#8217;d you do it?" "Oh," says the farmer, "it was easy. I painted the targets after I shot the holes." – An Old Joke</font>

<font size="1">Note on how to get the difference between independent binomial proportions using SAS </font><a href="http://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/viewer.htm#statug_freq_toc.htm" target="_blank"><font size="1">PROC FREQ</font></a> <font size="1">(tested in SAS 9.3M1).&#160; Also, benchmarks took from Prof. Newcombe ’s paper:</font>

> <cite><a href="http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?cmd=Retrieve&db=pubmed&dopt=Abstract&list_uids=9595617&query_hl=1"><strong><font size="1">Interval estimation for the difference between independent proportions: comparison of eleven methods.</font></strong></a><font size="1"> </font></cite>

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="Newcombe_diff" border="0" alt="Newcombe_diff" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/08/Newcombe_diff_thumb4.png" width="291" height="297" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/08/Newcombe_diff4.png)

<font size="1">Key findings (SAS output):</font>

[<img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="CI8" border="0" alt="CI8" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/CI8_thumb.png" width="436" height="255" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/CI8.png)

<font size="1">1. SAS Proc Freq offers 8 ( including 4 of total 11 in Prof. Newcombe ’s paper) methods to compute confidence intervals for difference between independent binomial proportions:</font>

  * <font size="1">Wald <font color="#ff0000">#1</font></font> 
  * <font size="1">Wald (Corrected) <font color="#ff0000">#2</font></font> 
  * <font size="1">Exact</font> 
  * <font size="1">Exact (FM Score)</font> 
  * <font size="1">Newcombe Score <font color="#ff0000">#10</font></font> 
  * <font size="1">Newcombe Score (Corrected) <font color="#ff0000">#11</font></font> 
  * <font size="1">Farrington-Manning</font> 
  * <font size="1">Hauck-Anderson</font> 

<font size="1">Note that #1 method is the most popular one in textbook, #10 might&#160; be the most wildly used method in industry.</font>

<font size="1">2. There is a big discrepancy in the outputs in the&#160; so called “<strong>exact</strong>” method among&#160; SAS Proc Freq and Prof. Newcombe ’s paper. Seems they used different methods (in the same “exact” families) under same name. Needs further investigation.</font>

<font size="1">The SAS codes:</font>

> <font size="1" face="Courier New">/* <br />2*2 table </font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; response0 response1 <br />group1&#160;&#160;&#160;&#160;&#160; 56&#160;&#160;&#160;&#160;&#160; 14 <br />group2&#160;&#160;&#160;&#160;&#160; 48&#160;&#160;&#160;&#160;&#160; 32 <br />*/</font>
> 
> <font size="1" face="Courier New">data ci; <br />&#160;&#160;&#160; input grp res count; <br />datalines; <br />1 0 56 <br />1 1 14 <br />2 0 48 <br />2 1 32 <br />;</font>
> 
> <font size="1" face="Courier New">/* <br />methods: <br />Exact <br />Farrington-Manning <br />Hauck-Anderson <br />Newcombe Score <br />Wald <br />*/ <br />ods select&#160; PdiffCLs; <br />ods output PdiffCLs=ci1; <br />proc freq data=ci order=data; <br />&#160;&#160;&#160; tables grp*res /riskdiff (CL=(EXACT FM HA WILSON WALD)); <br />&#160;&#160;&#160; weight count; <br />&#160;&#160;&#160; exact riskdiff; <br />run;</font>
> 
> <font size="1" face="Courier New">/* <br />methods: <br />Exact (FM Score) <br />*/ <br />ods select&#160; PdiffCLs; <br />ods output PdiffCLs=ci2; <br />proc freq data=ci order=data; <br />&#160;&#160;&#160; tables grp*res /riskdiff (CL=(EXACT)); <br />&#160;&#160;&#160; weight count; <br />&#160;&#160;&#160; exact riskdiff(fmscore); <br />run;</font>
> 
> <font size="1" face="Courier New">/* <br />methods: <br />Newcombe Score (Corrected) <br />Wald (Corrected) <br />*/ <br />ods select&#160; PdiffCLs; <br />ods output PdiffCLs=ci3; <br />proc freq data=ci order=data; <br />&#160;&#160;&#160; tables grp*res /riskdiff (CORRECT CL=(WILSON WALD)); <br />&#160;&#160;&#160; weight count; <br />&#160;&#160;&#160; exact riskdiff; <br />run; </font>
> 
> <font size="1" face="Courier New">/*put them all*/ <br />data CI_all; <br />&#160;&#160;&#160; set ci3 ci2 ci1; <br />&#160;&#160;&#160; CI='(&#8216;||compress(put(LowerCL,8.4))||&#8217;, &#8216;||compress(put(UpperCL,8.4))||&#8217;)&#8217;; <br />run;</font>
> 
> <font size="1" face="Courier New">proc sql; <br />&#160;&#160;&#160; select <br />&#160;&#160;&#160; case Type <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Wald" then "a" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Wald (Corrected)" then "b" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Exact" then "c" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Exact (FM Score)" then "d" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Newcombe Score" then "e" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Newcombe Score (Corrected)" then "f" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Farrington-Manning" then "g" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Hauck-Anderson" then "h" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; else "i" <br />&#160;&#160;&#160; end as order, <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; Type "method", <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; CI "95% Confidence Limits" <br />&#160;&#160;&#160; from CI_all <br />&#160;&#160;&#160; order by order <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; ; <br />quit;</font>
> 
> <font size="1"></font>

<font size="1">&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-</font>

<font size="1">You may be also interested in this post on calculating confidence intervals for single proportion: </font>

> [<font size="1">Statistical Notes (3): Confidence Intervals for Binomial Proportion Using SAS</font>](http://www.jiangtanghu.com/blog/2012/09/15/confidence-intervals-binomial-proportion/) <font size="1"></font>

<font size="1">using the following 11 methods:</font>

  * <font size="1">1.&#160; Simple asymptotic, Without CC | Wald</font> 
  * <font size="1">2.&#160; Simple asymptotic, With CC&#160;&#160;&#160;&#160;&#160;&#160; </font>
  * <font size="1">3.&#160; Score method, Without CC | Wilson&#160;&#160;&#160;&#160;&#160;&#160;&#160; </font>
  * <font size="1">4.&#160; Score method, With CC&#160;&#160;&#160;&#160; </font>
  * <font size="1">5. Binomial-based, &#8216;Exact&#8217; | Clopper-Pearson&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </font>
  * <font size="1">6.&#160; Binomial-based, Mid-p&#160;&#160;&#160;&#160;&#160;&#160; </font>
  * <font size="1">7.&#160; Likelihood-based&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </font>
  * <font size="1">8.&#160; Jeffreys&#160;&#160;&#160;&#160; </font>
  * <font size="1">9.&#160; Agresti-Coull,z^2/2 successes&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </font>
  * <font size="1">10. Agresti-Coull,2 successes and 2 fail&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </font>
  * <font size="1">11. Logit&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; </font>