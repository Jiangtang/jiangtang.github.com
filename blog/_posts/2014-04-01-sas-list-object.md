---
id: 1326
title: 'Use List Object in SAS: Yet Another Undocumented Feature in SAS 9.4'
date: 2014-04-01T23:42:24+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1326
permalink: /2014/04/01/sas-list-object/
categories:
  - R
  - SAS
tags:
  - Python
  - R
  - SAS
---
Last year I gave a talk in SESUG 2013 on [list manipulation on SAS using a collection of function-like macros](http://analytics.ncsu.edu/sesug/2013/BtB-18.pdf). Today I just explored in my recently upgraded SAS 9.4 that I can play with list natively, which means I can create a list, slice a list and do other list operations in Data Steps! This is not documented yet(which means it will not be supported by the software vendor) and I can see warning message in Log window like “WARNING: List object is preproduction in this release”,  and it is still limited somehow, so use it in your own risk (and of course, fun).  Adding such versatile list object will definitely make SAS programmers more powerful. I will keep watch its further development.

\***\***\***\******<span style="color: #ff0000;">Update</span>**\***\*****

Some readers emailed to me that they can’t get the expected results as I did here. I think it’s best to check your own system:

I. Make sure you use the latest SAS software. I only tested on a 64-bit Window 7 machine with SAS 9.4 TS1M1:

[<img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border-width: 0px;" title="SAS94" alt="SAS94" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/SAS94_thumb.png" width="442" height="186" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/SAS94.png)

II. Make sure all hotfixes were applied (You can use this [SAS Hot Fix Analysis, Download and Deployment Tool](http://ftp.sas.com/techsup/download/hotfix/HF2/SASHFADD.html)).

[<img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border-width: 0px;" title="hotfix" alt="hotfix" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/hotfix_thumb.png" width="432" height="252" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/hotfix.png)

\***\***\***\******<span style="color: #ff0000;">Update End</span>**\***\*****

The followings are some quick plays and I will report more after more research:

## 1. Create a List

It’s easy to create a list:

> <span style="font-family: 'Courier New';">data _null_;<br /> a = [&#8216;apple&#8217;, &#8216;orange&#8217;, &#8216;banana&#8217;];<br /> put a;<br /> run;</span>

the output in Log window:

[<img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border-width: 0px;" title="list1" alt="list1" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/list1_thumb.png" width="448" height="84" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/list1.png)

You can also transfer a string to a list:

> <span style="font-family: 'Courier New';">data _null_;<br /> a = &#8216;SAS94&#8217;<br /> b =list(a)<br /> put b;<br /> run;</span>

[<img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border-width: 0px;" title="list2" alt="list2" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/list2_thumb.png" width="460" height="80" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/list2.png)

## 2. Slice a List

Slicing a list is also pretty straightforward, like in R and Python:

> <span style="font-family: 'Courier New';">data _null_;<br /> a = [&#8216;apple&#8217;, &#8216;orange&#8217;, &#8216;banana&#8217;];<br /> b = a[0];<br /> c = a[:-1];<br /> d = a[1:2];<br /> put a;<br /> put b;<br /> put c;<br /> put d;<br /> run;</span>

[<img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border-width: 0px;" title="list3" alt="list3" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/list3_thumb.png" width="406" height="110" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/list3.png)

## 3. List is Immutable in SAS!?

I felt much confortable to play list operations in SAS but a weird thing just happened. I tried to change a value in a list:

> <span style="font-family: 'Courier New';">data _null_;<br /> a = [&#8216;apple&#8217;, &#8216;orange&#8217;, &#8216;banana&#8217;];<br /> a[0] = &#8216;Kivi&#8217;;<br /> put a;<br /> run;</span>

Unexpectedly, I got an error:

[<img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border-width: 0px;" title="list4" alt="list4" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/list4_thumb.png" width="443" height="76" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2014/04/list4.png)

hhh, I need to create a new list to hold such modification? This is funny.

Based on my quick exploration, the list object in SAS is pretty intuitive from a programmers’ point of view. But since it’s undocumented and I don’t know how long it will stay in “preproduction” phase,  just be careful to implement it in your production work.

Personally I feel very exciting to “hack” such wonderful list features in SAS 9.4. If well implemented, it will easily beat R and Python (which claim themselves supporting rich data types and objects) as a scripting language for SAS programmers. I will keep update in [this page](http://en.wikipedia.org/wiki/April_1).