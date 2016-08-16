---
id: 662
title: 'Statistical Notes (2): Equivalence Testing and TOST (Two One-Sided Test)'
date: 2012-09-12T22:39:23+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=662
permalink: /2012/09/12/tost-equivalence-test/
categories:
  - SAS
  - statistics
tags:
  - equivalence test
  - Geometric Mean
  - SAS
  - statistics
  - T-test
  - TOST
---
> _<a href="http://zedshaw.com/essays/programmer_stats.html" target="_blank"><font size="1">Programmers Need to Learn Statistics Or I will Kill Them All</font></a> <font size="1">–Zed A. Shaw</font>_

<font size="1">In an </font><a href="http://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/viewer.htm#statug_intropss_sect006.htm" target="_blank"><font size="1">equivalence testing</font></a><font size="1">&#160;</font>[<font size="1">example</font>](http://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/viewer.htm#statug_ttest_examples05.htm) <font size="1">against lognormal data,&#160; a TOST (Two One-Sided Test)&#160; option used in SAS TTEST procedure:</font>

> <font size="1" face="Courier New">proc ttest data=auc dist=lognormal <font color="#ff0000">tost(0.8, 1.25)</font>; <br />&#160;&#160; paired TestAUC*RefAUC; <br />run;</font>

<font size="1">And the output:</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="tost" border="0" alt="tost" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/tost_thumb.png" width="460" height="177" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/tost.png)

<font size="1">Since the 90% (<em>who not 95%? see below</em>) limit of the geometric mean ratio (0.9412) , [0.8634,1.0260], lies in the FDA endorsed equivalence bounds [0.8,1.25],&#160; then we can make a conclusion of “Equivalent” among these Test and Reference drugs. Following are the notes on how this so called TOST (Two One-Sided Test) works.</font>

<font size="1">In its original form, the hypothesis of equivalence testing is written as </font><a href="http://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/viewer.htm#statug_intropss_sect006.htm" target="_blank"><font size="1">difference on means</font></a> <font size="1">(equivalence by definition: not above the upper limit, and not below the lower limit):</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="hypo" border="0" alt="hypo" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/hypo_thumb.png" width="244" height="105" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/hypo.png)

<font size="1">Since our AUC example with lognormal data, the difference on means is transformed into a ratio,&#160; <a href="http://www.jiangtanghu.com/blog/2012/09/12/geomean/" target="_blank">geometric mean ratio</a>: if no difference in means, then the ratio simply equals 1. The two one-sided tests are (with form of ratio, not difference anymore):</font>

> <font size="1">I) upper one-sided T-test with a null ratio as the left bound of predefined limits, here is 0.8</font>
> 
> <font size="1">II) lower one-sided T-test with a null ratio as the right bound of predefined limits, here is 1.25.</font>

<font size="1">T-test I can be done as (with option sides=U, where U means upper one-sided test. This option also only goes with SAS 9.2 and later)</font>

> <font size="1" face="Courier New">proc ttest data=auc dist=lognormal h0=0.8&#160; <strong><font color="#ff0000">sides=U</font></strong>; <br />&#160;&#160; paired TestAUC*RefAUC; <br />run;</font>

<font size="1">And the output:</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="upper" border="0" alt="upper" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/upper_thumb.png" width="441" height="162" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/upper.png)

<font size="1">T-test II, lower one-sided (with option sides=L, where L means lower one-sided test):</font>

> <font size="1" face="Courier New">proc ttest data=auc dist=lognormal h0=1.25 <font color="#ff0000">sides=L</font>; <br />&#160;&#160; paired TestAUC*RefAUC; <br />run;</font>

<font size="1">And the output:</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="lower" border="0" alt="lower" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/lower_thumb.png" width="435" height="162" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/lower.png)

<font size="1">So, the two one-sided tests together get a limit of [0.8634,1.0260], which is exactly as same as we got before using TOST option, except the former noted as “95%” and the later, “90%”. That’s because, the 0.1 (<em>1-90%</em>) should be dividend by 2 for the two one-sided tests to ensure they can both get their 0.05 significance respectively. Namely, at significant level α=5%, the equivalence test gets a&#160; 100(1-2α)% = 90% interval.</font>

<font size="1">At last, the overall P-value, will take the maximum one in these two one-sided tests (here we get max{0.0031,<0.0001} = 0.0031).</font>

# SAS Notes

<font size="1">Just did a quick search, PROC MIXED seemed more popular for statisticians to perform equivalence test years before:</font>

<a href="http://onbiostatistics.blogspot.com/2012/04/cookbook-sas-codes-for-bioequivalence.html?utm_source=feedburner&utm_medium=feed&utm_campaign=Feed%3A+blogspot%2FsVwyB+%28On+Biostatistics+and+Clinical+Trials%29" target="_blank"><em><font size="1">Cookbook SAS Codes for Bioequivalence Test in 2x2x2 Crossover Design</font></em></a><font size="1">, by Chunqin Deng (2012)</font>

_<a href="http://www.lexjansen.com/pharmasug/2004/posters/po05.pdf" target="_blank"><font size="1">The Paired T-Test: Does PROC MIXED Produce the Same Results as PROC TTEST?</font></a>_ <font size="1">by Jack Nyberg (2004)</font>

<font size="1">Section 8.2<em> Bioequivalence Testing,</em> in</font> __<a href="http://www.amazon.com/Pharmaceutical-Statistics-Using-SAS-Practical/dp/159047886X" target="_blank"><font size="1"><em>Pharmaceutical Statistics Using SAS: A Practical Guide</em></font></a><font size="1">, by Alex Dmitrienko, Christy Chuang-Stein, and Ralph D&#8217;Agostino (2007)</font>

# <font style="font-weight: bold">Reference</font>

_<a href="http://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/viewer.htm#statug_ttest_syntax01.htm" target="_blank"><font size="1">SAS TTEST Procedure User Guide</font></a>_

_<a href="http://pubs.acs.org/doi/pdf/10.1021/ac053390m" target="_blank"><font size="1">Beyond the t-Test</font></a>_