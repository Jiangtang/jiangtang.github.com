---
id: 518
title: Happy Leap Year From Logical (Point of View) Operators
date: 2012-02-29T00:14:07+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=518
permalink: /2012/02/29/happy-leap-year-from-logical-point-of-view-operators/
categories:
  - SAS
tags:
  - logic operator
  - SAS
---
<font size="1">Today is Feb 29, –another <a href="http://en.wikipedia.org/wiki/Leap_year" target="_blank">leap year</a>! I just found it is a good chance to raise the topic of <a href="http://www.jiangtanghu.com/blog/2010/11/04/power-of-logic-operators-a-trick/" target="_blank">logic operators again</a>.</font>

<font size="1">To determine if 2012 is a leap year, use the straightforward logic expression (demo is SAS, follow the pseudo code in the wiki page of <a href="http://en.wikipedia.org/wiki/Leap_year" target="_blank">leap year</a>):</font>

> <font size="1" face="Courier New">if mod(year,4) = 0 then do;&#160;&#160; <br />&#160;&#160;&#160; if mod(year,100) = 0 then do;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; if mod(year,400) = 0 then is_leap = 1; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; else is_leap = 0; <br />&#160;&#160;&#160; end; <br />&#160;&#160;&#160; else is_leap = 1; <br />end; <br />else leap=0;</font>

<font size="1">while using logic operators (Boolean expression), only one line of codes needed:</font>

> <font size="1" face="Courier New">is_leap = (mod(year,4) = 0) <font color="#ff0000">and</font> <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; ( <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; (mod(year,100) ^= 0) <font color="#ff0000">or</font> (mod(year,400) = 0) <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; );</font> 

<font size="1">or using SAS bitwise logical operations:</font>

> <font size="1" face="Courier New">is_leap=<font color="#ff0000">bor</font>(<font color="#ff0000">band</font>(mod(year,4) = 0,mod(year,100) ^= 0), mod(year,400) = 0)</font>