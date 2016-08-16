---
id: 1176
title: Localize Your Macro Variable? Mostly Not Needed or Do It If You Only Want to Initiate It
date: 2013-03-29T19:22:46+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1176
permalink: /2013/03/29/localizing-or-initiating/
categories:
  - SAS
tags:
  - Macro
  - SAS
  - scope
---
<span style="font-size: small;"><a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/03/Scope.jpg"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="Scope" alt="Scope" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/03/Scope_thumb.jpg" width="240" height="180" border="0" /></a></span>

<span style="color: #ff0000; font-size: small;"><strong>[NOTE2013-05-30: This post is permanently suspended. In this post, I only focused on the initialization effect of the %local statement and totally ignored its function to avoid variable collisions as Quentin mentioned in comment box.]</strong></span>

<span style="font-size: small;">A piece of SAS codes to create a list of all variables within a dataset (a nice programming trick from </span>[<span style="font-size: small;">Art Carpenter, 2004</span>](http://www2.sas.com/proceedings/sugi30/028-30.pdf)<span style="font-size: small;">):</span>

> <span style="font-family: 'Courier New'; font-size: small;">%macro getvars(dset) ;<br /> <span style="color: #ff0000;">%local varlist ;</span><br /> %let fid = %sysfunc(open(&dset)) ;<br /> %if &fid %then %do ;<br /> %do i=1 %to %sysfunc(attrn(&fid,nvars)) ;<br /> %let <span style="color: #ff0000;">varlist</span>= <span style="color: #ff0000;">&varlist</span> %sysfunc(varname(&fid,&i));<br /> %end ;<br /> %let fid = %sysfunc(close(&fid)) ;<br /> %end ;<br /> &varlist<br /> %mend ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: small;">%put %getvars(%str(sashelp.iris));</span>

<span style="font-size: small;">One question would be: why declare macro variable <em>varlist</em> as local explicitly by a <em>%local</em> statement? Since it was defined within the macro <em>%getvar</em>, it just went to the local macro table automatically and the <em>%local</em> statement is not necessary anymore!</span>

<span style="font-size: small;">Such argument is definitely right. But the <em>%local</em> statement above was not intent to localize a macro variable, actually, it’s used to initiate it. If you just delete it, you will get a warning then an error:</span>

> <span style="font-size: small;">WARNING: Apparent symbolic reference VARLIST not resolved.<br /> ERROR: The text expression &VARLIST SPECIES contains a recursive reference to the macro variable VARLIST.  The<br /> macro variable will be assigned the null value.</span>

<span style="font-size: small;">This is because the macro variable <span style="color: #ff0000;"><em>&varlist</em></span><span style="color: #cccccc;"> in right side of the second</span> <em>%let</em> statement was not declared before. To be clear, you can also replace the <em>%local</em> statement  with an explicit initiating statement:</span>

> <span style="color: #ff0000; font-family: 'Courier New'; font-size: small;">%let varlist=;</span>

<span style="font-size: small;">In this example, the <em>%local</em> statement and the <em>%let</em> statement simply do the same job and the choice is totally subject to programmers’ preference(<em>well I prefer the later</em>).</span>

<span style="font-size: small;">So, take home question: any comments on the following snippet to count the numbers of word in a string<span style="font-size: small;">(also from </span><a href="http://www2.sas.com/proceedings/sugi30/028-30.pdf"><span style="font-size: small;">Art Carpenter, 2004</span></a>; <em>sorry Carpenter, your books and papers are the most familiar sources for me to learn SAS macro programming</em><span style="font-size: small;">)</span>:</span>

> <span style="font-family: 'Courier New'; font-size: small;">%macro wordcount(list);<br /> <span style="color: #ff0000;">    %local count;<br /> %let count=0;</span><br /> %do %while(%qscan(&list,&count+1,%str( )) ne %str());<br /> %let count = %eval(&count+1);<br /> %end;<br /> &count<br /> %mend wordcount;</span>
> 
> <span style="font-family: 'Courier New'; font-size: small;">%put %wordcount(a b cd);</span>