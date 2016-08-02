---
id: 1148
title: Linguistic Sorting in SAS Proc Sort
date: 2013-02-19T23:31:04+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1148
permalink: /2013/02/19/linguistic-sorting-in-sas-proc-sort/
categories:
  - SAS
tags:
  - NLS
  - SAS
  - SORT
---
<font size="1">Just took a look at the linguistic sorting features in </font>[<font size="1">SAS Sort procedure</font>](http://support.sas.com/documentation/cdl/en/proc/65145/HTML/default/viewer.htm#p1nd17xr6wof4sn19zkmid81p926.htm)<font size="1">, and got some neat options to apply to my task. For example, I want to sort ID in the following dataset:</font>

> <font size="1" face="Courier New">data t1; <br />&#160;&#160;&#160; input ID $ ; <br />datalines; <br />T20 <br />T4 <br />T3 <br />T1 <br />;</font>

<font size="1">and want to get such intuitive orderings (files sorting in Window 7 directory):</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="sort_num" border="0" alt="sort_num" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/sort_num_thumb.png" width="411" height="214" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/sort_num.png)

<font size="1">But when apply the default sorting:</font>

> <font size="1" face="Courier New">proc sort data=t1 out=t2; <br />&#160;&#160;&#160; by ID; <br />run;</font>

<font size="1">I get:</font>

> <font size="1" face="Courier New">T1 <br />T20 <br />T3 <br />T4</font>

<font size="1">To produce what expected, add a <font color="#ff0000">SORTSEQ</font> option:</font>

> <font size="1"><font face="Courier New">proc sort data=t1 out=t3&#160;&#160; <br />&#160;&#160;&#160; <font color="#ff0000">SORTSEQ=LINGUISTIC(NUMERIC_COLLATION=ON)</font> <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; ; <br />&#160;&#160;&#160; by ID; <br />run; </font></font>

> <font size="1"><font face="Courier New">T1 <br />T3 <br />T4 <br />T20</font></font>

<font size="1">In the first block of code, the default sorting is determined by their characters’ appearance in <a href="en.wikipedia.org/wiki/EBCDIC">EBCDIC</a> or the <a href="en.wikipedia.org/wiki/ASCII">ASCII</a> tables (according to OS). To change this default collating sequences, a specific linguistic collation (numeric collation) option added. </font>

<font size="1">For details, <em>see</em> the corresponding part in <em><a href="http://support.sas.com/documentation/cdl/en/proc/65145/HTML/default/viewer.htm#p0guut2xk8yz2yn17ibn9nwcyx8v.htm">SAS SORT Procedure</a></em> and <a href="http://support.sas.com/documentation/cdl/en/nlsref/63072/HTML/default/viewer.htm#p1d7k16vtur7s4n1nbbaf8ro6sk7.htm"><em>Collating Sequence in SAS(R) 9.3 National Language Support (NLS)</em></a><em>&#160;</em>with <a href="http://www2.sas.com/proceedings/forum2007/297-2007.pdf">a great paper</a>.</font>