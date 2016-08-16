---
id: 1377
title: Calculating Covariance by SAS, A Brutal Way
date: 2015-05-12T15:56:16+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1377
permalink: /2015/05/12/calculating-covariance-by-sas-a-brutal-way/
categories:
  - SAS
tags:
  - SAS
  - statistics
---
<span style="font-size: xx-small">It was very disappointed that there is only one built-in method to calculate covariance in Base SAS: that’s in </span>[<span style="font-size: xx-small">PROC CORR</span>](http://support.sas.com/documentation/cdl/en/proc/67327/HTML/default/viewer.htm#p0v0y1on1hbxukn0zqgsp5ky8hc0.htm) <span style="font-size: xx-small">(while you can also do it in </span>[<span style="font-size: xx-small">SAS/IML</span>](http://blogs.sas.com/content/iml/2010/12/08/computing-covariance-and-correlation-matrices.html)<span style="font-size: xx-small">, of course):</span>

[<span style="font-size: xx-small"><img title="sascorr" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border-top-width: 0px" border="0" alt="sascorr" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2015/05/sascorr_thumb.png" width="443" height="249" /></span>](http://www.jiangtanghu.com/blog/wp-content/uploads/2015/05/sascorr.png)

<span style="font-size: xx-small">The following is a quick-and-dirty way to get a function like %COV:</span>

> <font face="Courier New">%macro COV(data, var1,var2); <br />&#160;&#160;&#160; %local _cov; <br />&#160;&#160;&#160; %let rc = %sysfunc(dosubl(%str(</font>
> 
> <font face="Courier New">&#160;&#160;&#160; ods select none ; <br />&#160;&#160;&#160; ods output cov=_cov;</font>
> 
> <font face="Courier New">&#160;&#160;&#160; proc corr data=&data&#160; cov ; <br />&#160;&#160;&#160; var &var1 &var2 ; <br />&#160;&#160;&#160; run;</font>
> 
> <font face="Courier New">&#160;&#160;&#160; ods select all;</font>
> 
> <font face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; proc sql noprint; <br />&#160;&#160;&#160; select &var2 into :_cov <br />&#160;&#160;&#160; from _cov&#160; (obs=1) <br />&#160;&#160;&#160; ; <br />&#160;&#160;&#160; drop table&#160; _cov; <br />&#160;&#160;&#160; quit <br />&#160;&#160;&#160; ))); <br />&#160;&#160;&#160; &_cov <br />%mend COV;</font>
> 
> <span style="font-size: xx-small; font-family: &#39;Courier New&#39;"></span>

<span style="font-size: xx-small">You can use it in macro variable assignment:</span>

> <span style="font-size: xx-small; font-family: &#39;Courier New&#39;">%let cov = %COV(sashelp.iris,SepalLength,SepalWidth);</span>

<span style="font-size: xx-small">or in a data step:</span>

> <span style="font-size: xx-small; font-family: &#39;Courier New&#39;">data iris; <br />&#160;&#160;&#160; set sashelp.iris; <br />&#160;&#160;&#160; cov = %COV(sashelp.iris,SepalLength,SepalWidth); <br />run;</span>

<span style="font-size: xx-small">or in PROC SQL:</span>

> <span style="font-size: xx-small; font-family: &#39;Courier New&#39;">proc sql; <br />&#160;&#160;&#160; create table iris2 as <br />&#160;&#160;&#160; select *, <br />&#160;&#160;&#160; %COV(sashelp.iris,SepalLength,SepalWidth) as cov <br />&#160;&#160;&#160; from sashelp.iris; <br />quit;</span>

<span style="font-size: xx-small">One line conclusion: I LOVE </span>[<span style="font-size: xx-small">Dosubl</span>](http://www.jiangtanghu.com/blog/2015/03/09/list-manipulations-made-easy-and-little-bit-of-ugly-the-new-dosubl-function/) and hope this Dosubl also inspires your programming<span style="font-size: xx-small">!</span>