---
author: Jiangtang Hu
title: 'A SAS 9.3 Macro Trick: %put &amp;=var'
excerpt:
layout: post
category:
  - SAS
tags:
  - Macro
  - SAS
post_format: [ ]
---
This is new since SAS 9.3 on how to display macro variable name and its value. Try to run

> %let var=1,2,3;   
> %put &=var;

or

> %macro test(var);   
>     %put &=var;   
> %mend;   
> %test(%str(1,2,3))

and you will get in Log window

> VAR=1,2,3

You can read from [SAS 9.3 online doc][1]:

> If you place an equal sign between the ampersand and the macro variable name of a direct macro variable reference, the macro variable’s name displays in the log along with the macro variable’s value.

In SAS 9.2 and prior, you should type the macro variable twice:

> %let var=1,2,3;   
> %put var=&var;

PS: it is called a “Tip” in [SAS 9.3 online doc][1], but I’d rather call it a trick: not critical but nice to have (*save your typing!*). You may be also interested in [Rick Wicklin’s differentiation on Tip and Technique][2].

 [1]: http://support.sas.com/documentation/cdl/en/mcrolref/62978/HTML/default/viewer.htm#n189qvy83pmkt6n1bq2mmwtyb4oe.htm
 [2]: http://blogs.sas.com/content/iml/2010/11/01/tips-and-techniques-whats-the-difference/