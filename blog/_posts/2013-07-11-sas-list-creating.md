---
id: 1199
title: 'List Processing With SAS (1): List Creating I'
date: 2013-07-11T21:10:14+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1199
permalink: /2013/07/11/sas-list-creating/
categories:
  - SAS
tags:
  - List
  - Macro
  - SAS
---
Suppose you have 10 datasets, literally ds1, ds2, …ds10 and you need to concatenate them all. You may first get a quick shortcut **<font color="#ff0000">set ds1-ds10</font>**. If such list members were generated dynamically (and may hold a form like ds1a, ds2a,… ds10a) , you will probably come out a macro solution:

> <font face="Courier New">&#160;&#160; %macro doit; <br />&#160;&#160;&#160;&#160;&#160;&#160; data combine; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; set <font color="#ff0000">%do i=1 %to &n; ds&i %end;</font> ; <br />&#160;&#160;&#160;&#160;&#160;&#160; run; <br />&#160;&#160; %mend; <br />&#160;&#160; %doit</font>

where we conduct the list series in a %do loop. Also, suppose we need to fill out a list of datasets in a FROM clause of a SQL procedure. You can not copy the %do loop above because all elements should be separated by a comma. I [once wrote a recursive macro to produce such list](http://www.jiangtanghu.com/blog/2013/03/31/list-processing-with-sas-a-github-repository/):

> <font face="Courier New">%macro _list(n,pre=ds); <br />&#160;&#160;&#160; %if &n=1 %then &pre.1; <br />&#160;&#160;&#160;&#160; %else %_list(%eval(&n-1)),&pre.&n; <br />%mend _list;</font>
> 
> <font face="Courier New">%put %_list(10);</font> 

The question is, how can we produce such list of values at a universal form? I put all my collected SAS list processing utilities (macro like functions) at Github:

> <https://github.com/Jiangtang/SAS_ListProcessing/>

and we can begin with macro [%range](https://github.com/Jiangtang/SAS_ListProcessing/blob/master/range.sas) by Ian Whitlock and Chang Chung:

> <font face="Courier New">filename list url&#160; "</font>[<font face="Courier New">https://raw.github.com/Jiangtang/SAS_ListProcessing/master/_ListProcessing";</font>](https://raw.github.com/Jiangtang/SAS_ListProcessing/master/_ListProcessing";)   
> <font face="Courier New">%inc list;</font>
> 
> <font face="Courier New">%put %range(to=10); <br />%put %range(to=10, opre=%str(ds)); <br />%put %range(to=10, opre=%str(ds),osuf=%str(a)); <br />%put %range(from=2,to=10,step=3,osep=%str(,)); <br />%put %range(from=2,to=10,step=3,osep=%str(,),osuf=%str(ds));</font>
> 
> <font face="Courier New"></font>

The outputs:

> 1 2 3 4 5 6 7 8 9 10   
> ds1 ds2 ds3 ds4 ds5 ds6 ds7 ds8 ds9 ds10   
> ds1a ds2a ds3a ds4a ds5a ds6a ds7a ds8a ds9a ds10a   
> 2,5,8   
> 2ds,5ds,8ds 

[%range](https://github.com/Jiangtang/SAS_ListProcessing/blob/master/range.sas) is a very versatile macro like function which accepts lower and upper bounds, increments, separated symbol, prefix and suffix as parameters to create bunch of lists. 

##### Note:

To create a non-integer list, use [%range\_non\_int](https://github.com/Jiangtang/SAS_ListProcessing/blob/master/range_non_int.sas):

> <font face="Courier New">%put %range_non_int(start = 1 , end = 2 , by = .25 ) ;</font>

and you get

> 1 1.25 1.5 1.75 2