---
id: 588
title: 'OpenCDISC Validator V1.3: An Unboxing Review (1): counting issue'
date: 2012-03-31T16:58:00+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=588
permalink: /2012/03/31/opencdisc-validator-v1-3-an-unboxing-review-1-counting-issue/
categories:
  - CDISC
  - SAS
  - XML
tags:
  - CDISC
  - OpenCDISC
  - SAS
  - Validation
  - XML
---

<font size="1"> 

<p>
  The lasted <a href="http://www.opencdisc.org" target="_blank">OpenCDISC</a> Validator version 1.3 was released at 29 March, 2012 (btw, there is a typo in the Line 1 of <em>CHANGELOG.txt</em> within the package: “2012” not “2011”). <a href="http://www.jiangtanghu.com/blog/2012/02/19/github-and-weekend-programming/" target="_blank">As usual</a>, you can submit the following SAS scripts to get some basic information(remember to customize your directory):
</p>

<blockquote>
  <p>
    <font face="Courier New">filename CDISC url "</font><a href="https://raw.github.com/Jiangtang/Programming-SAS/master/Rules_Count_OpenCDISC_XML.sas&quot;;"><font face="Courier New">https://raw.github.com/Jiangtang/Programming-SAS/master/Rules_Count_OpenCDISC_XML.sas";</font></a>
  </p>
  
  <p>
    <font face="Courier New">%include CDISC;</font>
  </p>
  
  <p>
    <font face="Courier New">%Rules_Count_OpenCDISC_XML(dir=C:OpenCDISC1.3compareopencdisc-validator_1.3config)</font>
  </p>
</blockquote>

<p>
  and you get a summary of validation rules of OpenCDISC Validator V1.3 (<strong>499</strong> total unique rules):
</p>

<p>
  <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/OpenCDISC_V1.3.png"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="OpenCDISC_V1.3" border="0" alt="OpenCDISC_V1.3" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/OpenCDISC_V1.3_thumb.png" width="444" height="312" /></a>
</p>

<p>
  where
</p>

<blockquote>
  <p>
    AD: Analytical Data <br />CT: Controlled Terminology <br />DD: Data Definition <br />OD: Operation Data Model <br />SD: Study Data <br />SE: <a href="http://www.cdisc.org/send" target="_blank">SEND</a> data
  </p>
</blockquote>

<p>
  As comparison, a summary of V1.2.1 (<strong>385</strong> total unique rules) posted before:
</p>

<p>
  <img style="margin: 3px auto 5px; display: block; float: none" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/02/OC_by_model.png" width="446" height="292" />
</p>

<p>
  The most significant enhancement of V1.3 against V1.2.1 is the adding of rules for <a href="http://www.cdisc.org/stuff/contentmgr/files/0/3fa5f30f40ce5ecc7b3f91e558b55f73/misc/amendment_1_to_study_data_tabulation_model_v1_2_and_sdtmig_v3_1_2_final_2011_12_14.pdf" target="_blank">SDTM 3.1.2 with Amendment 1</a> and <a href="http://www.cdisc.org/send" target="_blank">SEND 3.0</a>. You can see there are also some changes among others modules, such ADaM 1.0 and SDTM 3.1.2. The OpenCDISC release newsletter said that there are <strong>43</strong> new SDTM rules added. Well, rules deleted, rules added, rules commented, we now have some arithmetical discrepancies.
</p>

<p>
  The scripts above capture all instances of validation rule IDs (also delete some commented for example in <em>config-<strong>define</strong>-1.0.xml</em>, four rules commented: OD0004, OD0005, OD0007, OD0008). We can also double validate the counts manually:
</p>

<ul>
  <li>
    copy all contents for example in <a href="http://www.opencdisc.org/projects/validator/cdisc-sdtm-3.1.2-validation-rules" target="_blank">SDTM 3.1.2</a> in its website into Notepad++ (where line numbers displayed)
  </li>
  <li>
    delete all unnecessary entries
  </li>
  <li>
    then the last line number is the total number of the rules (227 in this case).
  </li>
</ul>

<p>
  Another way to check the rules is to <a href="http://www.jiangtanghu.com/blog/2012/02/11/xml/" target="_blank">open the XML configuration files using a web browser</a>:
</p>

<p>
  <img style="margin: 3px auto 5px; display: block; float: none" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/02/XML_IE1.png" width="455" height="405" />
</p>

<p>
  Theoretically the three ways are identical in counting, but there is an open bug in the style sheet file in …OpenCDISC1.3opencdisc-validatorconfigresourcesxsl<strong>config.xsl</strong>, Line 175:
</p>

<blockquote>
  <p>
    <font face="Courier New"><xsl:template match="val:Unique|val:Condition|val:Match|val:Regex</font>
  </p>
  
  <p>
    <font face="Courier New">|val:Required|val:Lookup|val:Metadata"></font>
  </p>
</blockquote>

<p>
  There is no “val:Find” to render all the Find validation rules (AD0061 in config-<strong>adam</strong>-1.0.xml) so all Find validators are not displayed. A suggested workaround is just to add “val:Find” to the file:
</p>

<blockquote>
  <p>
    <font face="Courier New"><xsl:template match="val:Unique|val:Condition|val:Match|val:Regex</font>
  </p>
  
  <p>
    <font face="Courier New">|val:Required|val:Lookup|val:Metadata<font color="#ff0000">|val:Find</font>"></font>
  </p>
</blockquote>

<p>
  Actually in the “<em><a href="http://www.opencdisc.org/projects/validator/opencdisc-validation-framework#validation-rules" target="_blank">OpenCDISC Validation Framework</a></em>” page of OpenCDISC website, the “Find”validator is not <a href="http://www.jiangtanghu.com/blog/2012/02/29/not-documented-not-exist/" target="_blank">documented</a> yet.
</p>

<p>
  <<em>to be continued</em>>
</p>

<p>
  </font>
</p>