---
id: 1138
title: How to Jump into SAS Data Integration Studio
date: 2013-01-12T18:08:14+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1138
permalink: /2013/01/12/how-to-jump-into-sas-data-integration-studio/
categories:
  - Computer
  - SAS
tags:
  - ETL
  - SAS
  - SAS Data Integration Studio
  - SQL
  - Transformations
---
[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="SAS2DISJob" border="0" alt="SAS2DISJob" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/SAS2DISJob_thumb.png" width="415" height="452" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/SAS2DISJob.png)</a>

<font size="1">This is for for SAS programmers who might be reluctant to check out a GUI tool like SAS Data Integration Studio (DIS for short, which is graphic tool to implement ETL processes: extract, transform, load). DIS translates all users dragged nodes, transformations and process into SAS codes which are traditionally written by SAS programmers. I find one of the benefits of using DIS is that I can package all the ETL work to other players(technical or nontechnical) then they can replay the job by dragging and clicking. </font>

<font size="1">Actually besides translating all the visual nodes to SAS codes, DIS can also reversely incorporate your SAS codes to the graphic job shown as above. So SAS programmers can easily jump into DIS by importing their codes to get the graphic workflow (to get the first impression). Here is an one-minute demo:</font>

<font size="1">Save the following codes in a file(from </font><a href="http://support.sas.com/documentation/cdl/en/sqlproc/63043/HTML/default/viewer.htm#p0o4a5ac71mcchn1kc1zhxdnm139.htm" target="_blank"><font size="1">SAS SQL onlinedoc</font></a><font size="1">),</font>

> <font size="1" face="Courier New">%let dir=C:\;</font>
> 
> <font size="1" face="Courier New">libname source BASE "&dir"; <br />libname target BASE "&dir";</font>
> 
> <font size="1" face="Courier New">data source.one; <br />&#160;&#160;&#160; input x y; <br />datalines; <br />1 2 <br />2 3 <br />;</font>
> 
> <font size="1" face="Courier New">data source.two; <br />&#160;&#160;&#160; input x y; <br />datalines; <br />2 5 <br />3 6 <br />4 9 <br />;</font>
> 
> <font size="1" face="Courier New">proc sql; <br />&#160;&#160;&#160; create table target.three as <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; select o.x,o.y <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; from source.one as o, source.two as t <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; where o.x=t.x <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; ; <br />quit;</font>
> 
> <font size="1" face="Courier New">proc print data=target.three; <br />run;</font>

<font size="1">Just create a test folder in DIS (this demo was created in a working repository, in a Windows DIS 4.21 machine ) then right click mouse to “Import”-“Import SAS Code” to import the file created above then run the job generated and all set (you will get all stuff showed above).</font>

<font size="1">Note that the SAS libraries must be registered first in the <em>SAS Metadata</em> Server then you can use it. This demo omit this process only for demo purpose.</font>

<font size="1">You can check out the SQL Join by double clicking the SQL node:</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="SAS2DISJob_SQLJoin" border="0" alt="SAS2DISJob_SQLJoin" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/SAS2DISJob_SQLJoin_thumb.png" width="412" height="537" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/SAS2DISJob_SQLJoin.png)

<font size="1">and your codes in Code panel (still yours!):</font>

[<img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="image" border="0" alt="image" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/image_thumb.png" width="335" height="562" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/01/image.png)

<font size="1">Furthermore, without getting know bunch of the tool first, you can jump into DIS quickly by creating customized Transformations which are basically SAS codes with macro variables as the perimeters in the visual options box. Pretty neat? Just check it out!</font>