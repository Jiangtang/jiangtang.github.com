---
id: 1159
title: Yet Another Undocumented Feature (new in SAS 9.3)
date: 2013-02-26T21:00:14+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1159
permalink: /2013/02/26/yet-another-undocumented-feature-new-in-sas-9-3/
categories:
  - SAS
tags:
  - SAS
  - undocumented feature
---
<span style="font-size: xx-small;">Today just caught an undocumented SAS feature. I ran the following SAS codes to delete a dataset(in Windows 7 with SAS 9.3):</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">data a;<br /> b=1;<br /> run;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">proc datasets <span style="color: #ff0000;">noprint</span>;<br /> delete a;<br /> run;<br /> quit;</span>

<span style="font-size: xx-small;">and the dataset was deleted as I expected:</span>

> <span style="font-size: xx-small;">32   proc datasets noprint;<br /> 33       delete a;<br /> 34   run;</span>
> 
> <span style="font-size: xx-small;">NOTE: Deleting WORK.A (memtype=DATA).<br /> 35   quit;</span>

<span style="font-size: xx-small;">But when tested in a SAS 9.2 machine, I got errors</span>

> <span style="font-size: xx-small;">25   proc datasets noprint;<br /> &#8212;&#8212;-<br /> 22<br /> 202<br /> NOTE: Enter RUN; to continue or QUIT; to end the procedure.<br /> <span style="color: #ff0000;">ERROR</span> 22-322: Syntax error, expecting one of the following: ;, ALTER, DD, DDNAME, DETAILS,<br /> FORCE, GENNUM, KILL, LIB, LIBRARY, MEMTYPE, MT, MTYPE, NODETAILS, NOFS, NOLIST,<br /> NOWARN, PROTECT, PW, READ.<br /> <span style="color: #ff0000;">ERROR</span> 202-322: The option or parameter is not recognized and will be ignored.<br /> 26       delete a;<br /> 27   run;</span>
> 
> <span style="font-size: xx-small;">NOTE: Statements not processed because of errors noted above.<br /> 27 !     quit;</span>
> 
> <span style="font-size: xx-small;">NOTE: The SAS System stopped processing this step because of errors.</span>

<span style="font-size: xx-small;">Then I checked the SAS HelpDoc, there is no such “noprint” option in </span>[<span style="font-size: xx-small;">PROC DATASETS statement</span>](http://support.sas.com/documentation/cdl/en/proc/65145/HTML/default/viewer.htm#p0xdkenol7pi1cn14p0iq38shax4.htm)<span style="font-size: xx-small;">, but in </span>[<span style="font-size: xx-small;">CONTENTS statement</span>](http://support.sas.com/documentation/cdl/en/proc/65145/HTML/default/viewer.htm#p1v2467vdjbp7xn1222c7t3sejz3.htm) <span style="font-size: xx-small;">in the PROC DATASETS PROCEDURE. Actually I added the “noprint” option just because I expected it act like the same option in </span>[<span style="font-size: xx-small;">PROC FREQ statement</span>](http://support.sas.com/documentation/cdl/en/procstat/65543/HTML/default/viewer.htm#procstat_freq_syntax01.htm) <span style="font-size: xx-small;">to suppresses output. And (un)fortunately, it worked in my machine…</span>

UPDATE(2013-02-27): Just got feedback from a SAS developer this &#8220;noprint&#8221; will be documented in the upcoming SAS 9.4; actually it works like the existing &#8220;<a href="http://support.sas.com/documentation/cdl/en/proc/65145/HTML/default/viewer.htm#p0xdkenol7pi1cn14p0iq38shax4.htm" target="_blank">nolist</a>&#8221; option.