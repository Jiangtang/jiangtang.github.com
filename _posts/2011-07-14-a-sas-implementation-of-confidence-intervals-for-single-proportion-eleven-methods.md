---
id: 312
title: 'A SAS Implementation of Confidence Intervals for Single Proportion: Eleven Methods'
date: 2011-07-14T22:05:44+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/07/14/a-sas-implementation-of-confidence-intervals-for-single-proportion-eleven-methods/
permalink: /2011/07/14/a-sas-implementation-of-confidence-intervals-for-single-proportion-eleven-methods/
categories:
  - SAS
tags:
  - Confidence Interval
  - Newcombe
  - R
  - SAS
  - Single Proportion
---
<font size="1">The following two papers by Professor </font>[<font size="1">Robert Newcombe</font>](http://medicine.cf.ac.uk/en/person/prof-robert-gordon-newcombe/)<font size="1">, in my limit observation, are the most frequently cited papers in the industry for CI calculation:</font>

  * <cite><a href="http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?cmd=Retrieve&db=pubmed&dopt=Abstract&list_uids=9595616&query_hl=1"><strong><font size="1">Two-sided confidence intervals for the single proportion: comparison of seven methods.</font></strong></a><font size="1"> </font></cite>   
    <font size="1">Newcombe RG, <cite>Stat Med</cite> , Volume 17 , 8 (April 1998) pp.857-<strong>872</strong><strong></strong> </font>
  * <cite><a href="http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?cmd=Retrieve&db=pubmed&dopt=Abstract&list_uids=9595617&query_hl=1"><strong><font size="1">Interval estimation for the difference between independent proportions: comparison of eleven methods.</font></strong></a><font size="1"> </font></cite>   
    <font size="1">Newcombe RG, <cite>Stat Med</cite> , Volume 17 , 8 (April 1998) pp.<strong>873</strong>-890 </font>

<p style="margin-right: 0px">
  <font size="1">This post serves as an implementation using SAS accompany with the first paper on confidence intervals for single proportion(method 1-7). Additional 4 methods also provided:</font>
</p>

> <font size="1">1.&#160; Simple asymptotic, Without CC&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />2.&#160; Simple asymptotic, With CC&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />3.&#160; Score method, Without CC&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />4.&#160; Score method, With CC&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />5.&#160; Binomial-based, &#8216;Exact&#8217;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />6.&#160; Binomial-based, Mid-p&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />7.&#160; Likelihood-based&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />8.&#160; Jeffreys&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />9.&#160; Agresti-Coull,z^2/2 successes&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />10. Agresti-Coull,2 successes and 2 fail&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />11. Logit </font>

<p style="margin-right: 0px">
  <font size="1">The codes are available at</font>
</p>

> <p style="margin-right: 0px">
>   <a href="http://jiangtanghu.com/docs/en/CI_Single_Proportion.sas"><font size="1">http://jiangtanghu.com/docs/en/CI_Single_Proportion.sas</font></a><font size="1">&#160;</font>
> </p>

<p style="margin-right: 0px">
  <font size="1">It is a purely SAS/Base(data step and SQL) approach. I prefer data steps because it can be seamlessly incorporate into production work which looks like:</font>
</p>

> <font size="1" face="Courier New">/*r is the observed number of events/responders in n observations;*/ </font>
> 
> <font size="1" face="Courier New">%macro _Wald(r,n,alpha=0.05); </font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160;&#160;&#160; p=&r/&n; <br />&#160;&#160;&#160;&#160;&#160; z = probit (1-&alpha/2); <br />&#160;&#160;&#160;&#160;&#160; sd=sqrt(&n*p*(1-p)); *Standard Deviation ; <br />&#160;&#160;&#160;&#160;&#160; se=sd/&n;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; *standard error; <br />&#160;&#160;&#160;&#160;&#160; me=z*se;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; *margin of error; <br />&#160;&#160;&#160;&#160;&#160; p_CI_low = p-me; <br />&#160;&#160;&#160;&#160;&#160; p_CI_up&#160; = p+me; <br />&#160;&#160;&#160;&#160; p_CI=compress(catx("","[",put(round(p_CI_low,0.0001),6.4),",",put(round(p_CI_up,0.0001),6.4),"]")); <br />%mend _Wald; </font>
> 
> <font size="1" face="Courier New">data test; <br />&#160;&#160;&#160;&#160;&#160; input r n; <br />&#160;&#160;&#160;&#160; <font color="#ff0000">%_Wald(r,n);</font> <br />&#160;&#160;&#160;&#160;&#160; keep r n p p_CI; <br />datalines; <br />81 263 <br />15 148 <br />0 20 <br />1 29 <br />29 29 <br />;&#160;&#160; <br />run; </font>
> 
> <font size="1" face="Courier New">proc print data=test;run;</font>

<p style="margin-right: 0px">
  <font size="1">But when simulation required (in methods 6-7), some SQL clauses pop up. Admit that It makes the codes less elegant. In this situation, matrix operation language such as SAS/IML or R will do a better job.</font>
</p>

<p style="margin-right: 0px">
  <font size="1">Note that in SAS 9.2, PROC FREQ can produce the following five intervals(method 1, 3, 9 ,8, 5):</font>
</p>

> <font size="1">Wald (also with method 2)&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />Wilson&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />Agresti-Coull&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />Jeffreys&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />Clopper-Pearson (Exact)</font>

<p style="margin-right: 0px">
  <font size="1">For the five intervals in SAS 9.2, a good reference is <em>Confidence Intervals for the Binomial Proportion with Zero Frequency</em> by Xiaomin He and Shwu-Jen Wu:</font>
</p>

> <p style="margin-right: 0px">
>   <a href="www.pharmasug.org/download/papers/SP10.pdf" target="_blank"><font size="1">www.pharmasug.org/download/papers/SP10.pdf</font></a>
> </p>

<p style="margin-right: 0px">
  <font size="1">Also, an equivalent R version of the eleven methods by Abteilung Kriminologie is also available at</font>
</p>

> <p style="margin-right: 0px">
>   <a href="http://www2.jura.uni-hamburg.de/instkrim/kriminologie/Mitarbeiter/Enzmann/Software/prop.CI.r"><font size="1">http://www2.jura.uni-hamburg.de/instkrim/kriminologie/Mitarbeiter/Enzmann/Software/prop.CI.r</font></a>
> </p>

<font size="1">Such R repository is also a good resource for SAS users. I almost “translate” R implementations directly to SAS for this post.</font>

<font size="1"></font>