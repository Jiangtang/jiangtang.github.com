---
id: 311
title: 'Dive into CDISC Express (5): Generate and Validate SDTM domains and define.xml'
date: 2011-07-07T22:32:03+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/07/07/dive-into-cdisc-express-5-generate-and-validate-sdtm-domains-and-define-xml/
permalink: /2011/07/07/dive-into-cdisc-express-5-generate-and-validate-sdtm-domains-and-define-xml/
categories:
  - CDISC
  - SAS
tags:
  - CDISC
  - CDISC Express
  - SAS
---
> [_Dive into CDISC Express (1): Introductory_](http://www.jiangtanghu.com/blog/2011/06/28/dive-into-cdisc-express-1-introductory/)
> 
> _[Dive into CDISC Express (2): Create a New Study](http://www.jiangtanghu.com/blog/2011/07/02/dive-into-cdisc-express-2-create-a-new-study/)_
> 
> _[Dive into CDISC Express (3): Navigate mapping file](http://www.jiangtanghu.com/blog/2011/07/03/dive-into-cdisc-express-3-navigate-mapping-file/)_</p> 
> 
> _<a href="http://www.jiangtanghu.com/blog/2011/07/04/dive-into-cdisc-express-4-data-manipulation-techniques-2/" target="_blank">Dive into CDISC Express (4): Data manipulation techniques</a>_

A more friendly PDF version of these all CDISC Express series is also available in

> [http://jiangtanghu.com/docs/en/CDISCExpress.pdf](http://jiangtanghu.com/docs/en/CDISCExpress.pdf "http://jiangtanghu.com/docs/en/CDISCExpress.pdf")

The following tasks, such as generating SDTM domains and define.xml, need just some clicking button work in CDISC Express using a well designed mapping file. Few words needed due to the software.

<!--more-->


  


#### **5. Step 3 of 6: Validate mapping file (_Validate\_Mapping\_File.sas_)**

It would be back and forth to design, validate then modify and re-validate the mapping file. And sure finally, you will get all the work done, at least no syntax error (how to avoid semantic errors is upon your domain knowledge). A validated mapping file, named mapping.xls will be copied to **&#8230; docMapping file &#8211; validated version** from the working file, tmpmaping.xls. You will see 

> The corresponding log file in folder **&#8230; log**
> 
> A report in **…resultsMapping Validation**, named Mapping_validation.html

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="validate" border="0" alt="validate" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/validate_thumb.png" width="499" height="281" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/validate.png) 

Also the temporary datasets in **…tempdata** and **…temp**:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image004" border="0" alt="clip_image004" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image004_thumb1.jpg" width="497" height="189" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0041.jpg)

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image006" border="0" alt="clip_image006" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image006_thumb1.jpg" width="496" height="313" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0061.jpg)

#### **6. Step 4 of 6: Generate SDTM datasets** (_generate_SDTM.sas_)

If mapping file is OK, generating SDTM domains is just clicking the button. After submitting the codes, you will see the log file, reports, SDTM datasets and temporary datasets in corresponding folders:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="SDTM" border="0" alt="SDTM" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/SDTM_thumb.png" width="506" height="483" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/SDTM.png) 

##### **7. Step 5 of 6: Validate SDTM datasets** (_Validate\_SDTM\_Domains.sas_)

The outputs files of validating SDTM datasets are all located in **C:Program FilesCDISC ExpressSDTM Validation**:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image010" border="0" alt="clip_image010" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image010_thumb.jpg" width="500" height="377" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image010.jpg)

##### **8. Step 6 of 6: Generate Define.xml and xpt** (_generate_Definexml.sas_)

Get the final define.xml file and SAS transport files (.xpt):

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image012" border="0" alt="clip_image012" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image012_thumb.jpg" width="502" height="402" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image012.jpg)

### 9. Recommended reading and action taken

For a quick start and deep understanding, you could read the official documentations in the following sequence:

**C:Program FilesCDISC ExpressdocumentationFAQ.htm**

**C:Program FilesCDISC ExpressdocumentationQuick Start.htm**

**C:Program FilesCDISC ExpressdocumentationUser guide.htm**

A video tutorial would be also helpful:

**C:Program FilesCDISC Expressdocumentationvideotutorial.htm**

A must-read conference paper, _An Excel Framework to Convert Clinical Data to CDISC SDTM Leveraging SAS Technology_ by Sophie McCallum and Stephen Chan of Clinovo, supplies a wonderful discussion the architectures of CDISC Express:

<http://www.lexjansen.com/pharmasug/2011/ad/pharmasug-2011-ad08.pdf>

Of course, you do not need to review all the pages then get the confidence to use the software. Learn by doing and just dive into it. There is an opportunity for your practicing and you will also have a change to win an iPad2 from Clinovo’s CDISC Express Contest:

> <http://www.clinovo.com/cdisc/game>

The due day is July 15<sup>th</sup> and I already submitted my work. That’s fun.