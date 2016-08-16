---
id: 788
title: 'A SAS 9.3 Macro Trick: %put &amp;=var'
date: 2012-11-08T20:09:50+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=788
permalink: /2012/11/08/a-sas-9-3-macro-trick-put-var/
categories:
  - SAS
tags:
  - Macro
  - SAS
---
<font size="1">This is new since SAS 9.3 on how to display macro variable name and its value. Try to run</font>

> <font size="1" face="Courier New">%let <font color="#ff0000">var</font>=1,2,3; <br />%put <font color="#00ff00">&</font>=<font color="#ff0000">var</font>;</font>

<font size="1">or</font>

> <font size="1" face="Courier New">%macro test(<font color="#ff0000">var</font>); <br />&#160;&#160;&#160; %put <font color="#00ff00">&</font>=<font color="#ff0000">var</font>; <br />%mend; <br />%test(%str(1,2,3))</font>

<font size="1">and you will get in Log window</font>

> <font size="1">VAR=1,2,3</font>

<font size="1">You can read from <a href="http://support.sas.com/documentation/cdl/en/mcrolref/62978/HTML/default/viewer.htm#n189qvy83pmkt6n1bq2mmwtyb4oe.htm" target="_blank">SAS 9.3 online doc</a>:</font>

> <font size="1">If you place an equal sign between the <font color="#00ff00">ampersand</font> and the <font color="#ff0000">macro variable</font> <font color="#ff0000">name</font> of a direct macro variable reference, the macro variable&#8217;s name displays in the log along with the macro variable&#8217;s value.</font>

<font size="1">In SAS 9.2 and prior, you should type the macro variable twice:</font>

> <font size="1" face="Courier New">%let var=1,2,3; <br />%put var=&var;</font>

<font size="1">PS: it is called a “Tip” in <a href="http://support.sas.com/documentation/cdl/en/mcrolref/62978/HTML/default/viewer.htm#n189qvy83pmkt6n1bq2mmwtyb4oe.htm" target="_blank">SAS 9.3 online doc</a>, but I’d rather call it a trick: <font size="1">not critical but nice to have (<em>save your typing!</em>). You may be also interested in <a href="http://blogs.sas.com/content/iml/2010/11/01/tips-and-techniques-whats-the-difference/" target="_blank">Rick Wicklin’s differentiation on Tip and Technique</a>.</font></font>