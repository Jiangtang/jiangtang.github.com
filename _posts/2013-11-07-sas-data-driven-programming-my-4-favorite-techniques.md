---
id: 1279
title: 'SAS Data Driven Programming: My 4 Favorite Techniques'
date: 2013-11-07T10:10:21+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1279
permalink: /2013/11/07/sas-data-driven-programming-my-4-favorite-techniques/
categories:
  - SAS
tags:
  - Call Execute
  - Foreach
  - List
  - Macro
  - macro array
  - SAS
---
<font size="1">I use relatively fixed patterns in my SAS&#160; programming life. For so called data driven programming (or dynamic programming), I used the following 4 techniques, chronologically:</font>

  * <font size="1">macro array </font>
  * <font size="1">call execute </font>
  * <font size="1">list processing </font>
  * <font size="1">for each loop </font>

<font size="1">For a quick demo, I will start with a simple scenario in which the data set sashelp.zipcode should be spitted to pieces of datasets by states (in real projects, the codes would be more complicated but share the simple atom structure). For example, the dataset for North Carolina:</font>

> <font size="1" face="Courier New">data zipcode_NC; <br />&#160;&#160;&#160; set sashelp.zipcode(where=(statecode="NC")); <br />run;</font>

<font size="1">There are 50 states plus territories like Puerto Rico in the source data, so you won’t just use a simple string replacement by macro variable. My first SAS dynamic programming technique is using macro array, learned from Chapter 6 of <em>Carpenter&#8217;s Complete Guide to the SAS Macro Language</em>:</font>

##### 1. Macro array

> <font size="1" face="Courier New">proc sort data=sashelp.zipcode (keep=statecode) nodupkey out=statecode; <br />&#160;&#160;&#160; by statecode; <br />run;</font>
> 
> <font size="1" face="Courier New">data _null_; <br />&#160;&#160;&#160; set statecode end=eof; <br />&#160;&#160;&#160; i+1; <br />&#160;&#160;&#160; II=left(put(i,2.)); <br />&#160;&#160;&#160; call symputx(&#8216;statecode&#8217;||II,statecode); <br />&#160;&#160;&#160; if eof then call symputx(&#8216;n&#8217;,II); <br />run;</font>
> 
> <font size="1" face="Courier New">%macro doit; <br />%do i=1 %to &n; <br />&#160;&#160;&#160; data class_&&statecode&i; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; set sashelp.zipcode(where=(statecode="&&statecode&i")); <br />&#160;&#160;&#160; run; <br />%end; <br />%mend; <br />%doit</font>
> 
> <font size="1"></font>

<font size="1">Macro array is still my favorite and I use it everywhere. It creates multiple macros variables by sequence (macro array) from the control file, then apply a do loop over each macro variable to get job done: straightforward while robust(verbose somehow).</font>

##### 2. Call Execute

<font size="1">Call Execute is a power tool. It will make your codes much concise and efficient. I love it but with little bit of reluctance: regardless the potential timing issue, for me, it is not aesthetically readable in most cases. To make a relatively enjoyable Call Execute, I prefer to enclose the atom part of the program to a macro then use a single Call Execute to resolve it:</font>

> <font size="1" face="Courier New">%macro break(statecode); <br />&#160;&#160; data class_&statecode; <br />&#160;&#160;&#160;&#160;&#160; set sashelp.zipcode(where=(statecode="&statecode")); <br />&#160;&#160; run; <br />%mend;</font>
> 
> <font size="1" face="Courier New">data _null_; <br />&#160; set statecode; <br />&#160; call execute(&#8216;%break(&#8216;||trim(statecode)||&#8217;)&#8217;); <br />run;</font>

<font size="1">Heavily interacting with data step will just make Call Execute like black magic (this snippet comes from Mike Molter’s 2013 paper, <em><a href="http://www.lexjansen.com/pharmasug/2013/BB/PharmaSUG-2013-BB08.pdf">Coding For the Long Haul With Managed Metadata and Process Parameters</a></em>; sorry Mike, I know it works):</font>

> <font size="1" face="Courier New">data _null_ ; <br /> length lastds $4 ; <br /> set meta2 end=thatsit ; <br /> if _n_ eq 1 then do; <br />&#160;&#160;&#160;&#160; call execute (&#8216;proc sql; &#8216;) ; <br />&#160;&#160;&#160;&#160; lastds=&#8217;ae&#8217;; <br /> end; <br /> retain lastds ; <br />&#160; <br /></font><font size="1"><font face="Courier New"><font color="#ff0000"> call execute (&#8216;create table &#8216;||data set||&#8217; as select a.*,&#8217;||left(keepvars)||&#8217; from <br />&#8216;||lastds a left join suppae_tran(where=(idvar eq "&#8217;||compress(idvar)||&#8217;")) b on <br />a.usubjid=b.usubjid and a.&#8217;||compress(idvar)||&#8217;=&#8217;||left(joincond)||&#8217;;&#8217;);</font> <br />&#160; <br /> if thatsit then call execute(&#8216; quit; &#8216;) ; <br /> lastds=data set ; <br />run;</font> <br /></font>

<font size="1">Well there are always trade-offs. Separating Call Execute with data steps (my preference) will make it much more readable, but it is not cool anymore(compared to Mike’s style)! Coolness deserves the efforts and I know it’s part of programmers proud.</font>

##### 3. List Processing

<font size="1">I started to use list in SAS since 2011 and now I have a big collection:</font>

> [<font size="1">https://github.com/Jiangtang/SAS_ListProcessing</font>](https://github.com/Jiangtang/SAS_ListProcessing)

<font size="1">Macro array approach will create series of macro variables, while in list method, a single macro variable will be generated which hold series of values:</font>

> <font size="1" face="Courier New">proc sql noprint; <br />&#160;&#160;&#160; select statecode into:statecode separated by " " <br />&#160;&#160;&#160; from statecode <br />&#160;&#160;&#160; ; <br />quit;</font>
> 
> <font size="1" face="Courier New">%macro doit; <br />%do i=1 %to %sysfunc(countw(&statecode)); <br />&#160;&#160;&#160; %let a=%sysfunc(scan(&statecode,&i,&#8217; &#8216;)); <br />&#160;&#160;&#160; data class_&a; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; set sashelp.zipcode(where=(statecode="&a")); <br />&#160;&#160;&#160; run; <br />%end; <br />%mend; <br />%doit</font>

##### 4. For each

<font size="1">A foreach operation is dream for SAS programmers. Now I have one, for.sas by Jim Anderson:</font>

> <font size="1" face="Courier New">filename list url "</font>[<font size="1" face="Courier New">https://raw.github.com/Jiangtang/SAS_ListProcessing/master/_ListProcessing";</font>](https://raw.github.com/Jiangtang/SAS_ListProcessing/master/_ListProcessing";)        <font size="1" face="Courier New"><br />%inc list;</font>
> 
> <font size="1"><font face="Courier New">data %for(statecode, in=[statecode], do=%nrstr(class_&statecode(where=(statecode="&statecode")))); <br />&#160;&#160;&#160; set sashelp.zipcode; <br />run;</font> <br /></font>

<font size="1">Actually this %for is much more versatile than it appears in this simple demo. It can proceeds sequentially against SAS datasets, value list, number range, along with dataset contents and directory contents. Check it out and you will definitely love it:</font>

> [<font size="1">http://www.sascommunity.org/wiki/Streamlining_Data-Driven_SAS_With_The_%25FOR_Macro</font>](http://www.sascommunity.org/wiki/Streamlining_Data-Driven_SAS_With_The_%25FOR_Macro "http://www.sascommunity.org/wiki/Streamlining_Data-Driven_SAS_With_The_%25FOR_Macro")