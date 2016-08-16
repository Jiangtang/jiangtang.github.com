---
id: 1361
title: 'List Manipulations Made Easy (and little bit of UGLY): the New DOSUBL Function'
date: 2015-03-09T15:07:54+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1361
permalink: /2015/03/09/list-manipulations-made-easy-and-little-bit-of-ugly-the-new-dosubl-function/
categories:
  - SAS
tags:
  - SAS
---
<font size="1">Typically, </font>[<font size="1">SAS list manipulations</font>](http://www.jiangtanghu.com/blog/2013/03/31/list-processing-with-sas-a-github-repository/) <font size="1">needs bunch of SAS I/O functions which are not necessarily well known to all SAS programmers. The new </font>[<font size="1">DOSUBL</font>](http://support.sas.com/documentation/cdl/en/lefunctionsref/67398/HTML/default/viewer.htm#p09dcftd1xxg1kn1brnjyc0q93yk.htm) <font size="1">function makes this technique much more easier and little bit of ugly I must admit:</font>

> <font size="1" face="Courier New">%MACRO ExpandVarList(data=_LAST_, var=_ALL_); <br />&#160;&#160;&#160; %if %upcase(%superq(data)) = _LAST_ <br />&#160;&#160;&#160; %then %let data = &SYSLAST; <br />&#160;&#160;&#160; %let rc = %sysfunc(dosubl(%str( <br />&#160;&#160;&#160; proc transpose data=&DATA(obs=0) out=ExpandVarList_temp; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; var &VAR; <br />&#160;&#160;&#160; run; <br />&#160;&#160;&#160; proc sql noprint; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; select _name_ into :temp_varnames separated by &#8216; &#8216; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; from ExpandVarList_temp <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; ; <br />&#160;&#160;&#160; drop table ExpandVarList_temp; <br />&#160;&#160;&#160; quit <br />&#160;&#160;&#160; ))); <br />&#160;&#160;&#160; &temp_varnames <br />%MEND ExpandVarList;</font>
> 
> <font size="1" face="Courier New">%put %ExpandVarList(data=sashelp.class);</font>

<font size="1">This piece of code comes from <em><a href="https://support.sas.com/resources/papers/proceedings13/032-2013.pdf">Submitting SAS Code On The Side</a></em> by Rick Langston. It’s not elegant by any means compared to </font>[<font size="1">this version</font>](https://github.com/Jiangtang/SAS_ListProcessing/blob/master/getVar.sas)<font size="1">, but does have huge advantage of utilizing traditional SAS programming elements like data steps, procedures and such.</font>

<font size="1">&#8212;&#8212;&#8212;&#8212;UPDATE 2015-03-16&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;</font>

<font size="1">Ronan Martorell, a SAS programmer from Paris, came out other two methods for the task above, also leveraged by DOSUBL (<em>the sky is not limited!</em>). The followings are his piece of codes (with permissions; Thank you Ronan!):</font>

> <font size="1">&#160;<font face="Courier New">/* <font color="#ff0000">&#8212; Method no. 2 :using a Data Step + Array launched by DOSUBL&#8211;</font> */ <br />%macro VarList(data=); <br />&#160;&#160;&#160; %local varlist;</font></font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160; /* DOSUBL required for executing the Data Step in a distinct session */ <br />&#160;&#160;&#160; %let rc = %sysfunc(dosubl(%str( <br />&#160;&#160;&#160; Data _null_; <br />&#160;&#160;&#160; length varlist $32167.; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; set &data(obs=1); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; array avarn[*] _NUMERIC_; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; array avarc[*] _CHARACTER_; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; do i=1 to dim(avarn); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; varlist=CATX(&#8216; &#8216;,varlist, vname(avarn[i])); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; end; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; do i=1 to dim(avarc); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; *no self-reference allowed!; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; if vname(avarc[i]) NE &#8216;varlist&#8217; then <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; varlist=CATX(&#8216; &#8216;,varlist, vname(avarc[i])); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; end; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; call symputx(&#8216;varlist&#8217;,varlist); <br />&#160;&#160;&#160; run; <br />&#160;&#160;&#160; ))); <br />&#160;&#160;&#160; <br />&#160;&#160;&#160; &varlist <br />%mend VarList; <br />%put %VarList(data=sashelp.class);</font>
> 
> <font size="1" face="Courier New">/* <font color="#ff0000">&#8212; Method no. 3:&#160; using Dictionary View COLUMNS launched by DOSUBL</font> &#8211;*/ <br />%macro VarlistDIC(data=); <br />&#160;&#160;&#160; %local libname memname varlist;</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160; /* Test : if . separator exists in DataSet name then extracts Libname & Memname strings accordingly */ <br />&#160;&#160;&#160; %let libname=%UPCASE( %sysfunc( IFC( %index(&data, .) EQ 0, WORK, %scan(&data, <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; 1) ))); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; %let memname=%UPCASE( %sysfunc( IFC( %index(&data, .) EQ 0, &data, <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; %scan(&data, 2) ))); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; %let rc = %sysfunc(dosubl(%str( </font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160; proc sql noprint; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; select name into :varlist separated by &#8216; &#8216; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; from DICTIONARY.COLUMNS <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; where libname EQ "&libname" and memname EQ "&memname" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; ; <br />&#160;&#160;&#160; quit; <br />&#160;&#160;&#160; )));</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160; &varlist <br />%mend VarlistDIC; <br />%put %VarListDIC(data=sashelp.class);</font>

<font size="1">Ronan also kindly contributed his I/O version (check out <a href="https://github.com/Jiangtang/SAS_ListProcessing/blob/master/getVar.sas">another I/O version in my github page</a>):</font>

> <font size="1" face="Courier New">/* <font color="#ff0000">&#8212; Method no. 4 : using SCL function with iterative FETCHOB + DICTIONARY VIEW &#8212;</font> */ <br />%macro ListVar(libname=, memname=); <br />&#160;&#160;&#160; /* local var initialisation */ <br />&#160;&#160;&#160; %let listvar=; <br />&#160;&#160;&#160; %let i=0;&#160;&#160;&#160;&#160;&#160;&#160; <br />&#160;&#160;&#160; /* open dictionary view with WHERE clause*/ <br />&#160;&#160;&#160; %let id=%sysfunc(open(sashelp.vcolumn (where=( libname = "%upcase(&libname)" AND memname= "%upcase(&memname)")))); <br />&#160;&#160;&#160; /* load variable names into macro-variables (beware macro var collision !) */ <br />&#160;&#160;&#160; /* Cf. </font>[<font size="1" face="Courier New">http://www.notecolon.info/2013/01/note-open-function-reading-data-sets-in.html</font>](http://www.notecolon.info/2013/01/note-open-function-reading-data-sets-in.html) <font size="1" face="Courier New">*/ <br />&#160;&#160;&#160; %syscall set(id); <br />&#160;&#160;&#160; %let rc=0; <br />&#160;&#160;&#160; /* loop into each line and accumulate the variable names into a list*/ <br />&#160;&#160;&#160; %do %until(&rc LT 0); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; %let i=&i+1; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; %let rc=%sysfunc(fetchobs(&id, &i));</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; /* force loop exit once last variable has been stored into the list */ <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; %let listvar= %sysfunc( IFC ( &rc GE 0, &listvar &Name, &listvar )); <br />&#160;&#160;&#160; %end; <br />&#160;&#160;&#160; %let id=%sysfunc(close(&id));</font>
> 
> <font size="1" face="Courier New">&#160;&#160; /* expands the list */ <br />&#160; &listvar <br />%mend; <br />%put %ListVar(libname=sashelp, memname=class);</font>