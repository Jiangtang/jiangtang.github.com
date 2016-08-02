---
id: 1216
title: 'Open Box: SAS 9.4 in Windows 7'
date: 2013-07-28T16:06:37+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1216
permalink: /2013/07/28/open-box-sas-9-4-in-windows-7/
categories:
  - SAS
tags:
  - SAS
  - SAS 9.4
---
[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="SAS94" border="0" alt="SAS94" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS94_thumb.png" width="480" height="253" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS94.png)

<font size="1">That’s a record in my personal SAS software adoption: SAS 9.4 was released at 10 July 2013 and </font>[<font size="1">I just got it installed two weeks later</font>](http://www.jiangtanghu.com/blog/2013/07/11/catch-up-with-sas/)<font size="1">! </font>

<font size="1">Here my first-day notes with SAS 9.4:</font>

<font size="1">1. SAS Foundation 9.4 can be co-existed with SAS 9.3. If SAS 9.3 was already installed, the default of path of 9.4 is <strong>C:\Program Files\SASHome2</strong>; otherwise, it will take over <strong>C:\Program Files\SASHome</strong>.</font>

<font size="1">2. But for <strong>SAS PC Files Server 9.4</strong>, you should uninstall the old version first since they will share the same port number 9621.</font>

<font size="1">3. Only <strong>64 bit</strong> machine can hold SAS 9.4.</font>

<font size="1">4. No Java Runtime Environment(<strong>JRE</strong>) is pre-required. Instead, a </font>[<font size="1">SAS Private JRE</font>](http://support.sas.com/kb/48/548.html) <font size="1">(version 1.7.0_15) will be installed automatically (time to get rid of your 32 bit of JRE6, <em>jre-6u24-windows-i586</em>!).</font>

<font size="1">5. It is said Windows </font>[<font size="1"><strong>Powershell</strong></font>](http://support.sas.com/kb/50/123.html) <font size="1">will be needed for some SAS 9.4 deployment. I didn’t figure it out since I only did the SAS Foundation installation.</font>

<font size="1">6.The SAS Hot Fix Analysis, Download and Deployment Tool (</font>[<font size="1"><strong>SASHFADD</strong></font>](ftp://ftp.sas.com/techsup/download/hotfix/HF2/SASHFADD.html)<font size="1">) is currently not available for SAS 9.4. </font>

<font size="1">7. New icon(but the little “runman” is the same):</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="SAS93_icone" border="0" alt="SAS93_icone" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS93_icone_thumb.png" width="101" height="34" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS93_icone.png)[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="SAS_94_icone" border="0" alt="SAS_94_icone" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS_94_icone_thumb.png" width="106" height="49" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS_94_icone.png)

<font size="1">8. The default <strong>YEARCUTOFF</strong> is no longer 1920. It’s now 1926. OK, we have 12 years to reach to the year of 2025.</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="SAS94_yearcutoff" border="0" alt="SAS94_yearcutoff" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS94_yearcutoff_thumb.png" width="517" height="131" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS94_yearcutoff.png)

<font size="1">9. The SAS <strong>Documentation Viewer 9.4</strong> is pretty quicker.</font>