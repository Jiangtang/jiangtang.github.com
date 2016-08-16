---
id: 1145
title: 'SAS ODS Report Writing Interface: A Quick Demo'
date: 2013-02-17T20:21:00+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1145
permalink: /2013/02/17/sas-ods-report-writing-interface-a-quick-demo/
categories:
  - SAS
tags:
  - ODS
  - ODS Report Writing
  - Report
  - SAS
---
[<font size="1"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="IRIS" border="0" alt="IRIS" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/IRIS_thumb.png" width="335" height="451" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/IRIS.png)

<font size="1">I personally nominated </font>[<font size="1">SAS ODS Report Writing Interface</font>](http://support.sas.com/rnd/base/datastep/dsobject/index.html) <font size="1">was the one of the </font>[<font size="1">best technology I found in SAS in 2012</font>](http://www.jiangtanghu.com/blog/2012/12/31/best-of-sas-a-personal-nomination-2012/)<font size="1">. It can generates reports cell by cell and row by row and has much flexibility to produce highly customized reports. Basically, to use it,</font>

  * <font size="1">first assign an ODS destination. Nothing new, and I prefer HTML like</font>

> <font size="1" face="Courier New">ods html&#160;&#160; file="output.html" style=sasweb;</font>

  * <font size="1">then create a object(instance) based on the ODS Report Writing class, odsout,</font>

> <font size="1" face="Courier New">declare odsout myout();</font>

<font size="1">ODS Report Writing Interface holds some so called object oriented features. Odsout is a predefined class (or, a SET, a CONTAINER), then you take from it a instance or an object, myout(or any other legal SAS variable names). Suppose Odsout is a class for apples, then myout is a specific apple.</font>

  * <font size="1">apply methods associated with the Odsout class, like CELL, ROW, TABLE to generate reports.</font>

<font size="1">Roughly methods are just the functions (subroutines, procedures) in the object oriented world. For example, in SAS Data Steps, you use function <font face="Courier New">weight(apple)</font> to get the weight of the apple; in object oriented world, you use <font face="Courier New">apple.weight()</font> to return the same thing. In ODS Report Writing Interface, if you want to get a table, use TABLE methods:</font>

  * <font size="1">myout.TABLE_START() to start a table</font>
  * <font size="1">myout.TABLE_END to end a table</font>

<font size="1">Then all we need to do next is to use the flexible SAS data steps to leverage the ODS Report Writing Interface methods (see docs). The codes, you can see below, are pretty verbose compared to its counterparts, PROC REPORT, but that’s why it gains power to build highly customized reports. It’s also very structural (and easy to build, like playing blocks):</font>

> <font size="1" face="Courier New">/*making a sortable HTML table*/ <br />%macro ods_html_sort_table; <br />&#160;&#160;&#160; <script src=&#8217;</font>[<font size="1" face="Courier New">http://goo.gl/Pg0GB&#8217;</font>](http://goo.gl/Pg0GB')<font size="1" face="Courier New">></script> <br />&#160;&#160;&#160; <script src=&#8217;</font>[<font size="1" face="Courier New">http://goo.gl/ruKEb&#8217;</font>](http://goo.gl/ruKEb')<font size="1" face="Courier New">></script> <br />&#160;&#160;&#160; <script>$(document).ready(function(){$(&#8216;.table&#8217;).tablesorter({widgets: [&#8216;zebra&#8217;]});});</script> <br />%mend;</font>
> 
> <font size="1" face="Courier New">title ; <br />ods listing close; <br />ods html&#160;&#160; file="a:\test\iris.html" style=sasweb headtext="%ods_html_sort_table";</font>
> 
> <font size="1" face="Courier New">data _null; <br />&#160;&#160;&#160; set sashelp.iris; <br />&#160;&#160;&#160; by Species; <br />&#160;&#160;&#160; <br />/*&#160;&#160;&#160; create an object, obj, based on the ODS Report Writing class, odsout*/ <br />&#160;&#160;&#160; if _n_ = 1 then do; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; dcl odsout obj(); <br />&#160;&#160;&#160; end;</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160; if (first.Species) then do; *by group processing; <br />&#160;&#160;&#160;&#160;&#160;&#160; obj.title(text: "Fisher&#8217;s Iris Data Set by Species"); *title;</font>
> 
> <font size="1" face="Courier New">/*&#160;&#160;&#160;&#160;&#160;&#160; start a table*/ <br />&#160;&#160;&#160;&#160;&#160;&#160; obj.table_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; if (Species = "Setosa") then <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.image(file: "Iris_setosa.jpg" );*insert image; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; else if (Species = "Versicolor") then <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.image(file: "Iris_versicolor.jpg" ); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; else if (Species = "Virginica") then <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.image(file: "Iris_virginica.jpg" ); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_end();</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Iris Species",&#160; overrides: "fontweight=bold just=right" ); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: Species, column_span: 3, overrides: "just=left"); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_end();</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Unit",&#160; overrides: "fontweight=bold just=right" ); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "(mm)", column_span: 3, overrides: "just=left"); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_end(); <br />&#160;&#160;&#160;&#160;&#160;&#160; obj.table_end();</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160; /* start another table */ <br />&#160;&#160;&#160;&#160;&#160;&#160; obj.table_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.head_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Sepal Length" , overrides: "fontweight=bold"); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Sepal Width" , overrides: "fontweight=bold"); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Petal Length" , overrides: "fontweight=bold"); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Petal Width" , overrides: "fontweight=bold"); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_end(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.head_end(); <br />&#160;&#160;&#160; end;</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(data: SepalLength); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(data: SepalWidth); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(data: PetalWidth); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(data: SepalLength); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_end();</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160; if (last.Species) then do; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.table_end();</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.note(data: "Note: These Tables are Sortable."); *note;</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.foot_start(); *footer; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.cell_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_text(data: "Footer: Data from SAS V&sysver at &sysscp &sysscpl Sashelp.iris",just:"C"); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.cell_end(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.row_end(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.foot_end();</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.page(); <br />&#160;&#160;&#160; end; <br />run;</font>
> 
> <font size="1" face="Courier New">ods html close; <br />ods listing;</font>

<font size="1">Note:</font>

  * <font size="1">A flavor added to get a sortable HTML report. Thanks to </font>[<font size="1">Charlie Huang</font>](http://www.sasanalysis.com/2013/01/make-all-sas-tables-sortable-in-output.html) <font size="1">and then </font>[<font size="1">Andrew Z</font>](https://heuristically.wordpress.com/2013/01/17/sortable-html-tables-sas-ods/) <font size="1">to introduce a Javascript library JQury to SAS HTML report.</font>
  * <font size="1">The full report, see </font>[<font size="1">here</font>](https://heuristically.wordpress.com/2013/01/17/sortable-html-tables-sas-ods/)<font size="1">.</font>
  * <font size="1">If column spannings needed, use the following codes as header (and the report </font>[<font size="1">here</font>](http://www.jiangtanghu.com/docs/en/demo/iris_spanning.html)<font size="1">):</font>
> <font size="1" face="Courier New">obj.head_start(); <br />&#160;&#160;&#160; obj.row_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Sepal" , overrides: "fontweight=bold",column_span: 2); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Petal" , overrides: "fontweight=bold",column_span: 2); <br />&#160;&#160;&#160; obj.row_end();</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160; obj.row_start(); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Length" ); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Width" ); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Length" ); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; obj.format_cell(text: "Width" ); <br />&#160;&#160;&#160; obj.row_end(); <br />obj.head_end();</font>

  * <font size="1">ODS Report Writing Interface will get rid of its preproduction hat since SAS 9.4, but you can use it somehow since SAS 9.1.3. For more, see the <a href="http://support.sas.com/documentation/solutions/early/">draft SAS 9.4 ODS documentation</a> with <font size="1">ODS Report Writing Interface.</font></font>
  * <font size="1">To get started, see <a href="http://support.sas.com/rnd/base/datastep/dsobject/Power_to_show_paper.pdf">the developer’s paper</a>.</font>