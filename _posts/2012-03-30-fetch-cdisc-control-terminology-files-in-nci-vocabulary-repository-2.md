---
id: 584
title: 'Fetch CDISC Control Terminology Files in NCI Vocabulary Repository: All in One Click'
date: 2012-03-30T00:23:17+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=584
permalink: /2012/03/30/fetch-cdisc-control-terminology-files-in-nci-vocabulary-repository-2/
categories:
  - CDISC
  - SAS
tags:
  - CDISC
  - Control Terminology
  - GNU
  - NCI
  - Wget
---
<font size="1"><a href="http://www.cdisc.org/terminology" target="_blank">CDISC Control Terminology</a> is the most frequent updated model among CDISC standards. Take SDTM as example, the latest SDTM terminologies released at 23 March 2012; and f</font><font size="1">rom 2009 to 2011, there were 15 different SDTM terminology versions! If you just rely on your own local repository, you might miss the pace somehow.</font>

<font size="1">Here is a simple approach. Just submit the following one line of codes in a shell,</font>

> <font face="Courier New">wget </font>[<font face="Courier New">http://evs.nci.nih.gov/ftp1/CDISC/</font>](http://evs.nci.nih.gov/ftp1/CDISC/) <font face="Courier New">-r &#8211;no-parent&#160; -l 3</font>

<font size="1">and you will get all the CDISC Control Terminology files (plus historical versions) with proper folder structures in your local driver (the current directory of your shell).</font>

<font size="1">For syntax details, you can refer to its <a href="http://www.gnu.org/software/wget/manual/wget.html" target="_blank">online manual</a>:</font>

> <font size="1">-r: recursive retrieving</font>
> 
> <font size="1">&#8211;no-parent: only fetch files under the URL</font>
> 
> <font size="1">-l 3: set maximum depth level of 3 </font>&#160;

<font size="1">If you are a Windows user, you might install <a href="http://gnuwin32.sourceforge.net/packages/wget.htm" target="_blank">Wget for Windows</a> (it is a native tool in Unix/Linux under <font size="1">GNU</font>)and add it<em> </em>into your environmental variable, <em>Path</em>. You can also save the above scripts in a notepad and save it as a .bat file(<em>test.bat</em> for example). Next time you just click the <em>test.bat</em> to get all the updates.</font>

<font size="1">Wget is a very powerful tool. For me, the download speed is pretty acceptable (depends on internet connection) and almost no difference between a Windows 7 and a Ubuntu 11 machine:</font>

[<img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="Wget_Win7" border="0" alt="Wget_Win7" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/Wget_Win7_thumb.png" width="492" height="175" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/Wget_Win7.png)

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="Wget_ubuntu11" border="0" alt="Wget_ubuntu11" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/Wget_ubuntu11_thumb.png" width="491" height="149" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/Wget_ubuntu11.png)