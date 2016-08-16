---
id: 266
title: 'Dive into CDISC Express (3): Navigate mapping file'
date: 2011-07-03T21:19:18+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/07/03/dive-into-cdisc-express-3-navigate-mapping-file/
permalink: /2011/07/03/dive-into-cdisc-express-3-navigate-mapping-file/
categories:
  - CDISC
  - SAS
tags:
  - CDISC
  - CDISC Express
  - SAS
---
> <a href="http://www.jiangtanghu.com/blog/2011/06/28/dive-into-cdisc-express-1-introductory/" target="_blank"><em>Dive into CDISC Express (1): Introductory</em></a>
> 
> <a href="http://www.jiangtanghu.com/blog/2011/07/02/dive-into-cdisc-express-2-create-a-new-study/" target="_blank">Dive into CDISC Express (2): Create a New Study</a>

## 4. Step 2 of 6: Generate mapping file

Generating template (blank) mapping file only needs pieces of effort by submitting _generate\_mapping\_template.sas_. The toughest one is to fill it with mapping rules according to specified study.

### 4.1 Get the blank template mapping file (generate\_mapping\_template.sas)

To get the blank template mapping file, just fill the one line of macro call in generate\_mapping\_template.sas:

> <font face="Courier New">%createmapping(filespec=SDTM_Specs_3_1_1.xls, Dom=CM AE TV, req=YES, perm=YES, exp=YES);</font>

Also, you can specify SDTM implementation version, 3.1.1 or 3.1.2. For domains (&Dom), DM, CO and SUPPQUAL will be created automatically; you should list others accordingly:

> SDTM 3.1.1: SV CM EX AE DS MH DV EG IE LB PE QS SC VS TV TI XD SU XR XS XE TR (Total: 22)
> 
> SDTM 3.1.2: AE CE CM DA DS DV EG EX FA IE LB MB MH MS PC PE PP QS SC SE SU SV TA TE TI TS TV VS (Total: 28)

You should also choose the “CORE” variable (REQUIRED, PERMISSIBLE and EXPECTED) by triggering &req, &perm, and &exp to “YES” or “NO”. Note that

> REQUIRED and EXPECTED variables must always be included (req=YES, exp=YES);
> 
> PERMISSIBLE variables included if needed (perm=YES or perm=NO)

Submit _generate\_mapping\_template.sas_ and you can get a blank template mapping file tmpmapping.xls in **C:Program FilesCDISC Expresstemp**. 

[<img style="border-right-width: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; margin-left: 0px; border-left-width: 0px; margin-right: 0px" title="clip_image002" border="0" alt="clip_image002" align="left" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image002_thumb.jpg" width="478" height="436" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image002.jpg)

Copy it to **C:Program FilesCDISC ExpressstudiesCLINCAPdocMapping file &#8211; working version** for example used for study “CLINCAP” and then fill all the blank columns (it NEEDS efforts!). 

If this mapping file passes the validation process, a final version named mapping.xls will be copied automatically to **C:Program FilesCDISC ExpressstudiesCLINCAPdocMapping file &#8211; validated version** for later processing.

Note that if you already have some validated mapping file for other studies, it would serve as a good start rather than using the blank template from the scratch.

## 4.2 Navigate mapping file

Let’s take a look at the “real” worked mapping file for a demo study first, in **C:Program FilesCDISC Expressstudiesexample1docMapping file &#8211; working version**.

The first sheet is a welcome dashboard:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image004" border="0" alt="clip_image004" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image004_thumb.jpg" width="498" height="292" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image004.jpg)

Then StudyMetadata sheet, a XML metadata specification used to generate define.xml. you need only add some information in “Values” column:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image006" border="0" alt="clip_image006" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image006_thumb.jpg" width="491" height="377" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image006.jpg)

The FORMAT sheet:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image007" border="0" alt="clip_image007" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image007_thumb.gif" width="501" height="324" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image007.gif)

Such format structure is similar with the one we export the format from a format catalog using

> <font face="Courier New"><b>proc</b> <b>format</b> library=library cntlout=format_out;</font>
> 
> <font face="Courier New"><b>run</b>;</font>

In most production environment, programmers get formats from clinical data management group. If the entire formats are assigned into proper libraries (work or library), you don’t need to export such formats into this spreadsheet. Of course in the format sheet, you can type some customized format.

A typical domain sheet (AT LAST!) that needs efforts and our understanding of the software, DM for example:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image009" border="0" alt="clip_image009" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image009_thumb.jpg" width="480" height="439" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image009.jpg)

From the ‘Dataset’ column, three raw datasets from **C:Program FilesCDISC Expressstudiesexample1source** needed to map into DM domain, demog, siteinv and eligassess. Note that you can use any data step options such as drop=, rename=, where= for the input datasets.

At the last of ‘Dataset’ column, “all” indicates that all the previous datasets mentioned above should be merged together for final processing. 

In the ‘Merge Key’ column, ‘sitecode’ is designed to datasets demog and siteinv which means demog and siteinv should be merged by the common key, ‘sitecode’. 

As we mentioned, all the previous datasets should be merged at last. But there is no common key settled in the ‘Merge Key’ column. It is a common rule: if no key specified for merge, USUBJID is used by default.

The third column is ‘CDISC variable’, which list all the needed variables according to implementation version. An important note: you do not need to implement all the variables according to the order as they appear in the blank template mapping file. In the previous blank file, “AGE” in DM domain is ordered in Line 12, but in this working file, “AGE” is calculated in the second last order. The variable order of final DM domain will be as same as the blank one. 

It makes sense in practice. For example, the sequential variable, e.g. AESEQ is ordered after USUBJID, but you can only get the sequential number when all other variables well done. So SEQ variables are always computed in the final stage in a working mapping file.

“Expression” column specify the mapping rule from raw datasets to SDTM domains. Assignments, expressions and macro calls (rooted in **C:Program FilesCDISC Expressmacrosfunction_library**) are allowed in this column and most of them are straightforward. We will discuss more in the following section.

Sum up, we can “translate” this mapping sheet to SAS codes for better understanding of CDISC Express architecture: 

<!--more-->


  


> data tem1;
> 
> &#160;&#160;&#160; set demog;
> 
> &#160;&#160;&#160; STUDYID=study;
> 
> &#160;&#160;&#160; DOMAIN =&domain;
> 
> &#160;&#160;&#160; USUBJID=%CONCATENATE(_variables=study sitecode patid);
> 
> &#160;&#160;&#160; SUBJID =patid;
> 
> RFSTDTC=%D\_RFST(\_dataset=trtinf,\_date=trtinfdt,\_key=patid,\_ivrsds=ivrs,\_ivrsdt=randdat);
> 
> RFENDTC=%SORTLOOKUP(\_dataset=disc,\_variable=fupdat,\_key=patid,\_sort\_variable=fupdat,\_keep=last);
> 
> &#160;&#160;&#160; SITEID =sitecode;
> 
> &#160;&#160;&#160; INVID =invcode;
> 
> &#160;&#160; BRTHDTC=%FORMAT(\_variable=brthdat,\_format=yymmdd10);
> 
> &#160;&#160; SEX =%GENDER(_gender=sex);
> 
> &#160;&#160; RACE =%D_RACE();
> 
> &#160;&#160; ETHNIC =upcase(ethnic);
> 
> &#160;&#160; COUNTRY="USA";
> 
> &#160;&#160;&#160; DMDTC =%FORMAT(\_variable=formdat,\_format=yymmdd10);
> 
> &#160;&#160; ARMCD ="";
> 
> &#160;&#160;&#160; ARM ="";
> 
> run;
> 
> &#160;
> 
> data tem2;
> 
> &#160;&#160;&#160; merge tem1 siteinv(drop=invcode);
> 
> &#160;&#160;&#160; by sitecode;
> 
> &#160;&#160;&#160; INVNAM=trim(lname)||","||fname;
> 
> run;
> 
> &#160;
> 
> data dm;
> 
> &#160;&#160;&#160; merge tem2 eligassess;
> 
> &#160;&#160;&#160; by patid;
> 
> &#160; AGE =year(infcondt)-year(brthdat)-(month(brthdat)>month(infcondt))-(month(brthdat)=month(infcondt) and day(brthdat)>day(infcondt));
> 
> AGEU=%CONVERTIF([\_if\_variable=@AGE,\_if\_value=.,\_then\_value](mailto:_if_variable=@AGE,_if_value=.,_then_value)=, \_else\_value=YEARS);
> 
> run;

Following will be some explore the data manipulation techniques in CDISC Express, such as merge, transpose.

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="TobeContinued" border="0" alt="TobeContinued" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/TobeContinued_thumb1.jpg" width="246" height="187" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/TobeContinued1.jpg)