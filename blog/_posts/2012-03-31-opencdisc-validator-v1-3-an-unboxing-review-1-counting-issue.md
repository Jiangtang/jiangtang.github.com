---
author: Jiangtang Hu
title: 'OpenCDISC Validator V1.3: An Unboxing Review (1): counting issue'
excerpt:
layout: post
category:
  - CDISC
  - SAS
  - XML
tags:
  - CDISC
  - OpenCDISC
  - SAS
  - Validation
  - XML
post_format: [ ]
---
 
The lasted [OpenCDISC][1] Validator version 1.3 was released at 29 March, 2012 (btw, there is a typo in the Line 1 of *CHANGELOG.txt* within the package: “2012” not “2011”). [As usual][2], you can submit the following SAS scripts to get some basic information(remember to customize your directory):

> filename CDISC url "[https://raw.github.com/Jiangtang/Programming-SAS/master/Rules\_Count\_OpenCDISC_XML.sas";][3]
> 
> %include CDISC;
> 
> %Rules\_Count\_OpenCDISC\_XML(dir=C:OpenCDISC1.3compareopencdisc-validator\_1.3config)

and you get a summary of validation rules of OpenCDISC Validator V1.3 (**499** total unique rules):

[![OpenCDISC_V1.3][5]][5]

where

> AD: Analytical Data   
> CT: Controlled Terminology   
> DD: Data Definition   
> OD: Operation Data Model   
> SD: Study Data   
> SE: [SEND][5] data 

As comparison, a summary of V1.2.1 (**385** total unique rules) posted before:

![][6]

The most significant enhancement of V1.3 against V1.2.1 is the adding of rules for [SDTM 3.1.2 with Amendment 1][7] and [SEND 3.0][5]. You can see there are also some changes among others modules, such ADaM 1.0 and SDTM 3.1.2. The OpenCDISC release newsletter said that there are **43** new SDTM rules added. Well, rules deleted, rules added, rules commented, we now have some arithmetical discrepancies. 

The scripts above capture all instances of validation rule IDs (also delete some commented for example in *config-**define**-1.0.xml*, four rules commented: OD0004, OD0005, OD0007, OD0008). We can also double validate the counts manually: 

*   copy all contents for example in [SDTM 3.1.2][8] in its website into Notepad++ (where line numbers displayed) 
*   delete all unnecessary entries 
*   then the last line number is the total number of the rules (227 in this case).

Another way to check the rules is to [open the XML configuration files using a web browser][9]:

![][10]

Theoretically the three ways are identical in counting, but there is an open bug in the style sheet file in …OpenCDISC1.3opencdisc-validatorconfigresourcesxsl**config.xsl**, Line 175:

> <xsl:template match="val:Unique|val:Condition|val:Match|val:Regex
> 
> |val:Required|val:Lookup|val:Metadata">

There is no “val:Find” to render all the Find validation rules (AD0061 in config-**adam**-1.0.xml) so all Find validators are not displayed. A suggested workaround is just to add “val:Find” to the file:

> <xsl:template match="val:Unique|val:Condition|val:Match|val:Regex
> 
> |val:Required|val:Lookup|val:Metadata|val:Find">

Actually in the “*[OpenCDISC Validation Framework][11]*” page of OpenCDISC website, the “Find”validator is not [documented][12] yet. 

<*to be continued*>

</font>

 [1]: http://www.opencdisc.org
 [2]: http://www.jiangtanghu.com/blog/2012/02/19/github-and-weekend-programming/
 [3]: https://raw.github.com/Jiangtang/Programming-SAS/master/Rules_Count_OpenCDISC_XML.sas";
 []: http://dl.dropbox.com/u/69732603/OpenCDISC_V1.3.png
 [5]: http://www.cdisc.org/send
 [6]: http://dl.dropbox.com/u/69732603/OC_by_model.png
 [7]: http://www.cdisc.org/stuff/contentmgr/files/0/3fa5f30f40ce5ecc7b3f91e558b55f73/misc/amendment_1_to_study_data_tabulation_model_v1_2_and_sdtmig_v3_1_2_final_2011_12_14.pdf
 [8]: http://www.opencdisc.org/projects/validator/cdisc-sdtm-3.1.2-validation-rules
 [9]: http://www.jiangtanghu.com/blog/2012/02/11/xml/
 [10]: http://dl.dropbox.com/u/69732603/XML_IE1.png
 [11]: http://www.opencdisc.org/projects/validator/opencdisc-validation-framework#validation-rules
 [12]: http://www.jiangtanghu.com/blog/2012/02/29/not-documented-not-exist/