---
author: Jiangtang Hu
title: 'Be Your Own SAS Admin: Create Customized SAS Sessions'
excerpt:
layout: post
category:
  - Computer
  - SAS
tags:
  - SAS
post_format: [ ]
---
[![SASIcons][2]][2]

You may find such SAS desktop shortcuts useful:

*   click icon A then you get a SAS session titled “Project A” (you may notice your SAS session with title “SAS” by default). In this session, the current working folder is just where you put Project A (the default may be like C:usersyourID). Also, some autoexec codes run including libname, fileref, formats search, macro loading and other customized options/settings. 
*   Keep session A alive, then click icon B: you get your SAS session specified for Project B. And very important, there are no such annoying logs (you will most likely get such warnings when hitting your own SAS desktop icon twice): 

> NOTE: Unable to open SASUSER.REGSTRY. WORK.REGSTRY will be opened instead.   
> NOTE: All registry changes will be lost at the end of the session.   
> WARNING: Unable to copy SASUSER registry to WORK registry. Because of this,   
> WARNING: you will not see registry customizations during this session.   
> NOTE: Unable to open SASUSER.PROFILE. WORK.PROFILE will be opened instead.   
> NOTE: All profile changes will be lost at the end of the session.

Here is the how-to demo (tested in a Window 7 machine with SAS 9.3; the so called project folder is my GitHub programming folder,  *C:UsersjhuDocumentsGitHubProgramming-SAS*):

*   From *C:UsersjhuDocumentsMy SAS Files9.3*, copy user profile file [profile.sas7bcat][2] to  the project folder. This is used to prevent the annoying message above. 
*   Throw a **autoexec.sas** file to the project folder with anything you like; or if you do not like, skip it 
*   Put in the project folder a configuration file **sasv9.cfg** with the following settings (delete –autoexec option if you want): 

> -config "C:Program FilesSASHomeSASFoundation9.3nlsensasv9.cfg"   
> -sasinitialfolder "C:UsersjhuDocumentsGitHubProgramming-SAS"   
> -awstitle "My SAS Programming@GitHub"   
> -sasuser "C:UsersjhuDocumentsGitHubProgramming-SAS"   
> -autoexec "C:UsersjhuDocumentsGitHubProgramming-SASautoexec.sas"

*   Send ***C:Program FilesSASHomeSASFoundation9.3sas.exe*** to a desktop shortcut (I renamed it as “GitHub”). 
*   In desktop, find this icon and get its properties: in Target, replace all the text with 

> "C:Program FilesSASHomeSASFoundation9.3sas.exe" -config "C:UsersjhuDocumentsGitHubProgramming-SASsasv9.cfg"

[![SASIcons_target][4]][4]

Save the setting and exit then you click this icon and get:

[![GitHub][5]][5]





Note:

[Lex Jansen][5] made a good trick to start SAS in any specific folder by modifying the registry table in Windows; then you can right click mouse to get in a SAS session:

[![SAShere][7]][7]

It’s simple: just save the following text to a file with extension as REG and run it (the configuration also in Windows 7 with SAS 9.3):

> Windows Registry Editor Version 5.00
> 
> [HKEY\_CLASSES\_ROOTDirectoryshellSAS\_here\_v93]   
> @="&SAS here V9.3"   
> [HKEY\_CLASSES\_ROOTDirectoryshellSAS\_here\_v93command]   
> @=""C:Program FilesSASHomeSASFoundation9.3sas.exe" -sasinitialfolder "%V" -nosplash -CONFIG "C:Program FilesSASHomeSASFoundation9.3nlsensasv9.cfg""

 []: http://dl.dropbox.com/u/69732603/SASIcons.png
 [2]: http://support.sas.com/documentation/cdl/en/hostunx/61879/HTML/default/viewer.htm#a000386454.htm
 []: http://dl.dropbox.com/u/69732603/SASIcons_target.png
 []: http://dl.dropbox.com/u/69732603/GitHub.png
 [5]: http://www.lexjansen.com/
 []: http://dl.dropbox.com/u/69732603/SAShere.png