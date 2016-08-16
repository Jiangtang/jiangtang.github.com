---
id: 1369
title: Import .Rdata to SAS, along with Labels
date: 2015-05-12T13:06:28+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1369
permalink: /2015/05/12/import-rdata-to-sas-along-with-labels/
categories:
  - R
  - SAS
tags:
  - format
  - R
  - SAS
---
<span style="font-size: xx-small;">I didn’t </span>[<span style="font-size: xx-small;">play with SAS/IML</span>](http://www.jiangtanghu.com/blog/2010/10/29/sas-iml-basic/) <span style="font-size: xx-small;">for a while. I call it back when I need to read some R format data.</span>

<span style="font-size: xx-small;">Technically, .Rdata is not a data format. It’s rather a big container to hold bunch of R objects:</span>

<span style="font-size: xx-small;"><a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2015/05/Rdata1.png"><img style="background-image: none; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border: 0px;" title="Rdata" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2015/05/Rdata_thumb1.png" alt="Rdata" width="408" height="213" border="0" /></a></span>

<span style="font-size: xx-small;">In this example, when a .Rdata is loaded, 3 objects are included where ‘data’(the ‘real’ data) and ‘desc’ (data description portion) are of our interests.</span>

<span style="font-size: xx-small;">SAS/IML offers a nice interface to call R command which can be used to read the R format data:</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">proc iml;<br /> <strong>submit / R;</strong><br /> load(&#8220;C:/data/w5/R data sets for 5e/GPA1.RData&#8221;)<br /> <strong>endsubmit;</strong></span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">    <strong>call</strong> <strong>ImportDataSetFromR</strong>(&#8220;work.GPA1&#8221;, &#8220;<span style="color: #ff0000;">data</span>&#8220;);<br /> <strong>call</strong> <strong>ImportDataSetFromR</strong>(&#8220;work.GPA1desc&#8221;, &#8220;<span style="color: #ff0000;">desc</span>&#8220;);</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">quit;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">data _null_;<br /> set GPA1desc end = eof ;<br /> i+1;<br /> II=left(put(i,3.));<br /> call symputx(&#8216;var&#8217;||II,variable);<br /> call symputx(&#8216;label&#8217;||II,label);<br /> if eof then call symputx(&#8216;n&#8217;,II);<br /> run;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">%macro labelit;<br /> data gpa1;<br /> set gpa1;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">    label<br /> %do i=1 %to &n;<br /> &&var&i = &&label&i<br /> %end;<br /> ;<br /> run;<br /> %mend;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">%labelit</span>