---
id: 1247
title: 'Everything You Need to Know about Your SAS Session and No More&hellip;'
date: 2013-08-25T23:20:46+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1247
permalink: /2013/08/25/everything-you-need-to-know-about-your-sas-session-and-no-more/
categories:
  - SAS
tags:
  - SAS
---
<span style="font-size: xx-small;">You will get rich information for your SAS session(definitely more than you need) by submitting:</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">%put _all_; *all system macro variables;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">proc setinit; *all licensed software;<br /> run;</span>
> 
> proc product_status;
  
> run;
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">proc options; *options;<br /> run;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">proc javainfo;  *Java infor;<br /> run;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">proc registry list; *registry;<br /> run;</span>