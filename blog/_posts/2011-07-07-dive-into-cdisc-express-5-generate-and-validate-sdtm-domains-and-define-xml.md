---
author: Jiangtang Hu
title: 'Dive into CDISC Express (5): Generate and Validate SDTM domains and define.xml'
excerpt:
layout: post
category:
  - CDISC
  - SAS
tags:
  - CDISC
  - CDISC Express
  - SAS
post_format: [ ]
---
> [*Dive into CDISC Express (1): Introductory*][1]
> 
> *[Dive into CDISC Express (2): Create a New Study][2]*
> 
> *[Dive into CDISC Express (3): Navigate mapping file][3]*</p> 
> 
> *[Dive into CDISC Express (4): Data manipulation techniques][4]*

A more friendly PDF version of these all CDISC Express series is also available in

> [http://jiangtanghu.com/docs/en/CDISCExpress.pdf][5]

The following tasks, such as generating SDTM domains and define.xml, need just some clicking button work in CDISC Express using a well designed mapping file. Few words needed due to the software.

  
#### **5. Step 3 of 6: Validate mapping file (*Validate\_Mapping\_File.sas*)**

It would be back and forth to design, validate then modify and re-validate the mapping file. And sure finally, you will get all the work done, at least no syntax error (how to avoid semantic errors is upon your domain knowledge). A validated mapping file, named mapping.xls will be copied to **… docMapping file – validated version** from the working file, tmpmaping.xls. You will see 

> The corresponding log file in folder **… log**
> 
> A report in **…resultsMapping Validation**, named Mapping_validation.html

[![validate][7]][7] 

Also the temporary datasets in **…tempdata** and **…temp**:

[![clip_image004][8]][8]

[![clip_image006][9]][9]

#### **6. Step 4 of 6: Generate SDTM datasets **(*generate_SDTM.sas*)

If mapping file is OK, generating SDTM domains is just clicking the button. After submitting the codes, you will see the log file, reports, SDTM datasets and temporary datasets in corresponding folders:

[![SDTM][10]][10] 

##### **7. Step 5 of 6: Validate SDTM datasets **(*Validate\_SDTM\_Domains.sas*)

The outputs files of validating SDTM datasets are all located in **C:Program FilesCDISC ExpressSDTM Validation**:

[![clip_image010][11]][11]

##### **8. Step 6 of 6: Generate Define.xml and xpt **(*generate_Definexml.sas*)

Get the final define.xml file and SAS transport files (.xpt):

[![clip_image012][12]][12]

### 9. Recommended reading and action taken

For a quick start and deep understanding, you could read the official documentations in the following sequence:

**C:Program FilesCDISC ExpressdocumentationFAQ.htm**

**C:Program FilesCDISC ExpressdocumentationQuick Start.htm**

**C:Program FilesCDISC ExpressdocumentationUser guide.htm**

A video tutorial would be also helpful:

**C:Program FilesCDISC Expressdocumentationvideotutorial.htm**

A must-read conference paper, *An Excel Framework to Convert Clinical Data to CDISC SDTM Leveraging SAS Technology* by Sophie McCallum and Stephen Chan of Clinovo, supplies a wonderful discussion the architectures of CDISC Express:

<http://www.lexjansen.com/pharmasug/2011/ad/pharmasug-2011-ad08.pdf>

Of course, you do not need to review all the pages then get the confidence to use the software. Learn by doing and just dive into it. There is an opportunity for your practicing and you will also have a change to win an iPad2 from Clinovo’s CDISC Express Contest:

> <http://www.clinovo.com/cdisc/game>

The due day is July 15th and I already submitted my work. That’s fun.

 [1]: http://www.jiangtanghu.com/blog/2011/06/28/dive-into-cdisc-express-1-introductory/
 [2]: http://www.jiangtanghu.com/blog/2011/07/02/dive-into-cdisc-express-2-create-a-new-study/
 [3]: http://www.jiangtanghu.com/blog/2011/07/03/dive-into-cdisc-express-3-navigate-mapping-file/
 [4]: http://www.jiangtanghu.com/blog/2011/07/04/dive-into-cdisc-express-4-data-manipulation-techniques-2/
 [5]: http://jiangtanghu.com/docs/en/CDISCExpress.pdf "http://jiangtanghu.com/docs/en/CDISCExpress.pdf"
 []: http://dl.dropbox.com/u/69732603/validate.png
 []: http://dl.dropbox.com/u/69732603/clip_image0041.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image0061.jpg
 []: http://dl.dropbox.com/u/69732603/SDTM.png
 []: http://dl.dropbox.com/u/69732603/clip_image010.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image012.jpg