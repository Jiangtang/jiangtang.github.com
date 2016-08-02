---
author: Jiangtang Hu
title: 'CDISC Express: A Glance'
excerpt:
layout: post
category:
  - CDISC
  - SAS
tags:
  - CDISC
  - SAS
post_format: [ ]
---
This weekend I tested an application that can automatically transform clinical data to CDISC SDTM compliant datasets(3.1.1 and 3.1.2), [CDISC Express][1] of [Clinovo][2]. According to its license statements, you can download it for free and for personal use only.

The core of CDISC Express is an Excel configuration file called Mapping File which defines all the metadata and mapping rules required by CDISC SDTM standard. Then a set of SAS macros is used to

*   validate the SDTM mapping file 
*   generate SDTM datasets 
*   generate define.xml file 
*   validate the SDTM datasets 

I found its architecture is simple, concise and powerful. When mentioned “simple”, I mean it is easy to understand and implement. It is still in its version 1.0, I wish following enhancements in the future according my personal user experiences: 

*   More web browsers supports for define.xml file and documentation 
*   **More merge or set types** 
*   Debug mechanism enhancement

 [1]: http://www.clinovo.com/cdisc
 [2]: http://www.clinovo.com/