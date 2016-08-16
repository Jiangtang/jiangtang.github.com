---
id: 1253
title: Noninferiority Testing with SAS
date: 2013-08-26T22:59:27+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1253
permalink: /2013/08/26/noninferiority-testing-with-sas/
categories:
  - SAS
  - statistics
tags:
  - equivalence test
  - noninferiority test
  - PROC FREQ
  - Proc TTEST
  - SAS
  - statistics
---
<font size="1">I planed to extend nonWinferiority testing to one of my statistical notes,&#160; <em><a href="http://www.jiangtanghu.com/blog/2012/09/12/tost-equivalence-test/">Equivalence Testing and TOST (Two One-Sided Test)</a></em> since noninferiority test is simply half part of the equivalence test. Today I’m glad to find an even better explanation from</font>

> _[<font size="1">SAS Usage Note 48616: Design and analysis of noninferiority studies</font>](http://support.sas.com/kb/48/616.html)_

<font size="1">You will love it if you are interested in this subject (bookmark this link since it looks like unfinished somehow). Few comments:</font>

  * <font size="1">It’s better not to use a two-side test for noninferiority testing. In PROC TTEST, you can add option like “<font face="Courier New">side=U</font>” or “<font face="Courier New">side=L</font>”. </font>
  * <font size="1">If you do like a two-side test for noninferiority testing, it’s OK but DO remember assign an alpha value of 0.1 since the default value is 0.05 (if you’re lost by this statement, read this </font>[<font size="1">post</font>](http://www.jiangtanghu.com/blog/2012/09/12/tost-equivalence-test/) <font size="1">again). It’s pretty tricky and I saw lots of mistakes due to ignoring of this point.</font>
  * <font size="1">In note </font>[<font size="1">48616</font>](http://support.sas.com/kb/48/616.html)<font size="1">, it is said only test of mean(s) is supported by PROC TTEST. Actually, PROC TTEST can also test ratios (a </font>[<font size="1">log-transformation</font>](http://www.jiangtanghu.com/blog/2012/09/12/geomean/) <font size="1">will be applied) by a&#160; “<font face="Courier New">dist=lognormal</font>” option.</font>
  * <font size="1">To make decision in noninferiority, superiority, and equivalence testings, lower or/and upper limits are used to compare with the margin(s) rather than the P-value. They are of course equivalent but the former approach is much more accessible and meaningful for non-statistician researchers.</font>