---
id: 1298
title: A SAS Note for Length Limit of Strings in CDISC Datasets
date: 2014-02-18T23:37:22+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1298
permalink: /2014/02/18/a-sas-note-for-length-limit-of-strings-in-cdisc-datasets/
categories:
  - CDISC
  - SAS
tags:
  - CDISC
  - SAS
---
<font size="1">Clinical programmers are very familiar with the length limit of strings in CDISC compliant datasets, such as</font>

  * <font size="1">#1: variable names: <= 8 characters</font>
  * <font size="1">#2: variable labels: <= 40 characters</font>
  * <font size="1">#3: data set labels: <= 40 characters</font>
  * <font size="1">#4: data value of a single variable: <= 200 characters</font>

<font size="1">and they are due to the limitations of SAS XPORT transport files (v5). But there are some rules which are not&#160; as explicit as rule #1-4, for example,</font>

  * <font size="1">#5: For domain LB, data value of variable LBTESTCD: <= 8 characters</font>
  * <font size="1">#6: For domain LB, data value of variable LBTEST: <= 40 characters</font>

<font size="1">Rule #5-6 is much more strict than #4&#160; where 200 is the maximum. Actually, in SDTM Implementation Guide, the rational was well stated (“<em>4.1.5.3.1&#160; TEST NAME (&#8211;TEST) GREATER THAN 40 CHARACTERS</em>”):</font>

> <font size="1">Since the &#8211;TEST variable is meant to serve as a label for a &#8211;TESTCD when a Findings dataset is transposed to a more horizontal format, the length of &#8211;TEST is normally limited to 40 characters to conform to the limitations of the SAS V5 Transport format currently used for submission datasets.</font>

<font size="1">You can take the following piece of codes to understand it where rule #5-6 actually are set to follow rule #1-2:</font>

> <font size="1" face="Courier New">data lb; <br />&#160;&#160;&#160; input usubjid $ lbtestcd $&#160; lbtest $ lborres visitnum; <br />datalines; <br />001 AA aaaaa 12 1 <br />001 BB bbbbb 20 1 <br />001 CC ccccc 3&#160; 1 <br />001 AA aaaaa 4&#160; 2 <br />001 BB bbbbb 40 2 <br />001 CC ccccc 35 2 <br />;</font>
> 
> <font face="Courier New"><font size="1">proc transpose data=lb out=lb2 (drop=_name_); <br />&#160;&#160;&#160; by usubjid&#160; visitnum; <br />&#160;&#160;&#160; var lborres; <br /></font><font size="1"><font color="#ff0000">&#160;&#160;&#160; id lbtestcd; <br />&#160;&#160;&#160; idlabel lbtest;</font> <br />run;</font></font>

[<font size="1"><img title="idlabel" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; border-left: 0px; display: block; padding-right: 0px" border="0" alt="idlabel" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2014/02/idlabel_thumb.png" width="514" height="253" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2014/02/idlabel.png)