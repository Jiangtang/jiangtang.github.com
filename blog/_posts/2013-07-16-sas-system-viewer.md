---
id: 1204
title: The Return of SAS System Viewer
date: 2013-07-16T22:37:50+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1204
permalink: /2013/07/16/sas-system-viewer/
categories:
  - SAS
tags:
  - SAS
  - SAS System Viewer
  - SAS Universal Viewer
---
[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="SAS_System_Viewer" border="0" alt="SAS_System_Viewer" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS_System_Viewer_thumb.png" width="379" height="455" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS_System_Viewer.png)[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="SAS_Universal_Viewer" border="0" alt="SAS_Universal_Viewer" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS_Universal_Viewer_thumb.png" width="475" height="502" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/07/SAS_Universal_Viewer.png)

<font size="1">SAS Universal Viewer (UV) jumped out since SAS 9.2 and in most cases, it’s installed as replacement for the <a href="http://support.sas.com/demosdownloads/sysdep_t1.jsp?packageID=000313&jmpflag=N">SAS System Viewer</a>(SV) but I reinstalled SV in all machines where I had the right privileges. UV has some nice new feature but for me it is extremely and unacceptably slow. Every time I open a relatively not entirely small dataset (literally, 30MB) in UV, it shows up “initializing” <strong>forever </strong>(even the initializing process is done, I guess). SV will be “Ready” all the way in the same machine.&#160; </font>

<font size="1">UV will load all the datasets (called a library) in the same folder even when you only click one dataset to view. Yes it’s not a bug, actually it should be considered as a feature. When I click one dataset, I only need and want to view this specific one dataset; if needed, I will open multiple datasets in SV’s tabs, and it’s much quicker!</font>

<font size="1">Also compared to SV, UV has too many bells and whistles. In a single page, UV shows less information. Actually I do not need a UNIVERSAL viewer; I need only a SAS dataset viewer. It’s claimed that you can view SAS programs, logs, listings (and other general text files) and even HTML files in UV. It’s cool, but we already have other much better tools to open them.</font>

<font size="1">To those who want to switch the oldie and goodie SV, some tips:</font>

<font size="1">1. If possible, install SV before any other SAS foundation installation. If you reverse the process, an critical important SV component (<strong>sassfiod.dll</strong>) will be put in the SAS foundation folder (<em>C:\Program Files\SASHome\x86\General </em>for in a Windows 7 machine with SAS 9.3). Since SV is a stand-alone application, it is much safer to be separated from the SAS foundation. Install SV first and <strong>sassfiod.dll </strong>will be in <em>C:\Program Files (x86)\SAS\Shared Files\General</em> while SV itself, <em>C:\Program Files (x86)\SAS\SAS System Viewer</em>.</font>

<font size="1">2. If for any reason, you got error message like “<em>Cannot find file SASSFIOD</em>.<em>DLL</em>” when using SV, reinstall it or copy this file from a right machine to the proper folder(see #1).</font>

<font size="1">3. Use it as default SAS dataset viewer explicitly. Otherwise, UV, SAS Enterprise Guide and SAS Display Manager will compete to serve as the viewer.</font>

<font size="1">4. Enable the tabbed view through View->Options->General->File Display Mode.</font>