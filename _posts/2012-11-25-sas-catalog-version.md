---
id: 801
title: 'Extract the Version of SAS and OS of a SAS Format or Macro Catalog: A Little Bit of Perl Regular Expression'
date: 2012-11-25T20:36:52+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=801
permalink: /2012/11/25/sas-catalog-version/
categories:
  - Computer
  - SAS
tags:
  - format
  - Macro
  - Perl Regular Expression
  - SAS
---
<span style="font-size: xx-small;">SAS Sample 34444(<em><a href="http://support.sas.com/kb/34/443.html" target="_blank">Determine the operating system in which a format catalog was created</a></em>) posts piece of codes to get the version of SAS and OS of a SAS format catalog. It is useful since a SAS catalog can be only read in the operating systems same to its source machine.</span>

<span style="font-size: xx-small;">2 cents add to this note:</span>

<span style="font-size: xx-small;">First, we do not need to write codes to get to know the machine version for a catalog(<em><strong>formats.sas7bcat </strong></em>or<strong> <em>sasmacr.sas7bcat</em></strong>). Just open the catalog using a text editor, Notepad++, then you get</span>

> <span style="font-size: xx-small;">a SAS format catalog created by SAS 9.1 in a Windows XP Pro machine:</span>

[<span style="font-size: xx-small;"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="SAS_Format" alt="SAS_Format" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/11/SAS_Format_thumb.png" width="475" height="408" border="0" /></span>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/11/SAS_Format.png)

> <span style="font-size: xx-small;">and a SAS macro catalog by SAS 9.3 in a 64 bits Windows 7 Pro machine:</span>

[<span style="font-size: xx-small;"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="SAS_Macro" alt="SAS_Macro" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/11/SAS_Macro_thumb.png" width="464" height="375" border="0" /></span>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/11/SAS_Macro.png)

<span style="font-size: xx-small;">Second, if do want programming (for curiosity purpose; I like this idea), we can also improve the sample codes since the position and length information were hard coded in Line 21 (the question is: how can we know that?):</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">test=substr(theline,<span style="color: #ff0000;">210</span>,<span style="color: #ff0000;">20</span>);</span>

<span style="font-size: xx-small;">To get rid of hard coding, I use Perl Regular Expression. Just copy the archived codes for </span><a href="http://www.sesug.org/SESUG2012/abstract.html#BB-04" target="_blank"><span style="font-size: xx-small;">my SESUG 2012 talk</span></a> <span style="font-size: xx-small;">with tiny modification (I always use the same programming blocks if possible):</span>

[<span style="font-size: xx-small;">https://github.com/Jiangtang/SESUG2012/blob/master/read_SAP.sas</span>](https://github.com/Jiangtang/SESUG2012/blob/master/read_SAP.sas "https://github.com/Jiangtang/SESUG2012/blob/master/read_SAP.sas")

<span style="font-size: xx-small;">The following codes can be also used to run against SAS macro catalog:</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">filename fmt &#8220;a:formats.sas7bcat&#8221;;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">data fmt;<br /> infile fmt lrecl=1000 truncover;<br /> input line $1000.;<br /> run;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">data _null_;<br /> set fmt;<br /> if _n_=1 then do;<br /> retain queVer;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">            <span style="color: #ff0000;">ver=&#8221;/(\d+).[\d\w]+_[\d\w]+/&#8221;;</span><br /> queVer  = prxparse(ver);</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">            if missing(queVer) then do;<br /> putlog &#8220;ERROR: Invalid regexp&#8221; ver;<br /> stop;<br /> end;<br /> end;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">      queVerN  = prxmatch(queVer ,line);</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">      if queVerN > 0  then do ;<br /> call PRXsubstr(queVer,line,position,length);<br /> version = compress(substr(line, position, length));<br /> output;<br /> end;    </span>
> 
> <span style="font-size: xx-small;"><span style="font-family: 'Courier New';">      put position= length=;<br /> put version=;<br /> run;</span><br /> </span>

<span style="font-size: xx-small;">Test it against five Windows machines: </span>

> <span style="font-size: xx-small;">position=221 length=16<br /> version=9.0301M1X64_7PRO</span>
> 
> <span style="font-size: xx-small;">position=217 length=15<br /> version=9.0202M2NET_SRV </span>
> 
> <span style="font-size: xx-small;">position=221 length=17<br /> version=9.0202M3X64_SRV08 </span>
> 
> <span style="font-size: xx-small;">position=217 length=14<br /> version=9.0100A0XP_PRO</span>
> 
> <span style="font-size: xx-small;">position=217 length=15<br /> version=9.0101M3NET_SRV </span>

&nbsp;

<span style="font-size: xx-small;">P.S.: The pattern <strong>(d+).[dw]+_[dw]+</strong>  can be read as</span>

> <span style="font-size: xx-small;">number(s)                       +<br /> .                                      +<br /> some digits and words     +<br /> _                                     +<br /> some digits and words</span>

<span style="font-size: xx-small;">Since the underscore “_” is also included in meta-character <strong>w</strong>, it seems OK to simplify the pattern above to </span>

> **<span style="font-size: xx-small;">(d+).[dw]+ </span>**

<span style="font-size: xx-small;">But in a Window Server 2003 machine with SAS 9.2, it also returns the following unrelated information:</span>

> <span style="font-size: xx-small;">position=998 length=3<br /> version=2.S </span>