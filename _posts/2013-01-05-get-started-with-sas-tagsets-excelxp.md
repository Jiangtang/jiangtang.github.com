---
id: 1096
title: Get Started with SAS Tagsets.ExcelXP
date: 2013-01-05T17:46:24+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1096
permalink: /2013/01/05/get-started-with-sas-tagsets-excelxp/
categories:
  - SAS
tags:
  - Excel
  - ExcelXP
  - ODS
  - ODS Markup
  - ODS Tagsets
  - ODS template
  - SAS
---
<font size="1">Hate it or not (<em>Yes I do</em>), SAS programmers can’t just get rid of Microsoft Office Excel in their life.</font>

<font size="1">Now my turn (with Tagsets.ExcelXP, I can at least get rid of DDE)…</font>

# 0. SAS Templates window [<img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="ODSTEMPLATES" border="0" alt="ODSTEMPLATES" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/ODSTEMPLATES_thumb.png" width="470" height="296" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/ODSTEMPLATES.png)

<font size="1">A visual way to browse all ODS templates is to use windows command “ODSTEMPLATES” to invoke a SAS template window.</font>

# 1.&#160; Check the current ExcelXP tagset version

> <p align="left">
>   <font size="1"><font face="Courier New">filename temp temp; <br />ods tagsets.ExcelXP file=temp options(doc=&#8217;help&#8217;); <br />ods tagsets.ExcelXP close;</font> </font>
> </p>

<font size="1">Scroll down the Log window to the end and you get something like:</font>

> <font size="1">NOTE: This is the Excel XP tagset (Compatible with SAS 9.1.3 and above, <font color="#ff0000">v1.122</font>, 01/04/2011). </font>

# 2. Get the source codes of current ExcelXP tagset and library it’s stored

> <font size="1" face="Courier New">proc template; <br />&#160;&#160;&#160; source Tagsets.ExcelXP; <br />run;</font>

<font size="1">The Log window shows the template codes:</font>

> <font size="1">15&#160;&#160; proc template; <br />16&#160;&#160;&#160;&#160;&#160;&#160; source Tagsets.ExcelXP; <br />define tagset Tagsets.ExcelXP; <br />&#160;&#160; parent = Tagsets.ExcelBase; <br />end; <br />NOTE: Path &#8216;Tagsets.ExcelXP&#8217; is in: <font color="#ff0000">SASHELP.TMPLMST</font>. </font>

<font size="1">Note Tagsets.ExcelXP is subject to Tagsets.ExcelBase.</font>

<font size="1">The template store path uses a two level name in which SASHELP is a SAS library and TMPLMST, a name assigned to distinguish a set of templates. You can also store your customized templates in SASHELP.mytpl1, WORK.forTLF and such.</font>

<font size="1">If want a the source codes in a separated file rather than in Log window, try</font>

> <font size="1" face="Courier New">proc template;</font>
> 
> <font size="1" face="Courier New">source Tagsets.ExcelXP/<font color="#ff0000">file="a:\test\ExcelXP.tpl"</font>; <br />run;</font>

<font size="1">The extension doesn’t matter and you can use anything you like (including .SAS).</font>

# 3. List all ODS template store path

> <font size="1" face="Courier New">ods path show;</font>

<font size="1">Log:</font>

> <font size="1">Current ODS PATH list is:</font>
> 
> <font size="1">1. SASUSER.TEMPLAT(UPDATE) <br />2. SASHELP.TMPLMST(READ)</font>

<font size="1">This order also indicates the ODS template searching priority, first SASUSER.TEMPLAT then SASHELP.TMPLMST. If two templates with same name exist in both library, the one in SASUSER.TEMPLAT will be used.</font>

<font size="1">Templates in SASHELP.TMPLMST can’t be modified(read only).</font>

# 4. Install latest version in SASUSER library

<font size="1">The last version of ExcelXP tagset is v1.127 by far according to SAS ODS MARKUP portal:</font>

  * [<font size="1">http://support.sas.com/rnd/base/ods/odsmarkup/</font>](http://support.sas.com/rnd/base/ods/odsmarkup/ "http://support.sas.com/rnd/base/ods/odsmarkup/") 

> <font size="1" face="Courier New">filename excltags url &#8216;</font>[<font size="1" face="Courier New">http://support.sas.com/rnd/base/ods/odsmarkup/excltags.tpl&#8217;;</font>](http://support.sas.com/rnd/base/ods/odsmarkup/excltags.tpl';)        <font size="1" face="Courier New"><br />%include excltags;</font>

<font size="1">log:</font>

> <font size="1">NOTE: TAGSET &#8216;Tagsets.ExcelBase&#8217; has been saved to: SASUSER.TEMPLAT <br />NOTE: Overwriting existing template/link: Tagsets.Config_debug <br />NOTE: TAGSET &#8216;Tagsets.Config_debug&#8217; has been saved to: SASUSER.TEMPLAT <br /><font color="#ff0000">NOTE: TAGSET &#8216;Tagsets.ExcelXP&#8217; has been saved to: SASUSER.TEMPLAT</font> <br /></font>

<font size="1">Since there is already an ExcelXP tagset in SASHELP.TMPLMST and it can’t be overwritten, this new added ExcelXP tagset is thrown to SASUSER.TEMPLAT by adding a STORE option (check the source code) and will be used when statement “ODS tagsets.ExcelXP” invoked.</font>

# 5. List all templates

> <font size="1" face="Courier New">proc template; <br />&#160;&#160;&#160; list / store=sasuser.templat; <br />&#160;&#160;&#160; list / store=sashelp.tmplmst; <br />run;</font>

<font size="1">Get output:</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="sasuser_templat2" border="0" alt="sasuser_templat2" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/sasuser_templat2_thumb.png" width="332" height="285" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/sasuser_templat2.png)

<font size="1">If only type “Tagset” need (<em>to save space!</em>):</font>

> <font size="1" face="Courier New">proc template; <br />list <font color="#ff0000">tagsets</font>/store=sasuser.templat; <br />run;</font>

# &#160;

# 6. Delete template

> <font size="1"><font face="Courier New">proc template; <br />&#160;&#160;&#160; delete Tagsets.ExcelBase; <br />&#160;&#160;&#160; delete Tagsets.ExcelXP; <br />run;</font> <br /></font>

<p align="left">
  <font size="1">It’s always safe to perform delete statements since <font size="1">items in SASHELP.TMPLMST are read only.</font>&#160; In this case, the ExcelXP tagset in SASUSER.TEMPLAT will be deleted.</font>
</p>

<p align="left">
  <font size="1">log:</font>
</p>

> <font size="1">8617&#160;&#160; proc template; <br />8618&#160;&#160;&#160;&#160;&#160;&#160; delete Tagsets.ExcelBase; <br />NOTE: &#8216;Tagsets.ExcelBase&#8217; has been deleted from: SASUSER.TEMPLAT <br />8619&#160;&#160;&#160;&#160;&#160;&#160; delete Tagsets.ExcelXP; <br />NOTE: <font color="#ff0000">&#8216;Tagsets.ExcelXP&#8217; has been deleted from: SASUSER.TEMPLAT</font> </font>

<p align="left">
  <font size="1">check again following step #5 and get what’s in SASUSER.TEMPLAT (no ExcelXP tagset anymore):</font>
</p>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="sasuser_templat" border="0" alt="sasuser_templat" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/sasuser_templat_thumb.png" width="333" height="247" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/sasuser_templat.png)

# 7 Install in other specified library

<font size="1">Install ExcelXp tagset in a other library. It will be deleted if current SAS session is killed:</font>

> <font size="1" face="Courier New">libname excltags &#8216;a:\test&#8217;; <br />ods path (prepend) excltags.templat(update); <br />filename excltags url &#8216;</font>[<font size="1" face="Courier New">http://support.sas.com/rnd/base/ods/odsmarkup/excltags.tpl&#8217;;</font>](http://support.sas.com/rnd/base/ods/odsmarkup/excltags.tpl';)<font size="1"><font face="Courier New"> <br />%include excltags;</font> </font>

<font size="1">log:</font>

> NOTE: Overwriting existing template/link: Tagsets.ExcelBase   
> NOTE: TAGSET &#8216;Tagsets.ExcelBase&#8217; has been saved to: EXCLTAGS.TEMPLAT   
> NOTE: Overwriting existing template/link: Tagsets.Config_debug   
> NOTE: TAGSET &#8216;Tagsets.Config_debug&#8217; has been saved to: EXCLTAGS.TEMPLAT   
> NOTE: Overwriting existing template/link: Tagsets.ExcelXP   
> NOTE: <font color="#ff0000">TAGSET &#8216;Tagsets.ExcelXP&#8217; has been saved to: EXCLTAGS.TEMPLAT</font> 

<p align="left">
  <font size="1">show path as step #3:</font>
</p>

> <p align="left">
>   Current ODS PATH list is:
> </p>
> 
> <p align="left">
>   1. EXCLTAGS.TEMPLAT(UPDATE) <br />2. SASUSER.TEMPLAT(UPDATE) <br />3. SASHELP.TMPLMST(READ)
> </p>

<p align="left">
  <font size="1"></font><font size="1">If apply step #6 to delete ExcelXP tagset, the items in EXCLTAGS.TEMPLAT will be deleted(as same as the searching priority).</font>
</p>

# 8. Hello World

<p align="left">
  <font size="1">Adopted from one of Vince DelGobbo’s papers(<a href="http://support.sas.com/rnd/papers/index.html#excel2012">2012</a>):</font>
</p>

> <font face="Courier New">title &#8216;The CLASS Data Set&#8217;; <br />footnote &#8216;(From the SASHELP Library)&#8217;;</font>
> 
> <font face="Courier New">*Set some "global" tagset options that affect all worksheets;</font>
> 
> <font face="Courier New">ods tagsets.ExcelXP path="a:\test\" file=&#8217;MyWorkbook.xml&#8217; style=Printer <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; options(embedded_titles=&#8217;yes&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; embedded_footnotes=&#8217;yes&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; print_header=&#8217;&C&A&RPage &P of &N&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; print_footer=&#8217;&RPrinted &D at &T&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; autofilter=&#8217;2&#8242;);</font>
> 
> <font face="Courier New">%macro doit;</font>
> 
> <font face="Courier New">proc sort data=sashelp.class (keep=sex) out=class nodupkey; <br />&#160;&#160;&#160; by sex; <br />run;</font>
> 
> <font face="Courier New">data _null_; <br />&#160;&#160;&#160; set class end=eof; <br />&#160;&#160;&#160; II=left(put(_n_,2.)); <br />&#160;&#160;&#160; call symputx(&#8216;sex&#8217;||II,compress(sex)); <br />&#160;&#160;&#160; if eof then call symputx(&#8216;total&#8217;,II); <br />run;</font>
> 
> <font face="Courier New">%do i=1 %to &total; <br />&#160;&#160;&#160; ods tagsets.ExcelXP options(sheet_name="Students_&&sex&i");</font>
> 
> <font face="Courier New">&#160;&#160;&#160; proc print data=sashelp.class noobs style(Header)=[just=center]; <br />&#160;&#160;&#160;&#160;&#160; where (sex eq "&&sex&i"); <br />&#160;&#160;&#160;&#160;&#160; var name age&#160;&#160;&#160;&#160;&#160; / style(Column)=[background=#99ccff]; <br />&#160;&#160;&#160;&#160;&#160; var height weight / style(Column)=[background=#99ccff tagattr=&#8217;format:#.0&#8242;]; <br />&#160;&#160;&#160; run; </font>
> 
> <font face="Courier New">%end;</font>
> 
> <font face="Courier New">%mend doit;</font>
> 
> <font face="Courier New">%doit</font>
> 
> <font face="Courier New">ods tagsets.ExcelXP close;</font> 

<p align="left">
  <font size="1">This .XML file can be opened by Office Excel:</font>
</p>

<p align="left">
  <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/SAS_ExcelXP.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="SAS_ExcelXP" border="0" alt="SAS_ExcelXP" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/SAS_ExcelXP_thumb.png" width="372" height="442" /></a>
</p>

# 9. Get Help

<font size="1">As a new comer, I found the following materials useful and accessible:</font>

  * <div align="left">
      <font size="1"><a href="http://support.sas.com/rnd/base/ods/odsmarkup/">SAS ODS MARKUP homepage</a></font>
    </div>

  * <div align="left">
      <font size="1">SAS developer <a href="http://www.sas.com/reg/gen/corp/867226?page=Resources">Vince DelGobbo’s homepage on ExcelXP</a></font>
    </div>

  * <div align="left">
      <font size="1"><a href="http://www.sas.com/events/cm/867226/ExcelXPPaperIndex.pdf">Vince DelGobbo&#8217;s ExcelXP Tagset Paper Index</a></font>
    </div>

  * #### <font size="1"><a href="http://support.sas.com/rnd/base/ods/odsmarkup/excelxp_help.html">Quick Reference for the TAGSETS.EXCELXP Tagset</a></font>

  * #### <font size="1"><a href="http://support.sas.com/rnd/base/ods/odsmarkup/excelxp_demo.html">Try This Demo: The ExcelXP Tagset and Microsoft Excel</a></font>

  * #### <font size="1"><a href="http://support.sas.com/resources/papers/proceedings09/323-2009.pdf">Modifying ODS Statistical Graphics Templates in SAS 9.2 by Warren F. Kuhfeld</a></font>