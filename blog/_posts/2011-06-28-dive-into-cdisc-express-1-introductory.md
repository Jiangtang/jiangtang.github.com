---
author: Jiangtang Hu
title: 'Dive into CDISC Express (1): Introductory'
excerpt:
layout: post
category:
  - CDISC
  - SAS
  - XML
tags:
  - CDISC
  - CDISC Express
  - SAS
post_format: [ ]
---
Recently I did for my personal project some research on [Clinovo][1]’s open source application, [CDISC Express][2], a SAS application based on Excel framework designed to map clinical data to CDISC SDTM domains automatically. Not perfect yet, but it is easily understandable and practically usable after few hours’ of exploration of user guide. And most important, it is on the right way: an automatic CDISC converter is the magic weapon in almost every clinical programmer’s dream.

CDISC Express is the first and only practically usable open source CDISC converter I even met. I wrote [a post a month ago][3] when I first tested it with great interests and reported some issues to its [fix system][4]. Then I also had the great opportunity to discuss the software via email with its core developer, Romain Miralles. This post is just my personal notes on how to use and dig into the software, and will be best serve as a working documentation. You can return to me for any questions and comments.

By the way, there is an opportunity for your practicing and you will also have a change to win an iPad2 from Clinovo’s CDISC Express Contest:

> <http://www.clinovo.com/cdisc/game>

The due day is July 15th and I already submitted my work. That’s fun.

# 1. Download and Installation

You can get CDISC Express for free in

> <http://www.clinovo.com/cdisc/download>

It is a window application and will be installed by default in 

> **C:Program FilesCDISC Express**

[![clip_image002[4]][6]][6]

After installation, this path will be coded as a macro variable &CDISCPATH in the following six SAS files which are all located in **C:Program FilesCDISC Expressprograms**:

> *create\_new\_study.sas*
> 
> *generate_Definexml.sas*
> 
> *generate\_mapping\_template.sas*
> 
> *generate_SDTM.sas*
> 
> *Validate\_Mapping\_File.sas*
> 
> *Validate\_SDTM\_Domains.sas*

The macro variable reads as

> %LET CDISCPATH = C:Program FilesCDISC Express;

If you change the destination folder at the installation stage, e.g., to **D:CDISC Express**, the value of the macro variable &CDISCPATH will be changed accordingly in the six files mentioned before:

> %LET CDISCPATH = D:CDISC Express;

Note that if you want copy the whole folder of files to another destination, you should at least manually change the value of &CDISCPATH in such six files or add some codes to capture the path accordingly. From this point of view, the path setting of CDISC Express is not completely portable. Recommend that if you have such needs, just re-install the software in any destination you want. It will not write any records into registry and you can have many copies in one machine.

The following discussion assumes the software roots in **C:Program FilesCDISC Express.**

# **2. ****Working Flow**

You can follow all the 6 action steps one by one coded in

> **C:Program FilesCDISC Expressprograms**

##### 1) Create a new study (*create\_new\_study.sas*)

Simple and easy. Just assign a new study name in a macro call and run.

##### 2) Generate mapping file (*generate\_mapping\_template.sas*)

This is the critical and most time consuming part. You should design mapping rules for every domain needed in Excel spreadsheets (the MAPPING FILE). If done, all other tasks, such as generate SDTM datasets, SAS transport files, define.xml and validation, can be well done by just clicking[![clip_image003[4]][7]][7] buttons 

.

##### 3) Validate mapping file (*Validate\_Mapping\_File.sas*)

For validating the mapping file, just click the button. As mentioned, the most important work is designing mapping file. It would be back and forth to design mapping file and validate it.

##### 4) Generate SDTM datasets (*generate_SDTM.sas*)

If mapping file is OK, click the button.

##### 5) Validate SDTM datasets (*Validate\_SDTM\_Domains.sas*)

Click the button.

##### 6) Generate Define.xml (*generate_Definexml.sas*)

Click the button.

Following part will dig into the software step by step.

[![TobeContinued][8]][8]

 [1]: http://www.clinovo.com
 [2]: http://www.clinovo.com/cdisc
 [3]: http://www.jiangtanghu.com/blog/2011/05/16/cdisc-express-a-glance
 [4]: http://cdiscsupport.clinovo.com/
 []: http://dl.dropbox.com/u/69732603/clip_image0024.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image0034.gif
 []: http://dl.dropbox.com/u/69732603/TobeContinued.jpg