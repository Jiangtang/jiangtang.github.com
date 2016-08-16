---
id: 673
title: 'Statistical Notes (3): Confidence Intervals for Binomial Proportion Using SAS'
date: 2012-09-15T00:13:03+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=673
permalink: /2012/09/15/confidence-intervals-binomial-proportion/
categories:
  - SAS
  - statistics
tags:
  - Binomial proportion inverval
  - Confidence Interval
  - PROC FREQ
  - R
  - SAS
  - statistics
---
> <span style="font-size: xx-small;">A guy notices a bunch of targets scattered over a barn wall, and in the center of each, in the &#8220;bulls-eye,&#8221; is a bullet hole. &#8220;Wow,&#8221; he says to the farmer, &#8220;that&#8217;s pretty good shooting. How&#8217;d you do it?&#8221; &#8220;Oh,&#8221; says the farmer, &#8220;it was easy. I painted the targets after I shot the holes.&#8221; – An Old Joke</span>

<span style="font-size: xx-small;">Last year I dumped piece of </span><a href="http://www.jiangtanghu.com/blog/2011/07/14/a-sas-implementation-of-confidence-intervals-for-single-proportion-eleven-methods/" target="_blank"><span style="font-size: xx-small;">SAS codes to compute confidence intervals</span></a> <span style="font-size: xx-small;">for single proportion using 11 methods including 7 presented by one of Prof. Newcombe‘s  most wildly cited papers, <strong><em><a href="http://www.ncbi.nlm.nih.gov/pubmed/9595616?dopt=Abstract" target="_blank">Two-sided confidence intervals for the single proportion: comparison of seven methods</a></em> </strong>(r is the number of event in total cases of n):</span>

<p style="text-align: center;">
  <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/newcombe1.png" target="_blank"><img class="size-medium wp-image-1220 aligncenter" style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border: 0px;" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/newcombe1-240x300.png" alt="newcombe" width="240" height="300" border="0" srcset="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/newcombe1-240x300.png 240w, http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/newcombe1.png 300w" sizes="(max-width: 240px) 100vw, 240px" /></a>
</p>

<span style="font-size: xx-small;">To get such results using my macro, just submit the following SAS codes:</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">filename CI url &#8216;</span>[<span style="font-family: 'Courier New'; font-size: xx-small;">https://raw.github.com/Jiangtang/Programming-SAS/master/CI_Single_Proportion.sas&#8217;;</span>](https://raw.github.com/Jiangtang/Programming-SAS/master/CI_Single_Proportion.sas)<span style="font-size: xx-small;"><br /> </span><span style="font-family: 'Courier New'; font-size: xx-small;">%include CI;<br /> %CI_Single_Proportion(<span style="color: #ff0000;">r=81,n=263</span>);</span>

<span style="font-size: xx-small;">And the outputs(plus 4 additional methods):</span>

[<span style="font-size: xx-small;"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="Jiangtang" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/Jiangtang_thumb.png" alt="Jiangtang" width="490" height="303" border="0" /></span>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/Jiangtang.png)

<span style="font-size: xx-small;">In SAS 9.2 and 9.3, 6 of the 11 intervals can be calculated by </span><a href="http://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/viewer.htm#statug_freq_syntax08.htm" target="_blank"><span style="font-size: xx-small;">PROC FREQ</span></a><span style="font-size: xx-small;">. First, method 1, 3, 9 ,8, 5 via a <em>binomial</em> option: </span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">data test;<br /> input grp outcome $ count;<br /> datalines;<br /> 1 f 81<br /> 1 u 182<br /> ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">ods select BinomialCLs;<br /> proc freq data=test;<br /> tables outcome / binomial(all);<br /> weight Count;<br /> run;</span>

<span style="font-size: xx-small;">The outputs:</span>

[<span style="font-size: xx-small;"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="SASFreqCI" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/SASFreqCI_thumb.png" alt="SASFreqCI" width="461" height="223" border="0" /></span>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/SASFreqCI.png)

<span style="font-size: xx-small;">And you can get another Wald interval with a continuity correction (method 2) via <em>binomialC</em> option:</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">ods select BinomialCLs;<br /> proc freq data=test;<br /> tables outcome / <span style="color: #ff0000;">binomialc</span>(all);<br /> weight Count;<br /> run;</span>

<span style="font-size: xx-small;">get:</span>

[<span style="font-size: xx-small;"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="SASFreqCI_CC" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/SASFreqCI_CC_thumb.png" alt="SASFreqCI_CC" width="417" height="240" border="0" /></span>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/SASFreqCI_CC.png)

# <span style="font-weight: bold;">R Notes</span>

<span style="font-size: xx-small;">These two R packages contain a bunch of CI calculations:</span>

> <a href="http://cran.r-project.org/web/packages/binom/" target="_blank"><span style="font-size: xx-small;">Binom</span></a>
> 
> <a href="http://cran.r-project.org/web/packages/PropCIs/" target="_blank"><span style="font-size: xx-small;">PropCIS</span></a>

<span style="font-size: xx-small;">For SAS macro %CI_Single_Proportion, I borrowed a lot from this R implementation:</span>

> [<span style="font-size: xx-small;">http://www2.jura.uni-hamburg.de/instkrim/kriminologie/Mitarbeiter/Enzmann/Software/prop.CI.r</span>](http://www2.jura.uni-hamburg.de/instkrim/kriminologie/Mitarbeiter/Enzmann/Software/prop.CI.r)

# <span style="font-weight: bold;">Additional Notes</span>

<span style="font-size: xx-small;">If interested, a nice paper on binomial intervals with ties, the paper <em><a href="http://stats-www.open.ac.uk/TechnicalReports/BinTies1.pdf" target="_blank">Confidence intervals for a binomial proportionin the presence of ties</a></em>,  and<em> <a href="http://homepages.abdn.ac.uk/j.crawford/pages/dept/Binomial_Ties_CIs.htm" target="_blank">the program</a></em>. </span>