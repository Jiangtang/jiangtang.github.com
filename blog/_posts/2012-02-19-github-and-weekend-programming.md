---
author: Jiangtang Hu
title: GitHub and Weekend Programming
excerpt:
layout: post
category:
  - CDISC
  - SAS
  - Uncategorized
tags:
  - CDISC
  - GIThub
  - OpenCDISC
  - SAS
post_format: [ ]
---
[Yihui][1] of Iowa State just texted me that [GitHub][2] is programmers’ Facebook. Inspired by him(great thanks!), I also begin to play with GitHub now:

> <https://github.com/Jiangtang>

Currently I only created one repo as [personal SAS code repository][3]. To kill weekend time, I uploaded piece of codes to [count the OpenCDISC validation rules by models][4]. To use it:

> filename CDISC url “[https://raw.github.com/Jiangtang/Programming-SAS/master/Rules\_Count\_OpenCDISC_XML.sas][5]”;
> 
> %include CDISC;
> 
> %Rules\_Count\_OpenCDISC_XML(dir=C:tempOpenCDISCsoftwareopencdisc-validatorconfig)

while get:

[![OC_by_model][7]][7]

Happy weekend and happy programming.

 [1]: https://github.com/yihui
 [2]: https://github.com/
 [3]: https://github.com/Jiangtang/Programming-SAS
 [4]: https://github.com/Jiangtang/Programming-SAS/blob/master/Rules_Count_OpenCDISC_XML.sas
 [5]: https://raw.github.com/Jiangtang/Programming-SAS/master/Rules_Count_OpenCDISC_XML.sas
 []: http://dl.dropbox.com/u/69732603/OC_by_model.png