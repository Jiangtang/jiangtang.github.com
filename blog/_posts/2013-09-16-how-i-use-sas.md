---
id: 1263
title: How I Use SAS?
date: 2013-09-16T12:48:31+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1263
permalink: /2013/09/16/how-i-use-sas/
categories:
  - SAS
tags:
  - SAS
  - SAS 9.4
---
<font size="1">It’s pretty fun to read SAS/Graph expert </font>[<font size="1">Robert Allison</font>](http://robslink.com/SAS/Home.htm)<font size="1">’s note,<em> <a href="http://robslink.com/SAS/papers/using_sas/using_sas.htm">Using SAS- A Case Study</a></em> on his SAS programming environment, such as SAS version, OS, fileserver and editors. Here is my follow up:</font>

##### SAS Version

<font size="1">I always want to </font>[<font size="1">keep pace with the latest SAS</font>](http://www.jiangtanghu.com/blog/2013/07/11/catch-up-with-sas/) <font size="1">software; something I got it, sometime not. As of September 2013, </font>[<font size="1">I use SAS 9.4</font>](http://www.jiangtanghu.com/blog/2013/07/28/open-box-sas-9-4-in-windows-7/) <font size="1">in my workstation.</font>

<font size="1">For different tasks, clients or their combinations, I should use specific versions of SAS in customers’ computing environment remotely or in virtual machines; they are mostly SAS 9.2 and 9.3. Occasionally I touch SAS 9.1.3 (which was my first SAS version in 2006) and even 8.2 for migration purpose.</font>

<font size="1">I like the latest SAS because, I like all my desktop software and mobile apps to be updated, automatically at best. Although it is not necessary for some cases, I hate to have bits of yesterday’s food in my desktop. For SAS particularly, it doesn’t hurt to be move forward to the new version like 9.4 while I get bonus like </font>[<font size="1">ODS Reporting Writing Interface</font>](http://www.jiangtanghu.com/blog/2013/02/17/sas-ods-report-writing-interface-a-quick-demo/)<font size="1">. Work with multiple versions of SAS and I find SAS codes themselves are amazingly portable across versions and OS (<em>Dear R users—no offending, please rerun the </em></font>[_<font size="1">R codes</font>_](http://www.r-project.org/misc/acpclust.R)_ <font size="1">to generate the cover graph for </font>_[_<font size="1">www.r-project.org</font>_](http://www.r-project.org)<font size="1">).</font>

##### OS

<font size="1">I primarily work on Windows and run PC SAS. But even in Windows, I need to play with Unix/Linux SAS in such instances:</font>

<font size="1">1. SAS Drug Development: For version 4.x, I use Google Chrome in Windows to open a web interface, then launch a SAs session (with a web editor). The SAS itself is Linux based.</font>

<font size="1">2. SAS Integration Studio (DIS) and Enterprise Guide (EG): In some Windows machines, the DIS or EG is the only client available to talk with SAS which is installed in a Linux server. EG is great to connect multiple servers. DIS is primarily for ETL jobs, but it’s nice to have if you only want to run some SAS Base codes.</font>

<font size="1">3. If I need to jump into the black Unix box, I use Putty or Cygwin to get a terminal, write and edit code in vi and run it on batch.</font>

<font size="1">I rarely use SAS GUI (I use Xming to invoke it) in Unix; The X-window is ugly and to tell the truth, I don’t know how to play the program editor with line number like 0002! Sometime I use it to view the metadata tree.</font>

##### DMS or Batch

<font size="1">In PC SAS, I use DMS (Display Manager System, the one with the Enhanced Editor) for interactive debugging. If all goes well, I will run them in batch just to double check everything is OK.</font>

<font size="1">I run SAS in batch mode in Windows when use text editors (only) like </font>[<font size="1">VIM</font>](http://www.jiangtanghu.com/blog/2011/11/13/vim-as-a-sas-ide/) <font size="1">and </font>[<font size="1">Sublime Text</font>](http://www.jiangtanghu.com/blog/2012/07/13/sublimetext2-sas/) <font size="1">with SAS configurations.</font>

<font size="1">In Unix, I use a default editor vi to edit SAS code then run it in command line (the batch mode).</font>

##### Editors

<font size="1">My favorite editors in Windows are </font>[<font size="1">Notepad++,</font>](http://support.sas.com/resources/papers/proceedings11/211-2011.pdf) <font size="1"></font>[<font size="1">VIM</font>](http://www.jiangtanghu.com/blog/2011/11/13/vim-as-a-sas-ide/) <font size="1">and </font>[<font size="1">Sublime Text</font>](http://www.jiangtanghu.com/blog/2012/07/13/sublimetext2-sas/)<font size="1">. VIM and Sublime Text are great for writing while Notepad++ is perfect for viewing, finding and replacing. Since I got Sublime Text, I use it as partial replacement of VIM because it supports some basic VI operations.</font>

<font size="1">In Unix, I use vi. That’s because I didn’t touch Emacs.</font>

##### Viewing Outputs

<font size="1">I like the DMS in PC SAS because it supports all SAS elements, datasets, formats, macro catalogs and such. </font>[<font size="1">Before SAS 9.4</font>](http://www.jiangtanghu.com/blog/2013/08/27/sas-system-viewer-doesnt-support-sas-9-4-dataset/)<font size="1">, I also like to use </font>[<font size="1">SAS System Viewer</font>](http://www.jiangtanghu.com/blog/2013/07/16/sas-system-viewer/) <font size="1">to open SAS datasets. SAS Universal Viewer just sucks.</font>

<font size="1">For PDF outputs, I use Foxit Reader. For HTML, I like Google Chrome.</font>

<font size="1">In Unix, well, after batch run, I check the result in the mapped Windows driver.</font>

##### SAS Products

  * <font size="1"><strong>SAS Base</strong>: Data Step, ODS, SQL, Macro, XML, Regular Expression, Reporting, ODS Graphics and whatever makes a SAS programmer. Love it.</font> 
  * <font size="1">SAS/Graph: I didn’t touch it since the ODS graphics available in SAS 9.2. </font>
  * <font size="1"><strong>SAS/STAT</strong>: I’m not a statistician but a user. My favorite procedures are </font>[<font size="1">PROC TTEST</font>](http://www.jiangtanghu.com/blog/2012/09/12/tost-equivalence-test/)<font size="1">, </font>[<font size="1">PROC FREQ,</font>](http://www.jiangtanghu.com/blog/2013/08/25/confidence-intervals-for-difference-between-independent-binomial-proportions-a-sas-9-4stat-12-3-update/) <font size="1">PROC GLM, PROC LOGISTIC, PROC LIFETEST, PROC PHREG which I use heavily as a statistical SAS programmer in clinical section.</font> 
  * <font size="1">SAS/IML: I didn’t touch it after </font>[<font size="1">2010</font>](http://www.jiangtanghu.com/blog/2010/10/29/sas-iml-basic/)<font size="1">. That’s because I seldom find a machine licensed with IML! I think it would be good idea to </font>[<font size="1">put it to SAS Base</font>](http://www.jiangtanghu.com/blog/2012/10/16/incorporate-sasiml-to-base-sas/)<font size="1">.</font> 
  * <font size="1"><strong>SAS Data Integration Studio</strong>: For ETL. Sometimes it is my only client to talk with SAS. </font>
  * <font size="1"><strong>SAS Enterprise Guide</strong>: It’s a great client to communicate with multiple SAS servers, but it is not 100% compatible with SAS Base (it’s sad). I like its editor and navigation panels. It will rock in the future.</font> 
  * <font size="1"><strong>SAS Clinical Toolkits</strong> and <strong>SAS Clinical Data Integration</strong>: For CDISC stuff. It’s my primary technical job working as a clinical consultant.</font> 
  * <font size="1"><strong>SAS Drug Development</strong>: A SAS hosting environment for pharmas.</font> 
  * <font size="1"><strong>SAS System Viewer</strong>: The </font>[<font size="1">good</font>](http://www.jiangtanghu.com/blog/2013/07/16/sas-system-viewer/)<font size="1">.</font> 
  * <font size="1">SAS Universal Viewer: The </font>[<font size="1">bad</font>](http://www.jiangtanghu.com/blog/2013/07/16/sas-system-viewer/) <font size="1">but it is the only option in most machines.</font> 
  * <font size="1"><strong>SAS XML Mapper</strong>: The primary tool I use to play with XML files.</font> 
  * <font size="1"><strong>SAS Power&#160; and Sample Size</strong>: I checked it for a while to accompany with nQuery Advisor.</font> 
  * <font size="1"><strong>SAS PC File Server</strong>: a trouble maker when across Excel and SAS bitness (32/64 bits); but if installed right, it’s nice tool to read Excel files across OS.</font> 
  * <font size="1"><strong>SAS Documentation Viewer</strong>: I like the SAS 9.4 Documentation Viewer. It’s much quicker.</font> The only flaw is the lack of Favorite tab.