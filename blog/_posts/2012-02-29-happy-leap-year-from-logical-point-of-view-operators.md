---
author: Jiangtang Hu
title: >
  Happy Leap Year From Logical (Point of
  View) Operators
excerpt:
layout: post
category:
  - SAS
tags:
  - logic operator
  - SAS
post_format: [ ]
---
Today is Feb 29, –another [leap year][1]! I just found it is a good chance to raise the topic of [logic operators again][2].

To determine if 2012 is a leap year, use the straightforward logic expression (demo is SAS, follow the pseudo code in the wiki page of [leap year][1]):

> if mod(year,4) = 0 then do;     
>     if mod(year,100) = 0 then do;             
>         if mod(year,400) = 0 then is_leap = 1;   
>         else is_leap = 0;   
>     end;   
>     else is_leap = 1;   
> end;   
> else leap=0;

while using logic operators (Boolean expression), only one line of codes needed:

> is_leap = (mod(year,4) = 0) and   
>           (   
>             (mod(year,100) ^= 0) or (mod(year,400) = 0)   
>           ); 

or using SAS bitwise logical operations:

> is_leap=bor(band(mod(year,4) = 0,mod(year,100) ^= 0), mod(year,400) = 0)

 [1]: http://en.wikipedia.org/wiki/Leap_year
 [2]: http://www.jiangtanghu.com/blog/2010/11/04/power-of-logic-operators-a-trick/