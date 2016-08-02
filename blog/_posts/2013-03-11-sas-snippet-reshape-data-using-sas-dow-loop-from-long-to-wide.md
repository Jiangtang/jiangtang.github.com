---
id: 1167
title: 'SAS Snippet: Reshape Data Using SAS DoW Loop (From Long to Wide)'
date: 2013-03-11T21:10:28+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1167
permalink: /2013/03/11/sas-snippet-reshape-data-using-sas-dow-loop-from-long-to-wide/
categories:
  - SAS
tags:
  - DoW-Loop
  - SAS
  - Transpose
---
[<font size="1"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="F_Carpenter_cover.indd" border="0" alt="F_Carpenter_cover.indd" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/03/Art_SAS_thumb.gif" width="295" height="416" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/03/Art_SAS.gif)

<font size="1">In Art Carpenter’s latest book, <em><a href="https://support.sas.com/pubscat/bookdetails.jsp?pc=62454">Carpenter&#8217;s Guide to Innovative SAS Techniques</a></em>, a data step approach to transpose data (from long to wide) works like (Ch2.4.2):</font>

[<font size="1"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="Art_SAS_transpose" border="0" alt="Art_SAS_transpose" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/03/Art_SAS_transpose_thumb.png" width="341" height="325" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/03/Art_SAS_transpose.png)

> <font size="1" face="Courier New">data tst; <br />&#160;&#160;&#160; input type $ grp value $3.; <br />datalines; <br />A 1 a <br />A 2 aa <br />A 3 aaa <br />B 1 b <br />B 2 bb <br />B 3 bbb <br />C 1 c <br />C 2 cc <br />C 3 ccc <br />;</font>
> 
> <font size="1" face="Courier New">data art(keep=type grp1-grp3); <br />&#160;&#160; set tst; <br />&#160;&#160; by type; <br />&#160;&#160; retain grp1-grp3 ; <br />&#160;&#160; array grps {3} $ grp1-grp3; <br />&#160;&#160; if first.type then do i = 1 to 3; <br />&#160;&#160;&#160;&#160;&#160; grps{i} = " "; <br />&#160;&#160; end;</font>
> 
> <font size="1" face="Courier New">&#160;&#160; grps{grp} = value; <br />&#160;&#160; if last.type then output art ; <br />run;</font>

<font size="1">And such logic can be best demonstrated by a </font>[<font size="1">DoW Loop</font>](http://www.jiangtanghu.com/blog/2012/10/20/dow-loop-dorfman/)<font size="1">:</font>

> <font size="1"><font face="Courier New">data dow(keep=type grp1-grp3); <br />&#160;&#160;&#160;&#160; array grps[3] $ grp1-grp3; <br />&#160;&#160;&#160;&#160; do _n_ = 1 by 1 until(last.type); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; set tst; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; by type; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; grps[grp]=value; <br />&#160;&#160;&#160;&#160; end; <br />run;</font> </font>

# <font style="font-weight: bold">/*Note*/</font>

<font size="1">1. The traditional PROC TRANSPOSE approach:</font>

> <font size="1" face="Courier New">proc transpose data=tst <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; out=trans(drop=_:) <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; prefix=grp; <br />&#160;&#160; by type; <br />&#160;&#160; id grp; <br />&#160;&#160; var value; <br />run;</font>

<font size="1">2. Why use data step approach (both Art and DoW) to transpose data against the TRANSPOSE procedure:</font>

  * <font size="1">it’s much faster since data step array used</font>
  * <font size="1">save codes when complex transformation needed</font>
  * <font size="1">last but not least, it’s cool!</font>

<font size="1"></font>

<font size="1">3. Arthur Tabachneck maintains a general data step transposing macro, </font>[<font size="1">%transpose</font>](http://www.sascommunity.org/wiki/A_Better_Way_to_Flip_(Transpose)_a_SAS_Dataset) <font size="1">and you can call it like:</font>

> <font size="1" face="Courier New">%transpose(data=tst, out=mac, <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; by=type, var=value, <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; id=grp)</font>