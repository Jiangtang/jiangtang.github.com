---
id: 1305
title: Record Qualifier v.s. Variable Qualifier
date: 2014-03-18T11:00:36+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1305
permalink: /2014/03/18/record-qualifier-v-s-variable-qualifier/
categories:
  - CDISC
tags:
  - CDISC
---
<font size="2">If you think it’s clear enough to differentiate record qualifier from variable qualifier as they were defined (in <em>CDISC SDTM Version 1.3</em>):</font>

> <font size="2"><strong>Record Qualifiers</strong> define additional attributes of the observation record as a whole (rather than describing a particular variable within a record). Examples include &#8211;REASND, AESLIFE, and all other SAE flag variables in the AE domain; AGE, SEX, and RACE in the DM domain; and &#8211;BLFL, &#8211;POS, &#8211;LOC, &#8211;SPEC, and &#8211;NAM in a Findings domain</font>
> 
> <font size="2"><strong>Variable Qualifiers</strong> are used to further modify or describe a specific variable within an observation and are only meaningful in the context of the variable they qualify. Examples include &#8211;ORRESU, &#8211;ORNRHI, and &#8211;ORNRLO, all of which are Variable Qualifiers of &#8211;ORRES; and &#8211;DOSU, which is a Variable Qualifier of &#8211;DOSE.</font>

<font size="2">take a look at this table, where</font>

  * <font size="2">Role in column C comes from SDTMIG V3.1.3</font>
  * <font size="2">Role in column E comes from SDTM V1.3</font>

[<font size="2"><img title="qualifier" style="border-left-width: 0px; border-right-width: 0px; background-image: none; border-bottom-width: 0px; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; display: block; padding-right: 0px; border-top-width: 0px" border="0" alt="qualifier" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2014/03/qualifier_thumb.png" width="533" height="306" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2014/03/qualifier.png)

<font size="2">It is unavoidable for such systemic confusion among record qualifier and variable qualifier. A variable is a variable, and I don’t think it’s even possible to capture such subtle differences.</font>