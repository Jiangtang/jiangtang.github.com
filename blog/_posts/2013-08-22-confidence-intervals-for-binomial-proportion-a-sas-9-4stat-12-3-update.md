---
id: 1245
title: 'Confidence Intervals for Binomial Proportion: A SAS 9.4/STAT 12.3 Update'
date: 2013-08-22T10:57:01+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1245
permalink: /2013/08/22/confidence-intervals-for-binomial-proportion-a-sas-9-4stat-12-3-update/
categories:
  - SAS
  - statistics
tags:
  - Binomial proportion inverval
  - Confidence Interval
  - SAS
  - SAS 9.4
  - statistics
---
<font size="1">After getting the access to </font>[<font size="1">SAS 9.4</font>](http://www.jiangtanghu.com/blog/2013/07/28/open-box-sas-9-4-in-windows-7/) <font size="1">alone with SAS/STAT 12.3, I first took a look at my favorite SAS statistical procedure, </font>[<font size="1">PROF FREQ</font>](http://support.sas.com/documentation/cdl/en/statug/66103/HTML/default/viewer.htm#statug_freq_toc.htm)<font size="1">.&#160; Last year I had a note on </font>[<font size="1">confidence intervals for binomial proportion based on SAS 9.2/SAS9.3</font>](http://www.jiangtanghu.com/blog/2012/09/15/confidence-intervals-binomial-proportion/)<font size="1">. Now it’s time to throw out some updates.</font>

###### 1. A new confidence limits method added, Wilson (Corrected) 

<font size="1">In my previous post, SAS PROC FREQ computed 6 of the 11 intervals (#1, 2, 3, 5, 8, 9; see my macros, <em><a href="https://raw.github.com/Jiangtang/Programming-SAS/master/CI_Single_Proportion.sas">CI_Single_Proportion.sas</a></em>). Since SAS 9.4/STAT 12.3, #4 added:</font>

> <font size="1" face="Courier New">data test; <br />input grp outcome $ count; <br />datalines; <br />1 f 81 <br />1 u 182 <br />;</font>
> 
> <font size="1" face="Courier New">ods select BinomialCLs; <br />proc freq data=test; <br />&#160;&#160;&#160; tables outcome / binomial (CL=ALL); <br />&#160;&#160;&#160; weight Count; <br />run;</font>
> 
> <font size="1"><font face="Courier New">ods select BinomialCLs; <br />proc freq data=test; <br />&#160;&#160;&#160; tables outcome / <font color="#ff0000">binomialc</font> (CL=ALL); <br />&#160;&#160;&#160; weight Count; <br />run;</font> <br /></font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="CI_9.4" border="0" alt="CI_9.4" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/08/CI_9.4_thumb.png" width="343" height="164" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/08/CI_9.4.png)[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="CI_c_9.4" border="0" alt="CI_c_9.4" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/08/CI_c_9.4_thumb.png" width="351" height="168" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/08/CI_c_9.4.png)

###### 2. The <font color="#ff0000">binomialc</font> option is no longer documented, but still works

<font size="1">In the above session, a <font color="#ff0000">binomialc</font> option was used to compute the intervals with a continuity correction(CC). Actually it still works </font>[<font size="1">in SAS 9.4/STAT 12.3 but without documentation</font>](http://support.sas.com/documentation/cdl/en/statug/66103/HTML/default/viewer.htm#statug_freq_syntax08.htm) <font size="1">(it’s in </font>[<font size="1">SAS 9.2</font>](http://support.sas.com/documentation/cdl/en/procstat/63104/HTML/default/viewer.htm#procstat_freq_sect010.htm) <font size="1">and </font>[<font size="1">SAS 9.3</font>](http://support.sas.com/documentation/cdl/en/statug/63962/HTML/default/viewer.htm#statug_freq_sect010.htm)<font size="1">). Instead, a <font color="#ff0000">CORRECT</font> options is used for continuity correction:</font>

> <font size="1" face="Courier New">ods select BinomialCLs; <br />proc freq data=test; <br />&#160;&#160;&#160; tables outcome / binomial (<font color="#ff0000">CORRECT</font> CL=ALL); <br />&#160;&#160;&#160; weight Count; <br />run;</font>

<font size="1">Also, you can use it this way to only compute intervals with CC:</font>

> <font size="1" face="Courier New">ods select BinomialCLs; <br />proc freq data=test; <br />&#160;&#160;&#160; tables outcome / binomial (CL=W(<font color="#ff0000">CORRECT</font>) WALD(<font color="#ff0000">CORRECT</font>)); <br />&#160;&#160;&#160; weight Count; <br />run;</font>