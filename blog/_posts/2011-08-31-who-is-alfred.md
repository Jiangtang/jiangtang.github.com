---
author: Jiangtang Hu
title: Who is Alfred?
excerpt:
layout: post
category:
  - Database
  - misc
  - SAS
tags:
  - class
  - Iris
  - Oracle
  - SAS
post_format: [ ]
---
> Tell me something about Alfred, male or female? age? height and weight? 

Oracle database (version 9 and below) had a well known default demo account SCOTT with a password, TIGER (and TIGER was the name of the real person Bruce Scott ’s cat, [see][1]) and in this account, there are some tables named DEPT, EMP, BONUS and SALGRADE (you can read their meaning). Almost every Oracle DBA learn SQL using these database and an joke just says that in DBA’s meetings, people just  warm up saying “how about Smith?” And you should know that in the database, Smith is a clerk and his boss is Ford (whose boss is Jones)!

In the beginning I also raise a question for SAS programmers: who is Alfred? Don’t give quick answer such that “Alfred who”. Actually, you should already go through with Alfred very well as a SAS programmer:

> proc print data=sashelp.class;   
>     where name="Alfred";   
> run;

As a clinical SAS programmer, I play with data, get acquaintance with the data and subjects and then subjects are no longer “subject”. They have identities and  Alfred is a 14 years old boy. I have such habit mostly because in clinical world, data are very expensive (not like the massive transaction data in financial industry) and should be took more care. 

I dare say that “class” is the most famous SAS dataset in sashelp library and then in the SAS world. The first dataset used for demo is almost this “class”. I just did a quick Google search, “[sas sashelp.class][2]” returns about 44,400 results. Hope you can find any other SAS datasets to beat it.

Alfred in “class” pops into my mind because today, I do find a strong candidate. In SAS 9.2 (and 9.3), the sashelp library has a new member, Iris. YES, it is the “[Fisher Iris Flower Data][3]”, which can be safely considered the most famous and most  used dataset in machine learning and data mining papers and statistical applications. Currently it has [only 859 hits in Google][4], I think the number will reach high accompany with the wide use of SAS 9.2 and above, and to enforce my prediction, I will definitely play with the Iris data in the following future!

 [1]: http://www.dba-oracle.com/t_scott_tiger.htm
 [2]: http://www.google.com/search?hl=en&source=hp&biw=1111&bih=561&q=sas+sashelp.class&btnG=Google+Search&aq=f&aqi=g10&aql=&oq=&gs_rfai=#pq=+sas+sashelp.class&hl=en&cp=0&gs_id=t&xhr=t&q=sas+sashelp.class&qe=c2FzIHNhc2hlbHAuY2xhc3M&qesig=-1hRQj8XDofruHqJt-7o1Q&pkc=AFgZ2tkn99yjg_kNxO238PUOVve2MCFJUcgPCK-pXmvfyldpJvG0DchYcRuz_Azx9jhciBgWit8jDgrY6zs4T42InGlJtSBhGQ&pf=p&sclient=psy&source=hp&pbx=1&oq=sas+sashelp.class&aq=f&aqi=&aql=&gs_sm=&gs_upl=&bav=on.2,or.r_gc.r_pw.r_cp.&fp=265f5e3edf2ec82b&biw=1166&bih=665&bs=1
 [3]: http://en.wikipedia.org/wiki/Iris_flower_data_set
 [4]: http://www.google.com/search?hl=en&source=hp&biw=1111&bih=561&q=sas+sashelp.class&btnG=Google+Search&aq=f&aqi=g10&aql=&oq=&gs_rfai=#sclient=psy&hl=en&source=hp&q=sas+sashelp.iris+&pbx=1&oq=sas+sashelp.iris+&aq=f&aqi=&aql=&gs_sm=e&gs_upl=277383l277383l5l277945l1l1l0l0l0l0l0l0ll0l0&bav=on.2,or.r_gc.r_pw.r_cp.&fp=265f5e3edf2ec82b&biw=1166&bih=665