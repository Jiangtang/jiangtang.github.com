---
id: 1111
title: How to Get Row Numbers in SAS Proc SQL (and DO NOT Use the Undocumented MONOTONIC Function)
date: 2013-01-11T15:01:09+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1111
permalink: /2013/01/11/get-row-numbers-in-sas-proc-sql/
categories:
  - SAS
tags:
  - SAS
  - SQL
---
<span style="font-size: xx-small;">SAS programmers are longing for row number function used in Proc SQL, like </span>[<span style="font-size: xx-small;">ROW_NUMBER() in Oracle SQL</span>](http://docs.oracle.com/cd/B19306_01/server.102/b14200/functions137.htm) <span style="font-size: xx-small;">and it will act like data step system variable _N_. When you google this question, most likely you will get MONOTONIC() function, which might be one of the most famous </span>[<span style="font-size: xx-small;">undocumented features shipped by SAS</span>](www2.sas.com/proceedings/sugi29/040-29.pdf)<span style="font-size: xx-small;">. You can of course use it, but at your own risk! In SAS Usage Note 15138, it&#8217;s said:</span>

> <span style="font-size: xx-small;">The MONOTONIC() function is not supported in PROC SQL. Using the MONOTONIC() function in PROC SQL can cause missing or non-sequential values to be returned.</span>

<span style="font-size: xx-small;">Here question is, why stick to the function? Actually there is a long-existing Proc SQL option (<em>at least since SAS 9.1.3 which was my first SAS version</em>), </span>[<span style="font-size: xx-small;">NUMBER</span>](http://support.sas.com/documentation/cdl/en/sqlproc/63043/HTML/default/viewer.htm) <span style="font-size: xx-small;">to return the row numbers:</span>

> <span style="font-size: xx-small;"><span style="font-family: 'Courier New';">proc sql number outobs=5;<br /> select Species<br /> from sashelp.iris<br /> ;<br /> quit;</span></span>

<span style="font-size: xx-small;">See a new column &#8220;Row&#8221; was created in response to this NUMBER option.</span>

<p style="text-align: center;">
  <span style="font-size: xx-small;"><img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border-width: 0px;" alt="" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/011113_2003_HowtoGetRow1.png" border="0" /></span>
</p>

[update 2014/03/19] A reader asked how to capture such row number in a data set since the NUMBER option only affects in output. Well, if it shows up in output, we can always use ODS to retrieve it. Submit the follow codes to check which output table will be generated (which is **SQL_Results**):

> <span style="font-family: 'Courier New';">ods trace on;</span>
> 
> <span style="font-family: 'Courier New';">proc sql number outobs=5;<br /> select Species<br /> from sashelp.iris<br /> ;<br /> quit;</span>
> 
> <span style="font-family: 'Courier New';">ods trace off;</span>

Then  use the standard ODS OUTPUT statement to get it:

> <span style="font-family: 'Courier New';">ods output SQL_Results=rownumber;</span>
> 
> <span style="font-family: 'Courier New';">proc sql number outobs=5;<br /> select Species<br /> from sashelp.iris<br /> ;<br /> quit;</span>