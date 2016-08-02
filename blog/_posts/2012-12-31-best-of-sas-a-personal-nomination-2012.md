---
id: 1075
title: 'Best of SAS: A Personal Nomination 2012'
date: 2012-12-31T01:13:03+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1075
permalink: /2012/12/31/best-of-sas-a-personal-nomination-2012/
categories:
  - CDISC
  - SAS
tags:
  - Graph
  - Metadata
  - ODS
  - ODS Graphics
  - ODS Report Writing
  - PROC FREQ
  - Proc TTEST
  - SAS
  - SAS XML Mapper
  - T-test
  - XML
---
<font size="1">There SAS applications/procedures/features were not necessarily available since 2012. This year I paid special attention to them when began to use SAS 9.3. The following notes are&#160; totally my personal endorsement purely based my own experience as a user:</font>

# XML File Reading: SAS XML Mapper

<font size="1"><a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/SAS_XML_Mapper.png"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="SAS_XML_Mapper" border="0" alt="SAS_XML_Mapper" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/SAS_XML_Mapper_thumb.png" width="363" height="399" /></a></font>

<font size="1">SAS XML Mapper itself is not an elegant tool from software design perspective (an example: I keep multiple versions because the latest version seems not carry out all the functionalities from old ones), but it is best XML file processing tool for SAS programmers like me. The sweet part of SAS XML Mapper is that you can use it to get SAS datasets directly with a automatically generated XML mapping file. I use it to import XML files from </font>

> <font size="1">CDISC ODM based files like define.xml </font>
> 
> <font size="1">metadata querying results (XML) returned by SAS Metadata Server</font>

<font size="1">and it works pretty well and I just can’t live without it!</font>

# Graphics Facility: ODS Graphics

<font size="1">ODS Graphics is the raising star among SAS products family since its advent and I also fall into love with her. This system contains</font>

> <font size="1">five procedures with “SG” in names,</font>
> 
> <font size="1">a template language(GTL), and</font>
> 
> <font size="1">two GUI tools, ODS Graphics Editor, and ODS Graphics Designer</font>

<font size="1">in Base SAS and ODS Statistical Graphics in SAS/STAT (and in SAS/QC which I didn’t check out). ODS Graphics just makes SAS graph&#160; much beautiful and graphics task much fun (and elegant!). </font>

<font size="1">Btw, it may not be a fair game but still nice to check out a SAS ODS graph and some random pick up R graphs:</font>

<font size="1">This is <a href="http://blogs.sas.com/content/iml/2011/08/26/visualizing-correlations-between-variables-in-sas/">from Rick Wicklin</a> with 3 lines of codes including one “RUN” statement:</font>

> <pre>proc sgscatter data=sashelp.iris; 
matrix SepalLength--PetalLength /group=Species diagonal=(histogram kernel);
run;</pre>

[<img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="SAS_corr2" border="0" alt="SAS_corr2" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/SAS_corr2_thumb.png" width="400" height="408" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/SAS_corr2.png)

<font size="1">and this is the R homepage graph(and the <a href="http://www.r-project.org/misc/acpclust.R">R codes</a>):</font>

<font size="1"><a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/R_Graphics.png"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="R_Graphics" border="0" alt="R_Graphics" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/R_Graphics_thumb.png" width="396" height="294" /></a></font>

<font size="1">and this is <a href="http://gallery.r-enthusiasts.com/">R Graph Gallery</a> homepage:</font>

[<img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="r_graph_gallery" border="0" alt="r_graph_gallery" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/r_graph_gallery_thumb.png" width="403" height="287" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/r_graph_gallery.png)

<font size="1">I must say SAS ODS Graphics rocks!</font>

# Statistical Procedure: PROC TTEST and PROC FREQ

<font size="1">In this category I list two because they are equally extremely relevant and important for me as statistical SAS programmer.</font>

<font size="1">PROC TTEST makes equivalence test (which is extremely popular in clinical research) much more accessible by adding a TOST(two one-side test) option. Years ago SAS programmers might use PROC MIXED or other methods for this kind of statistical test(<font size="1">I also took a note on this topic, see <a href="http://www.jiangtanghu.com/blog/2012/09/12/tost-equivalence-test/" target="_blank">here</a></font>).</font>

<font size="1">The new on PROC FREQ I checked out is to support much richer methods on calculating confidence intervals for binomial proportion (my note <a href="http://www.jiangtanghu.com/blog/2012/09/15/confidence-intervals-binomial-proportion/" target="_blank">here</a>) and confidence intervals for difference between independent binomial proportions (my note <a href="http://www.jiangtanghu.com/blog/2012/09/23/statistical-notes-5-confidence-intervals-for-difference-between-independent-binomial-proportions-using-sas/" target="_blank">here</a>) which are also extremely important in clinical research and I programmed a lot.</font>

# Report Writing: ODS Report Writing Interface

<font size="1">My first SAS version was 9.1.3 where PROC REPORT is the primary SAS reporting writing tool (with ODS) while PROC TABULATE not in fashion anymore (and you may merely hear the arguments among these two procedures since then). I used PROC REPORT for all my production work for reporting since recently I tried the </font><a href="http://support.sas.com/rnd/base/datastep/dsobject/index.html" target="_blank"><font size="1">ODS Report Writing Interface</font></a> <font size="1">in a project for non-rectangular tables. It’s great and everyone was happy! </font>

<font size="1">Basically it is an ODS enhanced DATA _NULL_ reporting writing method (<em>DATA _NULL_ with <font color="#ff0000">FILE PRINT</font> statements: it’s an even older way for me</em>);a new ODS output object declared within DATA _NULL_:</font>

> <font size="1" face="Courier New">dcl odsout obj();</font>

<font size="1">I like this kind of reporting method: you can control your report line by line and cell by cell (although with more lines of structured codes!).</font>

# Metadata Querying Tool: PROC METADATA 

<font size="1">In this category, the other two strong candidates are JAVA interface and SAS Data Step Functions. I like PROC Metadata against JAVA because it holds the same full functionality (while SAS Data Step Functions, no yet) while I can still work in SAS to produce reports (just add a new line to start to use ODS Report Writing Interface:)). Furthermore, I feel much comfortable working with SAS!</font>

<font size="1">PROC Metadata uses XML as inputs and outputs: it may be not admirable compared to Data Step Functions. Since I use SAS XML Mapper, it’s not a problem anymore!</font>

# Documentation 

<font size="1">I like the totally new SAS help and documentation system both online and offline since SAS 9.3. </font>

<font size="1">First in Base SAS, lots of files were separated from “SAS Language Dictionary”,</font>

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="SAS_Docs_offline" border="0" alt="SAS_Docs_offline" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/SAS_Docs_offline_thumb.png" width="420" height="420" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/SAS_Docs_offline.png)

<font size="1">and in all procedures guide, the <a href="http://www.jiangtanghu.com/blog/2012/07/14/tab-is-a-tab-is-a-tab-is-a-tab/">tab</a> view looks great:</font>

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="SAS_Docs" border="0" alt="SAS_Docs" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/SAS_Docs_thumb.png" width="452" height="271" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/12/SAS_Docs.png)

<font size="1"></font>

<font size="1"></font>