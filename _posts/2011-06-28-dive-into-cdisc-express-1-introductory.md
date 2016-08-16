---
id: 244
title: 'Dive into CDISC Express (1): Introductory'
date: 2011-06-28T21:24:33+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/06/28/dive-into-cdisc-express-1-introductory/
permalink: /2011/06/28/dive-into-cdisc-express-1-introductory/
categories:
  - CDISC
  - SAS
  - XML
tags:
  - CDISC
  - CDISC Express
  - SAS
---
Recently I did for my personal project some research on <a href="http://www.clinovo.com" target="_blank">Clinovo</a>’s open source application, <a href="http://www.clinovo.com/cdisc" target="_blank">CDISC Express</a>, a SAS application based on Excel framework designed to map clinical data to CDISC SDTM domains automatically. Not perfect yet, but it is easily understandable and practically usable after few hours’ of exploration of user guide. And most important, it is on the right way: an automatic CDISC converter is the magic weapon in almost every clinical programmer’s dream.

CDISC Express is the first and only practically usable open source CDISC converter I even met. I wrote <a href="http://www.jiangtanghu.com/blog/2011/05/16/cdisc-express-a-glance" target="_blank">a post a month ago</a> when I first tested it with great interests and reported some issues to its <a href="http://cdiscsupport.clinovo.com/" target="_blank">fix system</a>. Then I also had the great opportunity to discuss the software via email with its core developer, Romain Miralles. This post is just my personal notes on how to use and dig into the software, and will be best serve as a working documentation. You can return to me for any questions and comments.

By the way, there is an opportunity for your practicing and you will also have a change to win an iPad2 from Clinovo’s CDISC Express Contest:

> <http://www.clinovo.com/cdisc/game>

The due day is July 15<sup>th</sup> and I already submitted my work. That’s fun.

# 1. Download and Installation

You can get CDISC Express for free in

> <http://www.clinovo.com/cdisc/download>

It is a window application and will be installed by default in 

> **C:Program FilesCDISC Express**

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image002[4]" border="0" alt="clip_image002[4]" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/06/clip_image0024_thumb.jpg" width="420" height="333" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/06/clip_image0024.jpg)

After installation, this path will be coded as a macro variable <font color="#ff0000">&CDISCPATH</font> in the following six SAS files which are all located in **C:Program FilesCDISC Expressprograms**:

> _create\_new\_study.sas_
> 
> _generate_Definexml.sas_
> 
> _generate\_mapping\_template.sas_
> 
> _generate_SDTM.sas_
> 
> _Validate\_Mapping\_File.sas_
> 
> _Validate\_SDTM\_Domains.sas_

The macro variable reads as

> <font face="Courier New">%LET CDISCPATH = C:Program FilesCDISC Express;</font>

If you change the destination folder at the installation stage, e.g., to **D:CDISC Express**, the value of the macro variable <font color="#ff0000">&CDISCPATH</font> will be changed accordingly in the six files mentioned before:

> <font face="Courier New">%LET CDISCPATH = D:CDISC Express;</font>

Note that if you want copy the whole folder of files to another destination, you should at least manually change the value of <font color="#ff0000">&CDISCPATH</font> in such six files or add some codes to capture the path accordingly. From this point of view, the path setting of CDISC Express is not completely portable. Recommend that if you have such needs, just re-install the software in any destination you want. It will not write any records into registry and you can have many copies in one machine.

The following discussion assumes the software roots in **C:Program FilesCDISC Express.**

# **2.** **Working Flow**

You can follow all the 6 action steps one by one coded in

> **C:Program FilesCDISC Expressprograms**

##### 1) Create a new study (_create\_new\_study.sas_)

Simple and easy. Just assign a new study name in a macro call and run.

##### 2) Generate mapping file (_generate\_mapping\_template.sas_)

This is the critical and most time consuming part. You should design mapping rules for every domain needed in Excel spreadsheets (the MAPPING FILE). If done, all other tasks, such as generate SDTM datasets, SAS transport files, define.xml and validation, can be well done by just clicking[<img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px" title="clip_image003[4]" border="0" alt="clip_image003[4]" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/06/clip_image0034_thumb.gif" width="37" height="33" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/06/clip_image0034.gif) buttons 

.

##### 3) Validate mapping file (_Validate\_Mapping\_File.sas_)

For validating the mapping file, just click the button. As mentioned, the most important work is designing mapping file. It would be back and forth to design mapping file and validate it.

##### 4) Generate SDTM datasets (_generate_SDTM.sas_)

If mapping file is OK, click the button.

##### 5) Validate SDTM datasets (_Validate\_SDTM\_Domains.sas_)

Click the button.

##### 6) Generate Define.xml (_generate_Definexml.sas_)

Click the button.

Following part will dig into the software step by step.

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="TobeContinued" border="0" alt="TobeContinued" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/06/TobeContinued_thumb.jpg" width="240" height="181" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/06/TobeContinued.jpg)