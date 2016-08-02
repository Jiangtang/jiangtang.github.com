---
author: Jiangtang Hu
title: 'Dive into CDISC Express (3): Navigate mapping file'
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
> [Dive into CDISC Express (2): Create a New Study][2]

## 4. Step 2 of 6: Generate mapping file

Generating template (blank) mapping file only needs pieces of effort by submitting *generate\_mapping\_template.sas*. The toughest one is to fill it with mapping rules according to specified study.

### 4.1 Get the blank template mapping file (generate\_mapping\_template.sas)

To get the blank template mapping file, just fill the one line of macro call in generate\_mapping\_template.sas:

> %createmapping(filespec=SDTM\_Specs\_3\_1\_1.xls, Dom=CM AE TV, req=YES, perm=YES, exp=YES);

Also, you can specify SDTM implementation version, 3.1.1 or 3.1.2. For domains (&Dom), DM, CO and SUPPQUAL will be created automatically; you should list others accordingly:

> SDTM 3.1.1: SV CM EX AE DS MH DV EG IE LB PE QS SC VS TV TI XD SU XR XS XE TR (Total: 22)
> 
> SDTM 3.1.2: AE CE CM DA DS DV EG EX FA IE LB MB MH MS PC PE PP QS SC SE SU SV TA TE TI TS TV VS (Total: 28)

You should also choose the “CORE” variable (REQUIRED, PERMISSIBLE and EXPECTED) by triggering &req, &perm, and &exp to “YES” or “NO”. Note that

> REQUIRED and EXPECTED variables must always be included (req=YES, exp=YES);
> 
> PERMISSIBLE variables included if needed (perm=YES or perm=NO)

Submit *generate\_mapping\_template.sas* and you can get a blank template mapping file tmpmapping.xls in **C:Program FilesCDISC Expresstemp**. 

[![clip_image002][4]][4]

Copy it to **C:Program FilesCDISC ExpressstudiesCLINCAPdocMapping file – working version** for example used for study “CLINCAP” and then fill all the blank columns (it NEEDS efforts!). 

If this mapping file passes the validation process, a final version named mapping.xls will be copied automatically to **C:Program FilesCDISC ExpressstudiesCLINCAPdocMapping file – validated version** for later processing.

Note that if you already have some validated mapping file for other studies, it would serve as a good start rather than using the blank template from the scratch.

## 4.2 Navigate mapping file

Let’s take a look at the “real” worked mapping file for a demo study first, in **C:Program FilesCDISC Expressstudiesexample1docMapping file – working version**.

The first sheet is a welcome dashboard:

[![clip_image004][5]][5]

Then StudyMetadata sheet, a XML metadata specification used to generate define.xml. you need only add some information in “Values” column:

[![clip_image006][6]][6]

The FORMAT sheet:

[![clip_image007][7]][7]

Such format structure is similar with the one we export the format from a format catalog using

> **proc** **format** library=library cntlout=format_out;
> 
> **run**;

In most production environment, programmers get formats from clinical data management group. If the entire formats are assigned into proper libraries (work or library), you don’t need to export such formats into this spreadsheet. Of course in the format sheet, you can type some customized format.

A typical domain sheet (AT LAST!) that needs efforts and our understanding of the software, DM for example:

[![clip_image009][8]][8]

From the ‘Dataset’ column, three raw datasets from **C:Program FilesCDISC Expressstudiesexample1source** needed to map into DM domain, demog, siteinv and eligassess. Note that you can use any data step options such as drop=, rename=, where= for the input datasets.

At the last of ‘Dataset’ column, “all” indicates that all the previous datasets mentioned above should be merged together for final processing. 

In the ‘Merge Key’ column, ‘sitecode’ is designed to datasets demog and siteinv which means demog and siteinv should be merged by the common key, ‘sitecode’. 

As we mentioned, all the previous datasets should be merged at last. But there is no common key settled in the ‘Merge Key’ column. It is a common rule: if no key specified for merge, USUBJID is used by default.

The third column is ‘CDISC variable’, which list all the needed variables according to implementation version. An important note: you do not need to implement all the variables according to the order as they appear in the blank template mapping file. In the previous blank file, “AGE” in DM domain is ordered in Line 12, but in this working file, “AGE” is calculated in the second last order. The variable order of final DM domain will be as same as the blank one. 

It makes sense in practice. For example, the sequential variable, e.g. AESEQ is ordered after USUBJID, but you can only get the sequential number when all other variables well done. So SEQ variables are always computed in the final stage in a working mapping file.

“Expression” column specify the mapping rule from raw datasets to SDTM domains. Assignments, expressions and macro calls (rooted in **C:Program FilesCDISC Expressmacrosfunction_library**) are allowed in this column and most of them are straightforward. We will discuss more in the following section.

Sum up, we can “translate” this mapping sheet to SAS codes for better understanding of CDISC Express architecture: 

  
> data tem1;
> 
>     set demog;
> 
>     STUDYID=study;
> 
>     DOMAIN =&domain;
> 
>     USUBJID=%CONCATENATE(_variables=study sitecode patid);
> 
>     SUBJID =patid;
> 
> RFSTDTC=%D\_RFST(\_dataset=trtinf,\_date=trtinfdt,\_key=patid,\_ivrsds=ivrs,\_ivrsdt=randdat);
> 
> RFENDTC=%SORTLOOKUP(\_dataset=disc,\_variable=fupdat,\_key=patid,\_sort\_variable=fupdat,\_keep=last);
> 
>     SITEID =sitecode;
> 
>     INVID =invcode;
> 
>    BRTHDTC=%FORMAT(\_variable=brthdat,\_format=yymmdd10);
> 
>    SEX =%GENDER(_gender=sex);
> 
>    RACE =%D_RACE();
> 
>    ETHNIC =upcase(ethnic);
> 
>    COUNTRY="USA";
> 
>     DMDTC =%FORMAT(\_variable=formdat,\_format=yymmdd10);
> 
>    ARMCD ="";
> 
>     ARM ="";
> 
> run;
> 
>  
> 
> data tem2;
> 
>     merge tem1 siteinv(drop=invcode);
> 
>     by sitecode;
> 
>     INVNAM=trim(lname)||","||fname;
> 
> run;
> 
>  
> 
> data dm;
> 
>     merge tem2 eligassess;
> 
>     by patid;
> 
>   AGE =year(infcondt)-year(brthdat)-(month(brthdat)>month(infcondt))-(month(brthdat)=month(infcondt) and day(brthdat)>day(infcondt));
> 
> AGEU=%CONVERTIF([\_if\_variable=@AGE,\_if\_value=.,\_then\_value][8]=, \_else\_value=YEARS);
> 
> run;

Following will be some explore the data manipulation techniques in CDISC Express, such as merge, transpose.

[![TobeContinued][10]][10]

 [1]: http://www.jiangtanghu.com/blog/2011/06/28/dive-into-cdisc-express-1-introductory/
 [2]: http://www.jiangtanghu.com/blog/2011/07/02/dive-into-cdisc-express-2-create-a-new-study/
 []: http://dl.dropbox.com/u/69732603/clip_image002.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image004.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image006.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image007.gif
 []: http://dl.dropbox.com/u/69732603/clip_image009.jpg
 [8]: mailto:_if_variable=@AGE,_if_value=.,_then_value
 []: http://dl.dropbox.com/u/69732603/TobeContinued1.jpg