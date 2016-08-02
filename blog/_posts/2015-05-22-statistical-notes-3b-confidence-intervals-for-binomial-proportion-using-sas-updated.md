---
id: 1386
title: 'Statistical Notes (3B): Confidence Intervals for Binomial Proportion Using SAS, Updated'
date: 2015-05-22T22:05:39+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1386
permalink: /2015/05/22/statistical-notes-3b-confidence-intervals-for-binomial-proportion-using-sas-updated/
categories:
  - SAS
  - statistics
tags:
  - Confidence Interval
  - SAS
  - statistics
---
<font size="1">This quick note serves as a supplementnote of my previous </font>[<font size="1">Statistical Notes (3): Confidence Intervals for Binomial Proportion Using SAS</font>](http://www.jiangtanghu.com/blog/2012/09/15/confidence-intervals-binomial-proportion/) <font size="1">which I will extend as a </font>[<font size="1">SESUG 2015</font>](http://www.sesug.org/SESUG2015/index.php) <font size="1">paper. Basically I added a new Blaker method to my <em><a href="https://raw.githubusercontent.com/Jiangtang/Programming-SAS/master/CI_Single_Proportion.sas">CI_Single_Proportion.sas</a></em> file and found more CIs from SAS PROC FREQ.</font>

<font size="1">First of all, call the script:</font>

> <font size="1"><font face="Courier New">filename CI url “</font><font face="Courier New"><a href="https://raw.github.com/Jiangtang/Programming-SAS/master/CI_Single_Proportion.sas">https://raw.github.com/Jiangtang/Programming-SAS/master/CI_Single_Proportion.sas</a>” ;</font> <br /><font face="Courier New">%include CI;</font></font>
> 
> <font size="1" face="Courier New">%CI_Single_Proportion(r=81,n=263);</font>

<font size="1">and the output:</font>

[<img title="CI_SAS" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border-top-width: 0px" border="0" alt="CI_SAS" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2015/05/CI_SAS_thumb.png" width="493" height="306" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2015/05/CI_SAS.png)

<font size="1">The #12 is the one newly added. We can get the same results by SAS PROC FREQ (I use SAS/Base 9.4, TS1M2, WIN64):</font>

> <font size="1" face="Courier New">data test; <br />input grp outcome $ count; <br />datalines; <br />1 f 81 <br />1 u 182 <br />;</font>
> 
> <font size="1" face="Courier New">ods select BinomialCLs; <br />proc freq data=test; <br />&#160;&#160;&#160; tables outcome / binomial (CL= <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; WALD <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; WILSON <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; CLOPPERPEARSON <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; MIDP <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; LIKELIHOODRATIO <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; JEFFREYS <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; AGRESTICOULL <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; LOGIT <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; BLAKER&#160; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; ); <br />&#160;&#160;&#160; weight Count; <br />run;</font>
> 
> <font size="1" face="Courier New">ods select BinomialCLs; <br />proc freq data=test; <br />&#160;&#160;&#160; tables outcome / binomial (CL = <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; WILSON(CORRECT) <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; WALD(CORRECT) <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; ); <br />&#160;&#160;&#160; weight Count; <br />run;</font>

<font size="1" face="Courier New">the output:</font>

[<img title="CI_SAS_FREQ" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border-top-width: 0px" border="0" alt="CI_SAS_FREQ" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2015/05/CI_SAS_FREQ_thumb.png" width="314" height="480" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2015/05/CI_SAS_FREQ.png)

<font size="1">Only #10 method is not implemented yet in SAS PROC FREQ. There are some Bayesian intervals available in SAS&#160; procedures but since I’m not familiar with Bayes, I will leave it blank by far.</font>