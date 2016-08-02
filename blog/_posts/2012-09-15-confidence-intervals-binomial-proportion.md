---
author: Jiangtang Hu
title: 'Statistical Notes (3): Confidence Intervals for Binomial Proportion Using SAS'
excerpt:
layout: post
category:
  - SAS
  - statistics
tags:
  - Binomial proportion inverval
  - Confidence Interval
  - PROC FREQ
  - R
  - SAS
  - statistics
post_format: [ ]
---
> A guy notices a bunch of targets scattered over a barn wall, and in the center of each, in the "bulls-eye," is a bullet hole. "Wow," he says to the farmer, "that’s pretty good shooting. How’d you do it?" "Oh," says the farmer, "it was easy. I painted the targets after I shot the holes." – An Old Joke

Last year I dumped piece of [SAS codes to compute confidence intervals][1] for single proportion using 11 methods including 7 presented by one of Prof. Newcombe‘s  most wildly cited papers, ***[Two-sided confidence intervals for the single proportion: comparison of seven methods][2]* **(r is the number of event in total cases of n):

[![Newcombe][4]][4]

To get such results using my macro, just submit the following SAS codes:

> filename CI url ‘[https://raw.github.com/Jiangtang/Programming-SAS/master/CI\_Single\_Proportion.sas’;][4]   
> %include CI;   
> %CI\_Single\_Proportion(r=81,n=263);

And the outputs(plus 4 additional methods):

[![Jiangtang][6]][6]

In SAS 9.2 and 9.3, 6 of the 11 intervals can be calculated by [PROC FREQ][6]. First, method 1, 3, 9 ,8, 5 via a *binomial* option: 

> data test;   
>     input grp outcome $ count;   
> datalines;   
> 1 f 81   
> 1 u 182   
> ;
> 
> ods select BinomialCLs;   
> proc freq data=test;   
>    tables outcome / binomial(all);   
>    weight Count;   
> run;

The outputs:

[![SASFreqCI][8]][8]

And you can get another Wald interval with a continuity correction (method 2) via *binomialC* option:

> ods select BinomialCLs;   
> proc freq data=test;   
>    tables outcome / binomialc(all);   
>    weight Count;   
> run;

get:

[![SASFreqCI_CC][9]][9]

# R Notes

These two R packages contain a bunch of CI calculations:

> [Binom][9]
> 
> [PropCIS][10] 

For SAS macro %CI\_Single\_Proportion, I borrowed a lot from this R implementation:

> <http://www2.jura.uni-hamburg.de/instkrim/kriminologie/Mitarbeiter/Enzmann/Software/prop.CI.r>

# Additional Notes

If interested, a nice paper on binomial intervals with ties, the paper *[Confidence intervals for a binomial proportionin the presence of ties][11]*,  and* [the program][12]*.

 [1]: http://www.jiangtanghu.com/blog/2011/07/14/a-sas-implementation-of-confidence-intervals-for-single-proportion-eleven-methods/
 [2]: http://www.ncbi.nlm.nih.gov/pubmed/9595616?dopt=Abstract
 []: http://dl.dropbox.com/u/69732603/Newcombe.png
 [4]: https://raw.github.com/Jiangtang/Programming-SAS/master/CI_Single_Proportion.sas';
 []: http://dl.dropbox.com/u/69732603/Jiangtang.png
 [6]: http://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/viewer.htm#statug_freq_syntax08.htm
 []: http://dl.dropbox.com/u/69732603/SASFreqCI.png
 []: http://dl.dropbox.com/u/69732603/SASFreqCI_CC.png
 [9]: http://cran.r-project.org/web/packages/binom/
 [10]: http://cran.r-project.org/web/packages/PropCIs/
 [11]: http://stats-www.open.ac.uk/TechnicalReports/BinTies1.pdf
 [12]: http://homepages.abdn.ac.uk/j.crawford/pages/dept/Binomial_Ties_CIs.htm