---
author: Jiangtang Hu
title: 'Dive into CDISC Express (4): Data manipulation techniques'
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
> *[Dive into CDISC Express (3): Navigate mapping file][3]*

### 4.3 Data manipulation techniques in CDISC Express

CDISC Express supplies relative rich sets of data manipulation techniques assembling with SAS languages used for data mapping. Following is a not limited listing and I will keep it updated.

### 4.3.1 Reference one dataset

A raw dataset name appear in “Dataset” column indicate a “set” operation in SAS.

All dataset options can be used when referencing a dataset, such as

> siteinv(drop=invcode)
> 
> siteinv(rename=(invcode=inv))
> 
> siteinv(where=(invcode ne “”))

You can also reference an external dataset. You should incorporate the external file in spreadsheet with name beginning with an underscore, “\_”, and “\_visits” in this case:

[![clip_image001][5]][5]

Then you can use it in any domains needed, e.g., TV domain:

[![clip_image003][6]][6]

There is a macro %cpd_importlist used to import the external dataset, “_visits”. Again, this macro roots in **C:Program FilesCDISC Expressmacrosfunction_library**.

Using a macro call to re-sharp or modify an input dataset offers great flexibility referencing data. We will also discuss the benefits later on.

### 4.3.2 Assignment

You can assign a number, string and a dataset variable with any valid SAS functions to a SDTM domain variable in “Expression” column. 

Sometimes a temporary variable needed for later calculation. You can produce such temporary variable in “Dataset” column with an assignment in the “Expression” column just similar with any other domain variables. Two differences: first, such temporary variables named begin with an asterisk, “*”; second, all temporary variables will not be included in the final domain. Once created, such temporary variables can be used for any other expressions.

[![clip_image005][7]][7]

There are three special symbols used in “Dataset” column of CDISC Express. Asterisk, “*” indicates a temporary variable, while other two are 

> Tilde, “~” : indicate a variable used for supplemental domain (SUPPQUAL).
> 
> Number sign, “#”: indicate a variable used for comments domain (CO).

Another symbol, at sign, “@”, used in “Expression” column, indicated referencing a variables produced before:

[![clip_image006][8]][8]

In this case, “AGEU” uses “AGE” as input, while “AGE” is calculated before. “@AGE” just indicates the dependency. In concept, it looks like the “calculated” option in SAS PROC SQL:

> **proc** **sql** ;
> 
> select (AvgHigh – **32**) * **5**/**9** as HighC , 
> 
> (AvgLow – **32**) * **5**/**9** as LowC ,
> 
> (calculated HighC – calculated LowC)
> 
> as Range 
> 
> from temps;
> 
> **quit**;

### 4.3.3 Match-merging

We already got a math-merging example before. If “all” appears as a dataset in the “Dataset” column, all the previous datasets should be merged first for later processing by the common key specified in “Merge Key” column. If no key assigned, patient ID is used by the system.

CDISC Express also supports two types of join, inner join and outer join (left, right, full) using data steps. The implementation has slightly difference with standard SQL, but the ideas are same.

We add a new column, “Join”, usually beside the “Merge Key” column.

[![clip_image008][9]][9]

There are two values for “Join”, “O” or “I” while “O” stands for “outer join” and “I”, “inner join”. A join indicator “I” equals a dataset option “in=” in action while “O” means no. Use the above as illustration, the corresponding SAS codes behind look like

> **data** temp;
> 
> merge demog(in=a) siteinv(in=b);
> 
> by sitecode;
> 
> if b;
> 
> **run**;

This is so called “right outer join”. The combination of “I” and “O” in these two datasets can perform all the four types of join, one inner join and three outer join: 

[![in][10]][10] 

As we could see, if no “Join” column specified, CDISC Express will perform inner join by default.

So far CDISC Express cannot support multiply merge keys. For example, the following file is illegal currently: 

 











| **Dataset ** | **Merge Key** |
||
| arm          | siteid, grpno |
| armdescri    | siteid, grpno |

The developer Romain indicated that such enhancements would be raised to the next round of product road map and he also proposed a work around. To use multiple keys for merging, we can create a temporary variable holding such multiple keys as a concatenation then this temporary variable can be used as a single merging key.

### 4.3.4 Concatenating

Above we discussed lots about “merge” operation in CDISC Express. This section dedicated for “set” operation. We already know how to “set” one dataset for referencing, but how to “set” multiple datasets, i.e, “Concatenating”?

Symmetrically, an “all” appears in “Dataset” column indicating merging operation, an “all (stack)” indicates concatenating operation:

[![clip_image014][11]][11]

The above file can be also translated to SAS codes for better understanding:

  
> **data** height;
> 
> set vtsigns(where=(height ne **.**));
> 
> VSTESTCD="HEIGHT";
> 
> VSTEST ="Height";
> 
> VSORRES =put(height,best12.);
> 
> VSORRESU="cm";
> 
> VSSTRESC=put(height,best12.);
> 
> VSSTRESN=height;
> 
> VSSTRESU="cm";
> 
> **run**;
> 
> **data** weight;
> 
> set vtsigns(where=(weight ne **.**));
> 
> VSTESTCD="WEIGHT";
> 
> VSTEST ="Weight";
> 
> VSORRES =put(weight,best12.);
> 
> VSORRESU="kg";
> 
> VSSTRESC=put(weight,best12.);
> 
> VSSTRESN=weight;
> 
> VSSTRESU="cm";
> 
> **run**;
> 
> **data** vs;
> 
> set height weight;
> 
> STUDYID =study;
> 
> DOMAIN =&domain;
> 
> USUBJID =%***CONCATENATE***(_variables=study sitecode patid);
> 
> VSSEQ =%***SEQUENCE***();
> 
> **.** **.** **.**
> 
> run;

4.3.5 Transpose

Clinical SAS programmers do lots of transpose operation to re-sharp the raw data to fit the CDISC standards. Currently there is no explicit guide in CDISC Express on how to transpose, but this is not the end of story.

There are two types of transpose:

[![clip_image016][12]][12]

> Type I: from a wide dataset (more variables, less observations) to a long dataset (less variables, more observations), e.g. transposing a one-row-per-subject datasets to a multiple-row-per-subject dataset 

[![clip_image018][13]][13]

> Type II: from a long dataset (less variables, more observations) to a wide dataset (more variables, less observations), e.g. transposing a multiple-row-per-subject dataset to a one-row-per-subject datasets

As good practices, in SAS we always use data steps with “output” statement to perform type I transpose and use PROC TRANSPOSE for type II. Although CDISC Express doesn’t support transpose operation in an explicit way, at least you can perform type I transpose and surprisingly we already saw it before!

Just back to section of concatenating. The example is taken from **C:Program FilesCDISC Expressstudiesexample2.**

We can see the input data vtsigns is typical wide table (more variables, less observations):

[![clip_image021][14]][14]

And the final domain VS is a typical long table (less variables, more observations):

[![clip_image023][15]][15]

So obviously, such concatenating operation just did a wonderful type I transpose, from a wide table to a long table! More often, the compact SAS codes for type I transpose look like:

> **data** vs;
> 
> set vtsigns;
> 
> if height ne **.** then do;
> 
> VSTESTCD="HEIGHT";
> 
> VSTEST ="Height";
> 
> VSORRES =put(height,best12.);
> 
> VSORRESU="cm";
> 
> VSSTRESC=put(height,best12.);
> 
> VSSTRESN=height;
> 
> VSSTRESU="cm";
> 
> output;
> 
> end;
> 
> if weight ne **.** then do;
> 
> VSTESTCD="WEIGHT";
> 
> VSTEST ="Weight";
> 
> VSORRES =put(weight,best12.);
> 
> VSORRESU="kg";
> 
> VSSTRESC=put(weight,best12.);
> 
> VSSTRESN=weight;
> 
> VSSTRESU="cm";
> 
> output;
> 
> end;
> 
> **.** **.** **.**
> 
> run;

### 4.3.6 All others: use macro!

Now we discussed almost all the common data derivation techniques in programmers’ daily life and the corresponding implementation in CDISC Express. At least we have one question unsolved: how to perform type II transpose, i.e. from a long table to a wide table?

It would be an open question for the developers of the application. But we can also solve this problem in current framework: use macro, customized macro. You can use macros in “Expression” and “Dataset” column. Macro used in “Dataset” column returns a dataset, while macro in “Expression” column returns series of string: that’s the basic structure you should consider when customize your own macros. For more, you can reference the macros in **C:Program FilesCDISC Expressmacrosfunction_library**. For example, &concatenate used in “Expression” column; &cpd_importlist in “Dataset” column.

So it would be convenient to create temporary datasets using macros imbedded type II transpose operation in “Dataset” column. Every thing SAS can do, you can also implement it in CDISC Express. Just use macros, in “Expression” and “Dataset” column accordingly.****

The raw data varies according to trial design and clinical data capture system and procedures. It is impossible and impractical to anticipate the CDISC SDTM converter such as CDISC Express to map all the data just clicking a button. The introducing of CDISC Express doesn’t keep programmers away. It just keeps most of the trivial work away from programmers’ daily life and let them more concentrated on creative work and be productive and efficient.

Following would be the close of such pages.

[![TobeContinued][16]][16]

 [1]: http://www.jiangtanghu.com/blog/2011/06/28/dive-into-cdisc-express-1-introductory/
 [2]: http://www.jiangtanghu.com/blog/2011/07/02/dive-into-cdisc-express-2-create-a-new-study/
 [3]: http://www.jiangtanghu.com/blog/2011/07/03/dive-into-cdisc-express-3-navigate-mapping-file/
 []: http://dl.dropbox.com/u/69732603/clip_image001.gif
 []: http://dl.dropbox.com/u/69732603/clip_image003.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image005.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image006.gif
 []: http://dl.dropbox.com/u/69732603/clip_image008.jpg
 []: http://dl.dropbox.com/u/69732603/in.png
 []: http://dl.dropbox.com/u/69732603/clip_image014.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image016.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image018.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image021.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image023.jpg
 []: http://dl.dropbox.com/u/69732603/TobeContinued2.jpg