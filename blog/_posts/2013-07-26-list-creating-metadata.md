---
id: 1205
title: 'List Processing With SAS (2): List Creating II'
date: 2013-07-26T00:24:50+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1205
permalink: /2013/07/26/list-creating-metadata/
categories:
  - SAS
tags:
  - List
  - SAS
---
[<span style="font-size: xx-small;">%range</span>](http://www.jiangtanghu.com/blog/2013/07/11/sas-list-creating/) <span style="font-size: xx-small;">is a genetic list creator. To apply data driven programming technique, we need to fetch metadata from source data dynamically, for example, to get all variables from a input dataset.</span>

<span style="font-size: xx-small;">You can easily make it by</span>

<span style="font-size: xx-small;">1. PROC SQL, from </span> <span style="font-size: xx-small;">a SAS dictionary table, or macro variable by SELECT INTO; or</span>

<span style="font-size: xx-small;">2. Proc Contents; or</span>

<span style="font-size: xx-small;">3. even <a href="http://www.sascommunity.org/wiki/Tip_of_the_Day:July_21">a smart data step with RESOLVE function and with CALL SYMPUT</a>, like </span>

> <pre>%let namelist=;
data _null_;
	set sashelp.class;
	call symput('namelist', trim(resolve('&namelist'))||' '||trim(name));
run;
%put &namelist;</pre>

&nbsp;

<span style="font-size: xx-small;">In my <a href="https://github.com/Jiangtang/SAS_ListProcessing">repository</a>, there is a elegant function-like macro where SAS file processing functions like open(), close() are used, </span>[<span style="font-size: xx-small;">%getVar</span>](https://github.com/Jiangtang/SAS_ListProcessing/blob/master/getVar.sas)<span style="font-size: xx-small;">. Below follows examples to fetch variables from a dataset, based on variable type, numeric or character:</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">filename list url &#8220;</span>[<span style="font-family: 'Courier New'; font-size: xx-small;">https://raw.github.com/Jiangtang/SAS_ListProcessing/master/_ListProcessing&#8221;;</span>](https://raw.github.com/Jiangtang/SAS_ListProcessing/master/_ListProcessing";)<span style="font-family: 'Courier New'; font-size: xx-small;"></p> 
> 
> <p>
>   %inc list;</span>
> </p>
> 
> <p>
>   <span style="font-family: 'Courier New'; font-size: xx-small;">%put %getVar(%str(sashelp.class));</p> 
>   
>   <p>
>     %put %getVar(%str(sashelp.class),n); </span>
>   </p>
>   
>   <p>
>     %put %getVar(%str(sashelp.class),C);
>   </p></blockquote> 
>   
>   <p>
>     <span style="font-size: xx-small;">Outputs:</span>
>   </p>
>   
>   <blockquote>
>     <p>
>       <span style="font-size: xx-small;">Name Sex Age Height Weight</p> 
>       
>       <p>
>         Age Height Weight </span>
>       </p>
>       
>       <p>
>         Name Sex
>       </p>
>       
>       <p>
>         &nbsp;
>       </p></blockquote> 
>       
>       <p>
>         <span style="font-size: xx-small;">Another example to list all the elements from a directory using </span><a href="https://github.com/Jiangtang/SAS_ListProcessing/blob/master/dir.sas"><span style="font-size: xx-small;">%dir</span></a><span style="font-size: xx-small;"> by </span><a href="http://www.datasavantconsulting.com/roland/"><span style="font-size: xx-small;">Roland Rashleigh-Berry</span></a><span style="font-size: xx-small;">:</span>
>       </p>
>       
>       <blockquote>
>         <p>
>           <span style="font-family: 'Courier New'; font-size: xx-small;">%put %dir(d:\test);</span>
>         </p>
>       </blockquote>
>       
>       <p>
>         <span style="font-size: xx-small;">For more, check out the List Creating part of the portal:</span>
>       </p>
>       
>       <p>
>         <a href="https://github.com/Jiangtang/SAS_ListProcessing"><span style="font-size: xx-small;">https://github.com/Jiangtang/SAS_ListProcessing</span></a>
>       </p>