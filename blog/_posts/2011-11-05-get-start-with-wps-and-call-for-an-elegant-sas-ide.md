---
id: 436
title: Get Start with WPS, and Call for an Elegant SAS IDE!
date: 2011-11-05T21:50:42+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/11/05/get-start-with-wps-and-call-for-an-elegant-sas-ide/
permalink: /2011/11/05/get-start-with-wps-and-call-for-an-elegant-sas-ide/
categories:
  - SAS
tags:
  - IDE
  - SAS
  - VIM
  - WPS
---
I got a trial version of <a href="http://www.teamwpc.co.uk/products/wps" target="_blank">WPS</a> (the latest version 2.5.2.0 at Windows), which engine can interpret “some of the language of SAS”. I took piece of codes for testing and some passed while some popped up with errors (so currently it is only a limited version of SAS). I don’t drive into the deep part yet of what WPS can do and can’t do, but I do love the WPS way to organize projects, folders and files (including souse files):

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="WPS_SAS" border="0" alt="WPS_SAS" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/11/WPS_SAS_thumb.png" width="507" height="380" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/11/WPS_SAS.png)

WPS uses a lite version of <a href="http://www.eclipse.org/" target="_blank">Eclipse</a> as GUI(WPS Workbench; the “lite” means WPS Workbench can’t be extensible as the original Eclipse but really with shorter response time). Besides its Project Explore for folders and files management(left panel), I also love its Outline in right panel to show the SAS programming elements and errors information in log window: 

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="WPS_LOG" border="0" alt="WPS_LOG" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/11/WPS_LOG_thumb.png" width="502" height="381" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/11/WPS_LOG.png) 

Then I’d like to switch to SAS itself. Frankly speaking, at least in IDE part, WPS looks pretty better than the current corresponding SAS:

[<img style="border-bottom: 0px; border-left: 0px; display: block; float: none; margin-left: auto; border-top: 0px; margin-right: auto; border-right: 0px" title="SAS_GUI" border="0" alt="SAS_GUI" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/11/SAS_GUI_thumb.png" width="495" height="406" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/11/SAS_GUI.png)

Of course I hold the principle of “substance over form”, but if available, the form itself also make people comfortable and enjoyable (for example, the Apple products…). As far as I know, the new version of SAS DI Studio and Enterprise Miner both have pretty much improvement in GUI from ergonomic point of view. Even for code editor, Enterprise Guide Editor&#160; is now more superior than so called SAS Enhanced Editor. But as a SAS programmer (not only the SAS user), I may spend all my day in the Base SAS window! 

I also spent some time to configure VIM as a relative simple SAS IDE as a temporally replacement (F3 to run, F5 to jump to program window, F6 to log window, F7 to output window just as the same as in SAS IDE):

[<img style="border-bottom: 0px; border-left: 0px; display: block; float: none; margin-left: auto; border-top: 0px; margin-right: auto; border-right: 0px" title="VIM_SAS" border="0" alt="VIM_SAS" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/11/VIM_SAS_thumb.png" width="488" height="575" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/11/VIM_SAS.png) It’s simple but always can do the job as SAS itself while looks really cool to comfort myself as a programmer. So, what’s going on in the next release? Still wait.