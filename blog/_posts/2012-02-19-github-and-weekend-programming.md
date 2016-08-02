---
id: 513
title: GitHub and Weekend Programming
date: 2012-02-19T16:17:32+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=513
permalink: /2012/02/19/github-and-weekend-programming/
categories:
  - CDISC
  - SAS
  - Uncategorized
tags:
  - CDISC
  - GIThub
  - OpenCDISC
  - SAS
---
<font size="1"><a href="https://github.com/yihui" target="_blank">Yihui</a> of Iowa State just texted me that <a href="https://github.com/" target="_blank">GitHub</a> is programmers’ Facebook. Inspired by him(great thanks!), I also begin to play with GitHub now:</font>

> [<font size="1">https://github.com/Jiangtang</font>](https://github.com/Jiangtang)

<font size="1">Currently I only created one repo as <a href="https://github.com/Jiangtang/Programming-SAS" target="_blank">personal SAS code repository</a>. To kill weekend time, I uploaded piece of codes to <a href="https://github.com/Jiangtang/Programming-SAS/blob/master/Rules_Count_OpenCDISC_XML.sas" target="_blank">count the OpenCDISC validation rules by models</a>. To use it:</font>

> <font size="1">filename CDISC url “<a href="https://raw.github.com/Jiangtang/Programming-SAS/master/Rules_Count_OpenCDISC_XML.sas">https://raw.github.com/Jiangtang/Programming-SAS/master/Rules_Count_OpenCDISC_XML.sas</a>”;</font>
> 
> <font size="1">%include CDISC;</font>
> 
> <font size="1">%Rules_Count_OpenCDISC_XML(dir=C:tempOpenCDISCsoftwareopencdisc-validatorconfig)</font>

<font size="1">while get:</font>

<font size="1"><a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/02/OC_by_model.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="OC_by_model" border="0" alt="OC_by_model" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/02/OC_by_model_thumb.png" width="360" height="238" /></a></font>

<font size="1">Happy weekend and happy programming.</font>