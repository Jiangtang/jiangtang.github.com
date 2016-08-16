---
id: 1355
title: To Exit or Not Exit, the SAS Ways
date: 2014-09-11T22:55:59+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1355
permalink: /2014/09/11/to-exit-or-not-exit-the-sas-ways/
categories:
  - SAS
tags:
  - Logic
  - SAS
---
> <font size="1">The tragedy of life is not that it ends so soon, but that we wait so long to begin it. –by W. M. Lewis</font>

<font size="1">So, which is the exit style you prefer, in the following 3 macros (which are all valid SAS codes): </font>

> <font size="1" face="Courier New">/*#1 if branch*/ <br />%macro tragedy_of_life1(ds); <br />&#160;&#160;&#160; %if %sysfunc(exist(&ds)) %then %do; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; proc print data=&ds noobs; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; run; <br />&#160;&#160;&#160; %end; <br />&#160;&#160;&#160; <font color="#ff0000">%else %do</font>; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; %put ERROR: Dataset &ds not exist.; <br />&#160;&#160;&#160; %end; <br />%mend;</font>
> 
> <font size="1" face="Courier New">/*#2 abort*/ <br />%macro tragedy_of_life2(ds); <br />&#160;&#160;&#160; %if %sysfunc(exist(&ds)) ^= 1 %then %do; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; %put ERROR: Dataset &ds not exist.; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; %<font color="#ff0000">abort</font> cancel;&#160;&#160;&#160; <br />&#160;&#160;&#160; %end;</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160; proc print data=&ds noobs; <br />&#160;&#160;&#160; run; <br />%mend;</font>
> 
> <font size="1" face="Courier New">/*#3 goto*/ <br />%macro tragedy_of_life3(ds); <br />&#160;&#160;&#160; %if %sysfunc(exist(&ds)) ^= 1 %then %do; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; %put ERROR: Dataset &ds not exist.; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; %<font color="#ff0000">goto</font> iExit;&#160;&#160;&#160; <br />&#160;&#160;&#160; %end;</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160; proc print data=&ds noobs; <br />&#160;&#160;&#160; run;</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160; %iExit: <br />%mend;</font>

<font size="1">I personally use #2, <em><strong>%abort cancel</strong></em>. For <strong><em>goto</em></strong> in #3, it might not a good idea to use <strong><em>goto</em></strong> statement in any cases, so I avoid it as long as I can. </font>

<font size="1">#1 is good, but you can imagine that the branches will grow dramatically if lots of exceptions are under checking. <em><strong>%abort cancel</strong></em> in #2 will best serve the purpose to isolate the blocks.</font>