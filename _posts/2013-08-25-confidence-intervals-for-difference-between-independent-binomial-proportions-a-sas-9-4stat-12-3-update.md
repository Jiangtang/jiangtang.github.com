---
id: 1251
title: 'Confidence Intervals for Difference Between Independent Binomial Proportions: A SAS 9.4/STAT 12.3 Update'
date: 2013-08-25T23:32:29+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1251
permalink: /2013/08/25/confidence-intervals-for-difference-between-independent-binomial-proportions-a-sas-9-4stat-12-3-update/
categories:
  - SAS
  - statistics
tags:
  - Binomial proportion inverval
  - Confidence Interval
  - SAS
  - SAS 9.4
  - statistics
---
<font size="1">For the computing of confidence intervals for difference between two independent binomial proportions in SAS 9.4/STAT 12.3, it’s hard to figure out exactly how many methods are available because there is no “CL=ALL” trigger in RISKDIFF option (but you can get one in <a href="http://www.jiangtanghu.com/blog/2013/08/22/confidence-intervals-for-binomial-proportion-a-sas-9-4stat-12-3-update/">BIONOMIAL option</a> to compute the confidence intervals for binomial proportion). As far as I hacked, I got 11 intervals (</font>[<font size="1">last year I tried SAS 9.3 and got 8</font>](http://www.jiangtanghu.com/blog/2012/09/23/statistical-notes-5-confidence-intervals-for-difference-between-independent-binomial-proportions-using-sas/)<font size="1">; codes available below):</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="CI_diff_94" border="0" alt="CI_diff_94" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/08/CI_diff_94_thumb.png" width="392" height="346" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/08/CI_diff_94.png)

<font size="1">1. There 3 new methods I just got from SAS 9.4/STAT 12.3 are&#160; Miettinen-Nurminen-Mee, Miettinen-Nurminen and Agresti-Caffo.</font>

<font size="1">2.&#160; The methods with number marks are align with Prof. Newcombe ’s paper, <em><a href="http://www.ncbi.nlm.nih.gov/pubmed/9595617?dopt=Abstract"><strong>Interval estimation for the difference between independent proportions: comparison of eleven methods</strong></a><strong>&#160;</strong>(a fraction of outputs attached in <a href="http://www.jiangtanghu.com/blog/2012/09/23/statistical-notes-5-confidence-intervals-for-difference-between-independent-binomial-proportions-using-sas/">my post</a>)</em>.</font>

<font size="1">3. I’m still trying to figure out why the <font color="#ff0000">exact</font> method produces different numbers compared to what’s in Prof. Newcombe’s report.</font>

<font size="1">4. The codes produced the outputs:</font>

> <font size="1" face="Courier New">data ci; <br />&#160;&#160;&#160; input grp res count; <br />datalines; <br />1 0 56 <br />1 1 14 <br />2 0 48 <br />2 1 32 <br />;</font>
> 
> <font size="1" face="Courier New">/* <br />non-exactmethods: <br />Agresti-Caffo <br />Farrington-Manning <br />Hauck-Anderson <br />Miettinen-Nurminen <br />Newcombe Score <br />Wald <br />*/ </font>
> 
> <font size="1" face="Courier New">ods select&#160; PdiffCLs; <br />ods output PdiffCLs=ci1; <br />proc freq data=ci order=data; <br />&#160;&#160;&#160; tables grp*res /riskdiff (CL=(AC FM HA MN WILSON WALD)); <br />&#160;&#160;&#160; weight count; <br />run;</font>
> 
> <font size="1" face="Courier New">/* <br />exact methods: <br />Exact <br />Exact (FM Score) <br />*/ <br />ods select&#160; PdiffCLs; <br />ods output PdiffCLs=ci2; <br />proc freq data=ci order=data; <br />&#160;&#160;&#160; tables grp*res /riskdiff (CL=(EXACT)); <br />&#160;&#160;&#160; weight count; <br />&#160;&#160;&#160; exact riskdiff; <br />run;</font>
> 
> <font size="1" face="Courier New">ods select&#160; PdiffCLs; <br />ods output PdiffCLs=ci3; <br />proc freq data=ci order=data; <br />&#160;&#160;&#160; tables grp*res /riskdiff (CL=(EXACT)); <br />&#160;&#160;&#160; weight count; <br />&#160;&#160;&#160; exact riskdiff(fmscore); <br />run;</font>
> 
> <font size="1" face="Courier New">/* <br />methods (CC): <br />Mee <br />Newcombe Score (Corrected) <br />Wald (Corrected) <br />*/ <br />ods select&#160; PdiffCLs; <br />ods output PdiffCLs=ci4; <br />proc freq data=ci order=data; <br />&#160;&#160;&#160; tables grp*res /riskdiff (CORRECT CL=(MN(CORRECT=NO) WILSON WALD)); <br />&#160;&#160;&#160; weight count; <br />run;</font>
> 
> <font size="1" face="Courier New">data CI_all; <br />&#160;&#160;&#160; set ci4 ci3 ci2 ci1; <br />&#160;&#160;&#160; CI='(&#8216;||compress(put(LowerCL,8.4))||&#8217;, &#8216;||compress(put(UpperCL,8.4))||&#8217;)&#8217;; <br />run;</font>
> 
> <font size="1" face="Courier New">proc sql; <br />&#160;&#160;&#160; select <br />&#160;&#160;&#160; case Type <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Wald" then "a" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Wald (Corrected)" then "b" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Miettinen-Nurminen-Mee" then "b1" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Miettinen-Nurminen" then "b2"&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Agresti-Caffo" then "b3" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Exact" then "c" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Exact (FM Score)" then "d" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Newcombe Score" then "e" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Newcombe Score (Corrected)" then "f" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Farrington-Manning" then "g" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; when "Hauck-Anderson" then "h" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; else "i" <br />&#160;&#160;&#160; end as order length=2, <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; Type "method", <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; CI "95% Confidence Limits" <br />&#160;&#160;&#160; from CI_all <br />&#160;&#160;&#160; order by order <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; ; <br />quit;</font>