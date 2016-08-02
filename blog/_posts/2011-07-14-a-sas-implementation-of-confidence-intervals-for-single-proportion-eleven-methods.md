---
author: Jiangtang Hu
title: 'A SAS Implementation of Confidence Intervals for Single Proportion: Eleven Methods'
excerpt:
layout: post
category:
  - SAS
tags:
  - Confidence Interval
  - Newcombe
  - R
  - SAS
  - Single Proportion
post_format: [ ]
---
The following two papers by Professor [Robert Newcombe][1], in my limit observation, are the most frequently cited papers in the industry for CI calculation:

*   [**Two-sided confidence intervals for the single proportion: comparison of seven methods.**][2]    
    Newcombe RG, Stat Med , Volume 17 , 8 (April 1998) pp.857-**872****** 
*   [**Interval estimation for the difference between independent proportions: comparison of eleven methods.**][3]    
    Newcombe RG, Stat Med , Volume 17 , 8 (April 1998) pp.**873**-890 

This post serves as an implementation using SAS accompany with the first paper on confidence intervals for single proportion(method 1-7). Additional 4 methods also provided:

> 1.  Simple asymptotic, Without CC                          
> 2.  Simple asymptotic, With CC                             
> 3.  Score method, Without CC                               
> 4.  Score method, With CC                                  
> 5.  Binomial-based, ‘Exact’                                
> 6.  Binomial-based, Mid-p                                  
> 7.  Likelihood-based                                       
> 8.  Jeffreys                                               
> 9.  Agresti-Coull,z^2/2 successes                          
> 10. Agresti-Coull,2 successes and 2 fail                   
> 11. Logit 

The codes are available at

> [http://jiangtanghu.com/docs/en/CI\_Single\_Proportion.sas][4] 

It is a purely SAS/Base(data step and SQL) approach. I prefer data steps because it can be seamlessly incorporate into production work which looks like:

> /*r is the observed number of events/responders in n observations;*/ 
> 
> %macro _Wald(r,n,alpha=0.05); 
> 
>       p=&r/&n;   
>       z = probit (1-&alpha/2);   
>       sd=sqrt(&n\*p\*(1-p)); *Standard Deviation ;   
>       se=sd/&n;            *standard error;   
>       me=z*se;             *margin of error;   
>       p\_CI\_low = p-me;   
>       p\_CI\_up  = p+me;   
>      p\_CI=compress(catx("","[",put(round(p\_CI\_low,0.0001),6.4),",",put(round(p\_CI_up,0.0001),6.4),"]"));   
> %mend _Wald; 
> 
> data test;   
>       input r n;   
>      %_Wald(r,n);   
>       keep r n p p_CI;   
> datalines;   
> 81 263   
> 15 148   
> 0 20   
> 1 29   
> 29 29   
> ;     
> run; 
> 
> proc print data=test;run;

But when simulation required (in methods 6-7), some SQL clauses pop up. Admit that It makes the codes less elegant. In this situation, matrix operation language such as SAS/IML or R will do a better job.

Note that in SAS 9.2, PROC FREQ can produce the following five intervals(method 1, 3, 9 ,8, 5):

> Wald (also with method 2)                     
> Wilson                   
> Agresti-Coull            
> Jeffreys                 
> Clopper-Pearson (Exact)

For the five intervals in SAS 9.2, a good reference is *Confidence Intervals for the Binomial Proportion with Zero Frequency* by Xiaomin He and Shwu-Jen Wu:

> <www.pharmasug.org/download/papers/SP10.pdf>

Also, an equivalent R version of the eleven methods by Abteilung Kriminologie is also available at

> <http://www2.jura.uni-hamburg.de/instkrim/kriminologie/Mitarbeiter/Enzmann/Software/prop.CI.r>

Such R repository is also a good resource for SAS users. I almost “translate” R implementations directly to SAS for this post.

 [1]: http://medicine.cf.ac.uk/en/person/prof-robert-gordon-newcombe/
 [2]: http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?cmd=Retrieve&db=pubmed&dopt=Abstract&list_uids=9595616&query_hl=1
 [3]: http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?cmd=Retrieve&db=pubmed&dopt=Abstract&list_uids=9595617&query_hl=1
 [4]: http://jiangtanghu.com/docs/en/CI_Single_Proportion.sas