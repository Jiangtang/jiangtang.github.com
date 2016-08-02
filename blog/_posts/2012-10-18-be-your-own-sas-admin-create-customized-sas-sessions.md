---
id: 757
title: 'Be Your Own SAS Admin: Create Customized SAS Sessions'
date: 2012-10-18T19:51:36+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=757
permalink: /2012/10/18/be-your-own-sas-admin-create-customized-sas-sessions/
categories:
  - Computer
  - SAS
tags:
  - SAS
---
&nbsp;

[<span style="font-size: xx-small;"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="SASIcons" alt="SASIcons" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/SASIcons_thumb.png" width="414" height="216" border="0" /></span>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/SASIcons.png)

<span style="font-size: xx-small;">You may find such SAS desktop shortcuts useful:</span>

  * <span style="font-size: xx-small;">click icon A then you get a SAS session titled “Project A” (you may notice your SAS session with title “SAS” by default). In this session, the current working folder is just where you put Project A (the default may be like C:usersyourID). Also, some autoexec codes run including libname, fileref, formats search, macro loading and other customized options/settings. </span>
  * <span style="font-size: xx-small;">Keep session A alive, then click icon B: you get your SAS session specified for Project B. And very important, there are no such annoying logs (you will most likely get such warnings when hitting your own SAS desktop icon twice): </span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">NOTE: <span style="color: #ff0000;">Unable</span> to open SASUSER.REGSTRY. WORK.REGSTRY will be opened instead.<br /> NOTE: All registry changes will be lost at the end of the session.<br /> <span style="color: #ff0000;">WARNING</span>: Unable to copy SASUSER registry to WORK registry. Because of this,<br /> WARNING: you will not see registry customizations during this session.<br /> NOTE: Unable to open SASUSER.PROFILE. WORK.PROFILE will be opened instead.<br /> NOTE: All profile changes will be lost at the end of the session.</span>

<span style="font-size: xx-small;">Here is the how-to demo (tested in a Window 7 machine with SAS 9.3; the so called project folder is my GitHub programming folder,  <em>C:\Users\jhu\Documents\GitHubProgramming-SAS</em>):</span>

  * <span style="font-size: xx-small;">From <em>C:\Users\jhu\Documents\My SAS Files\9.3</em>, copy user profile file </span><a href="http://support.sas.com/documentation/cdl/en/hostunx/61879/HTML/default/viewer.htm#a000386454.htm" target="_blank"><span style="font-size: xx-small;">profile.sas7bcat</span></a> <span style="font-size: xx-small;">to  the project folder. This is used to prevent the annoying message above.</span>
  * <span style="font-size: xx-small;">Throw a <strong>autoexec.sas</strong> file to the project folder with anything you like; or if you do not like, skip it</span>
  * <span style="font-size: xx-small;">Put in the project folder a configuration file <strong>sasv9.cfg</strong> with the following settings (delete –autoexec option if you want):</span>

> <span style="font-family: 'Courier New';"><span style="font-size: xx-small;"><span style="color: #ff0000;">-config</span> &#8220;C:\Program Files\SASHome\SASFoundation\9.3\nls\ensasv9.cfg&#8221;<br /> <span style="color: #ff0000;">-sasinitialfolder</span> &#8220;C:\Users\jhu\Documents\GitHubProgramming-SAS&#8221;<br /> <span style="color: #ff0000;">-awstitle</span> &#8220;My SAS Programming@GitHub&#8221;<br /> <span style="color: #ff0000;">-sasuser</span> &#8220;C:\Users\jhu\Documents\GitHubProgramming-SAS&#8221;<br /> <span style="color: #ff0000;">-autoexec</span> &#8220;C:\Users\jhu\Documents\GitHubProgramming-SASautoexec.sas&#8221;</span></span>

  * <span style="font-size: xx-small;">Send <em><strong>C:\Program Files\SASHome\SASFoundation\9.3\sas.exe</strong></em> to a desktop shortcut (I renamed it as “GitHub”).</span>
  * <span style="font-size: xx-small;">In desktop, find this icon and get its properties: in Target, replace all the text with</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">&#8220;C:\Program Files\SASHome\SASFoundation\9.3\sas.exe&#8221; -config &#8220;C:\Users\jhu\Documents\GitHubProgramming-SAS\sasv9.cfg&#8221;</span>

[<span style="font-size: xx-small;"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="SASIcons_target" alt="SASIcons_target" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/SASIcons_target_thumb.png" width="337" height="489" border="0" /></span>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/SASIcons_target.png)

<span style="font-size: xx-small;">Save the setting and exit then you click this icon and get:</span>

[<span style="font-size: xx-small;"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="GitHub" alt="GitHub" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/GitHub_thumb.png" width="517" height="379" border="0" /></span>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/GitHub.png)

&nbsp;

&nbsp;

<span style="font-size: xx-small;">Note:</span>

<a href="http://www.lexjansen.com/" target="_blank"><span style="font-size: xx-small;">Lex Jansen</span></a> <span style="font-size: xx-small;">made a good trick to start SAS in any specific folder by modifying the registry table in Windows; then you can right click mouse to get in a SAS session:</span>

[<span style="font-size: xx-small;"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="SAShere" alt="SAShere" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/SAShere_thumb.png" width="400" height="301" border="0" /></span>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/SAShere.png)

<span style="font-size: xx-small;">It’s simple: just save the following text to a file with extension as REG and run it (the configuration also in Windows 7 with SAS 9.3):</span>

> <span style="font-size: xx-small;">Windows Registry Editor Version 5.00</span>
> 
> <span style="font-size: xx-small;">[HKEY_CLASSES_ROOTDirectoryshellSAS_here_v93]<br /> @=&#8221;&SAS here V9.3&#8243;<br /> [HKEY_CLASSES_ROOTDirectoryshellSAS_here_v93command]<br /> @=&#8221;&#8221;C:Program FilesSASHomeSASFoundation9.3sas.exe&#8221; -sasinitialfolder &#8220;%V&#8221; -nosplash -CONFIG &#8220;C:Program FilesSASHomeSASFoundation9.3nlsensasv9.cfg&#8221;&#8221;</span>