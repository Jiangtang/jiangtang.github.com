---
id: 735
title: Current Working Folder in SAS
date: 2012-10-08T22:19:47+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=735
permalink: /2012/10/08/current-working-folder-in-sas/
categories:
  - Uncategorized
tags:
  - CMD
  - current folder
  - Powershell
  - SAS
  - Shell
---
<span style="font-size: xx-small;"><a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/whereamI.jpg"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border: 0px;" title="whereamI" alt="whereamI" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/whereamI_thumb.jpg" width="377" height="370" border="0" /></a></span>

<span style="font-size: xx-small;">The concept of </span><a href="http://support.sas.com/documentation/cdl/en/hostwin/63047/HTML/default/viewer.htm#p16esisc4nrd5sn1ps5l6u8f79k6.htm" target="_blank"><span style="font-size: xx-small;">current working directory in SAS</span></a> <span style="font-size: xx-small;">is not as important as it sounds. Most SAS users point to file reference (fileref) and library reference (libname, a “namespace”-like mechanism to access files ), which are much convenient in large project with multiple folders.</span>

<span style="font-size: xx-small;">Sometimes I push files to the current folder in relatively small task because I don’t want to</span>

  * <span style="font-size: xx-small;">jump to <em>C:\Users\jhu\appdata\Local\Temp\SAS\Temporary Files\_TD2820_</em>like folder to get the temporary datasets (in WORK library) </span>
  * <span style="font-size: xx-small;">hard code a folder to receive ODS outputs.</span>

<span style="font-size: xx-small;">The demo codes(a SAS system autocall macro %xlog used):</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">/*display current directory in LOG window*/<br /> %<span style="color: #ff0000;">xlog</span>(cd);</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">/*change current working directory */<br /> x &#8220;cd a:\test&#8221;;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">/*display current directory in LOG window*/<br /> %xlog(cd);</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">/*output a dataset in current directory */<br /> <span style="color: #ff0000;">data &#8220;iris&#8221;;</span><br /> set sashelp.iris;<br /> run;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">/*output a pdf file in current directory */<br /> ods pdf <span style="color: #ff0000;">file=&#8221;iris.pdf&#8221;;</span><br /> proc print data=&#8221;iris&#8221;;<br /> run;<br /> ods pdf close;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">/*show files in current directory */<br /> %xlog(dir);</span>

<span style="font-size: xx-small;">And the LOG window may like:</span>

> <span style="font-family: Consolas; font-size: xx-small;">Path<br /> &#8212;-<br /> C:\Users\jhu</span>
> 
> <span style="font-family: Consolas; font-size: xx-small;">Path<br /> &#8212;-<br /> A:\test</span>
> 
> <span style="font-size: xx-small;"><span style="font-family: Consolas;">    Directory: A:test</span><br /> </span><span style="font-family: Consolas; font-size: xx-small;">Mode        LastWriteTime   Length Name<br /> &#8212;-        &#8212;&#8212;&#8212;&#8212;-   &#8212;&#8212; &#8212;-<br /> -a&#8212; 10/8/2012  12:49 PM   113665 iris.pdf<br /> -a&#8212; 10/8/2012  12:49 PM    13312 iris.sas7bdat</span>

# NOTES:

  * <span style="font-size: xx-small;">You can get autocall macro %xlog in (if SAS 9.3 in Windows 7)</span>

> <span style="font-size: xx-small;">C:\Program Files\SASHome\SASFoundation\9.3\<span style="color: #ff0000;">core\sasmacro</span></span>

<span style="font-size: xx-small;">An equivalent macro <span style="color: #ff0000;">%xlst</span> generates the shell command outputs to LIST window.</span>

  * <span style="font-size: xx-small;">If prefer Windows Powershell, a similar macro can be used (put it to autocall if needed):</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">%macro <span style="color: #ff0000;">pslog</span>(cmd);<br /> option nonotes;<br /> filename pslogcmd pipe &#8220;<span style="color: #ff0000;">powershell</span> &cmd&#8221;;<br /> data _null_;<br /> file log;<br /> infile pslogcmd;<br /> input;<br /> put _INFILE_;<br /> run;<br /> option notes;<br /> %mend pslog;</span>

<span style="font-size: xx-small;">Test the following commands:</span>

> <span style="font-size: xx-small;"><span style="font-family: 'Courier New';">%pslog(gl);<br /> %pslog(get-location);<br /> %pslog(get-host)</span></span>