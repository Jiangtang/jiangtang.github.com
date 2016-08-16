---
id: 292
title: 'Dive into CDISC Express (4): Data manipulation techniques'
date: 2011-07-04T20:52:42+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/07/04/dive-into-cdisc-express-4-data-manipulation-techniques-2/
permalink: /2011/07/04/dive-into-cdisc-express-4-data-manipulation-techniques-2/
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
> _<a href="http://www.jiangtanghu.com/blog/2011/07/02/dive-into-cdisc-express-2-create-a-new-study/" target="_blank">Dive into CDISC Express (2): Create a New Study</a>_
> 
> _<a href="http://www.jiangtanghu.com/blog/2011/07/03/dive-into-cdisc-express-3-navigate-mapping-file/" target="_blank">Dive into CDISC Express (3): Navigate mapping file</a>_

### 4.3 Data manipulation techniques in CDISC Express

CDISC Express supplies relative rich sets of data manipulation techniques assembling with SAS languages used for data mapping. Following is a not limited listing and I will keep it updated.

### 4.3.1 Reference one dataset

A raw dataset name appear in “Dataset” column indicate a “set” operation in SAS.

All dataset options can be used when referencing a dataset, such as

> <font face="Courier New">siteinv(drop=invcode)</font>
> 
> <font face="Courier New">siteinv(rename=(invcode=inv))</font>
> 
> <font face="Courier New">siteinv(where=(invcode ne “”))</font>

You can also reference an external dataset. You should incorporate the external file in spreadsheet with name beginning with an underscore, “\_”, and “\_visits” in this case:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image001" border="0" alt="clip_image001" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image001_thumb.gif" width="434" height="302" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image001.gif)

Then you can use it in any domains needed, e.g., TV domain:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image003" border="0" alt="clip_image003" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image003_thumb.jpg" width="493" height="244" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image003.jpg)

There is a macro <font color="#ff0000">%cpd_importlist</font> used to import the external dataset, “_visits”. Again, this macro roots in **C:Program FilesCDISC Expressmacrosfunction_library**.

Using a macro call to re-sharp or modify an input dataset offers great flexibility referencing data. We will also discuss the benefits later on.

### 4.3.2 Assignment

You can assign a number, string and a dataset variable with any valid SAS functions to a SDTM domain variable in “Expression” column. 

Sometimes a temporary variable needed for later calculation. You can produce such temporary variable in “Dataset” column with an assignment in the “Expression” column just similar with any other domain variables. Two differences: first, such temporary variables named begin with an asterisk, “*”; second, all temporary variables will not be included in the final domain. Once created, such temporary variables can be used for any other expressions.

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image005" border="0" alt="clip_image005" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image005_thumb.jpg" width="494" height="312" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image005.jpg)

There are three special symbols used in “Dataset” column of CDISC Express. Asterisk, “*” indicates a temporary variable, while other two are 

> Tilde, “~” : indicate a variable used for supplemental domain (SUPPQUAL).
> 
> Number sign, “#”: indicate a variable used for comments domain (CO).

Another symbol, at sign, “@”, used in “Expression” column, indicated referencing a variables produced before:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image006" border="0" alt="clip_image006" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image006_thumb.gif" width="448" height="104" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image006.gif)

In this case, “AGEU” uses “AGE” as input, while “AGE” is calculated before. “@AGE” just indicates the dependency. In concept, it looks like the “calculated” option in SAS PROC SQL:

> <font face="Courier New"><b>proc</b> <b>sql</b> ;</font>
> 
> <font face="Courier New">select (AvgHigh &#8211; <b>32</b>) * <b>5</b>/<b>9</b> as HighC , </font>
> 
> <font face="Courier New">(AvgLow &#8211; <b>32</b>) * <b>5</b>/<b>9</b> as LowC ,</font>
> 
> <font face="Courier New">(calculated HighC &#8211; calculated LowC)</font>
> 
> <font face="Courier New">as Range </font>
> 
> <font face="Courier New">from temps;</font>
> 
> <font face="Courier New"><b>quit</b>;</font>

### 4.3.3 Match-merging

We already got a math-merging example before. If “all” appears as a dataset in the “Dataset” column, all the previous datasets should be merged first for later processing by the common key specified in “Merge Key” column. If no key assigned, patient ID is used by the system.

CDISC Express also supports two types of join, inner join and outer join (left, right, full) using data steps. The implementation has slightly difference with standard SQL, but the ideas are same.

We add a new column, “Join”, usually beside the “Merge Key” column.

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image008" border="0" alt="clip_image008" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image008_thumb.jpg" width="442" height="377" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image008.jpg)

There are two values for “Join”, “O” or “I” while “O” stands for “outer join” and “I”, “inner join”. A join indicator “I” equals a dataset option “in=” in action while “O” means no. Use the above as illustration, the corresponding SAS codes behind look like

> <font face="courier new"><b>data</b> temp;</font>
> 
> <font face="courier new">merge demog(in=a) siteinv(in=b);</font>
> 
> <font face="courier new">by sitecode;</font>
> 
> <font face="courier new">if b;</font>
> 
> <font face="courier new"><b>run</b>;</font>

This is so called “right outer join”. The combination of “I” and “O” in these two datasets can perform all the four types of join, one inner join and three outer join: 

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="in" border="0" alt="in" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/in_thumb.png" width="499" height="313" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/in.png)&#160;

As we could see, if no “Join” column specified, CDISC Express will perform inner join by default.

So far CDISC Express cannot support multiply merge keys. For example, the following file is illegal currently: 

&#160;

<p align="center">
  <table border="1" cellspacing="0" cellpadding="0">
    <tr>
      <td valign="top" width="138">
        <p>
          <b>Dataset </b>
        </p>
      </td>
      
      <td valign="top" width="203">
        <p>
          <b>Merge Key</b>
        </p>
      </td>
    </tr>
    
    <tr>
      <td valign="top" width="138">
        <p>
          arm&#160;&#160;&#160;
        </p>
      </td>
      
      <td valign="top" width="203">
        <p>
          siteid, grpno
        </p>
      </td>
    </tr>
    
    <tr>
      <td valign="top" width="138">
        <p>
          armdescri
        </p>
      </td>
      
      <td valign="top" width="203">
        <p>
          siteid, grpno
        </p>
      </td>
    </tr>
  </table>
  
  <p>
    The developer Romain indicated that such enhancements would be raised to the next round of product road map and he also proposed a work around. To use multiple keys for merging, we can create a temporary variable holding such multiple keys as a concatenation then this temporary variable can be used as a single merging key.
  </p>
  
  <h3>
    4.3.4 Concatenating
  </h3>
  
  <p>
    Above we discussed lots about “merge” operation in CDISC Express. This section dedicated for “set” operation. We already know how to “set” one dataset for referencing, but how to “set” multiple datasets, i.e, “Concatenating”?
  </p>
  
  <p>
    Symmetrically, an “all” appears in “Dataset” column indicating merging operation, an “all (stack)” indicates concatenating operation:
  </p>
  
  <p>
    <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image014.jpg"><img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image014" border="0" alt="clip_image014" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image014_thumb.jpg" width="493" height="396" /></a>
  </p>
  
  <p>
    The above file can be also translated to SAS codes for better understanding:
  </p>
  
  <p>
    <!--more-->
    
    <br /> 
    
    <blockquote>
      <p>
        <a name="OLE_LINK2"></a><a name="OLE_LINK1"><b><font face="Courier New">data</font></b></a><font face="Courier New"> height;</font>
      </p>
      
      <p>
        <font face="Courier New">set vtsigns(where=(height ne <b>.</b>));</font>
      </p>
      
      <p>
        <font face="Courier New">VSTESTCD="HEIGHT";</font>
      </p>
      
      <p>
        <font face="Courier New">VSTEST ="Height";</font>
      </p>
      
      <p>
        <font face="Courier New">VSORRES =put(height,best12.);</font>
      </p>
      
      <p>
        <font face="Courier New">VSORRESU="cm";</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESC=put(height,best12.);</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESN=height;</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESU="cm";</font>
      </p>
      
      <p>
        <font face="Courier New"><b>run</b>;</font>
      </p>
      
      <p>
        <font face="Courier New"><b>data</b> weight;</font>
      </p>
      
      <p>
        <font face="Courier New">set vtsigns(where=(weight ne <b>.</b>));</font>
      </p>
      
      <p>
        <font face="Courier New">VSTESTCD="WEIGHT";</font>
      </p>
      
      <p>
        <font face="Courier New">VSTEST ="Weight";</font>
      </p>
      
      <p>
        <font face="Courier New">VSORRES =put(weight,best12.);</font>
      </p>
      
      <p>
        <font face="Courier New">VSORRESU="kg";</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESC=put(weight,best12.);</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESN=weight;</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESU="cm";</font>
      </p>
      
      <p>
        <font face="Courier New"><b>run</b>;</font>
      </p>
      
      <p>
        <font face="Courier New"><b>data</b> vs;</font>
      </p>
      
      <p>
        <font face="Courier New">set height weight;</font>
      </p>
      
      <p>
        <font face="Courier New">STUDYID =study;</font>
      </p>
      
      <p>
        <font face="Courier New">DOMAIN =&domain;</font>
      </p>
      
      <p>
        <font face="Courier New">USUBJID =%<b><i>CONCATENATE</i></b>(_variables=study sitecode patid);</font>
      </p>
      
      <p>
        <font face="Courier New">VSSEQ =%<b><i>SEQUENCE</i></b>();</font>
      </p>
      
      <p>
        <font face="Courier New"><b>.</b> <b>.</b> <b>.</b></font>
      </p>
      
      <p>
        <font face="Courier New">run;</font>
      </p>
    </blockquote>
    
    <p>
      4.3.5 Transpose
    </p>
    
    <p>
      Clinical SAS programmers do lots of transpose operation to re-sharp the raw data to fit the CDISC standards. Currently there is no explicit guide in CDISC Express on how to transpose, but this is not the end of story.
    </p>
    
    <p>
      There are two types of transpose:
    </p>
    
    <p>
      <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image016.jpg"><img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image016" border="0" alt="clip_image016" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image016_thumb.jpg" width="492" height="207" /></a>
    </p>
    
    <blockquote>
      <p>
        Type I: from a wide dataset (more variables, less observations) to a long dataset (less variables, more observations), e.g. transposing a one-row-per-subject datasets to a multiple-row-per-subject dataset
      </p>
    </blockquote>
    
    <p>
      <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image018.jpg"><img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image018" border="0" alt="clip_image018" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image018_thumb.jpg" width="514" height="224" /></a>
    </p>
    
    <blockquote>
      <p>
        Type II: from a long dataset (less variables, more observations) to a wide dataset (more variables, less observations), e.g. transposing a multiple-row-per-subject dataset to a one-row-per-subject datasets
      </p>
    </blockquote>
    
    <p>
      As good practices, in SAS we always use data steps with “output” statement to perform type I transpose and use PROC TRANSPOSE for type II. Although CDISC Express doesn’t support transpose operation in an explicit way, at least you can perform type I transpose and surprisingly we already saw it before!
    </p>
    
    <p>
      Just back to section of concatenating. The example is taken from <b>C:Program FilesCDISC Expressstudiesexample2.</b>
    </p>
    
    <p>
      We can see the input data vtsigns is typical wide table (more variables, less observations):
    </p>
    
    <p>
      <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image021.jpg"><img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image021" border="0" alt="clip_image021" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image021_thumb.jpg" width="469" height="405" /></a>
    </p>
    
    <p>
      And the final domain VS is a typical long table (less variables, more observations):
    </p>
    
    <p>
      <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image023.jpg"><img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="clip_image023" border="0" alt="clip_image023" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image023_thumb.jpg" width="303" height="662" /></a>
    </p>
    
    <p>
      So obviously, such concatenating operation just did a wonderful type I transpose, from a wide table to a long table! More often, the compact SAS codes for type I transpose look like:
    </p>
    
    <blockquote>
      <p>
        <font face="Courier New"><b>data</b> vs;</font>
      </p>
      
      <p>
        <font face="Courier New">set vtsigns;</font>
      </p>
      
      <p>
        <font face="Courier New">if height ne <b>.</b> then do;</font>
      </p>
      
      <p>
        <font face="Courier New">VSTESTCD="HEIGHT";</font>
      </p>
      
      <p>
        <font face="Courier New">VSTEST ="Height";</font>
      </p>
      
      <p>
        <font face="Courier New">VSORRES =put(height,best12.);</font>
      </p>
      
      <p>
        <font face="Courier New">VSORRESU="cm";</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESC=put(height,best12.);</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESN=height;</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESU="cm";</font>
      </p>
      
      <p>
        <font face="Courier New">output;</font>
      </p>
      
      <p>
        <font face="Courier New">end;</font>
      </p>
      
      <p>
        <font face="Courier New">if weight ne <b>.</b> then do;</font>
      </p>
      
      <p>
        <font face="Courier New">VSTESTCD="WEIGHT";</font>
      </p>
      
      <p>
        <font face="Courier New">VSTEST ="Weight";</font>
      </p>
      
      <p>
        <font face="Courier New">VSORRES =put(weight,best12.);</font>
      </p>
      
      <p>
        <font face="Courier New">VSORRESU="kg";</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESC=put(weight,best12.);</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESN=weight;</font>
      </p>
      
      <p>
        <font face="Courier New">VSSTRESU="cm";</font>
      </p>
      
      <p>
        <font face="Courier New">output;</font>
      </p>
      
      <p>
        <font face="Courier New">end;</font>
      </p>
      
      <p>
        <font face="Courier New"><b>.</b> <b>.</b> <b>.</b></font>
      </p>
      
      <p>
        <font face="Courier New">run;</font>
      </p>
    </blockquote>
    
    <h3>
      4.3.6 All others: use macro!
    </h3>
    
    <p>
      Now we discussed almost all the common data derivation techniques in programmers’ daily life and the corresponding implementation in CDISC Express. At least we have one question unsolved: how to perform type II transpose, i.e. from a long table to a wide table?
    </p>
    
    <p>
      It would be an open question for the developers of the application. But we can also solve this problem in current framework: use macro, customized macro. You can use macros in “Expression” and “Dataset” column. Macro used in “Dataset” column returns a dataset, while macro in “Expression” column returns series of string: that’s the basic structure you should consider when customize your own macros. For more, you can reference the macros in <b>C:Program FilesCDISC Expressmacrosfunction_library</b>. For example, <font color="#ff0000">&concatenate</font> used in “Expression” column; <font color="#ff0000">&cpd_importlist</font> in “Dataset” column.
    </p>
    
    <p>
      So it would be convenient to create temporary datasets using macros imbedded type II transpose operation in “Dataset” column. Every thing SAS can do, you can also implement it in CDISC Express. Just use macros, in “Expression” and “Dataset” column accordingly.<b></b>
    </p>
    
    <p>
      The raw data varies according to trial design and clinical data capture system and procedures. It is impossible and impractical to anticipate the CDISC SDTM converter such as CDISC Express to map all the data just clicking a button. The introducing of CDISC Express doesn’t keep programmers away. It just keeps most of the trivial work away from programmers’ daily life and let them more concentrated on creative work and be productive and efficient.
    </p>
    
    <p>
      Following would be the close of such pages.
    </p>
    
    <p>
      <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/TobeContinued2.jpg"><img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="TobeContinued" border="0" alt="TobeContinued" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/TobeContinued_thumb2.jpg" width="240" height="181" /></a>
    </p>