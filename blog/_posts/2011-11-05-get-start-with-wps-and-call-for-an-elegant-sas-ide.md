---
author: Jiangtang Hu
title: >
  Get Start with WPS, and Call for an
  Elegant SAS IDE!
excerpt:
layout: post
category:
  - SAS
tags:
  - IDE
  - SAS
  - VIM
  - WPS
post_format: [ ]
---
I got a trial version of [WPS][1] (the latest version 2.5.2.0 at Windows), which engine can interpret “some of the language of SAS”. I took piece of codes for testing and some passed while some popped up with errors (so currently it is only a limited version of SAS). I don’t drive into the deep part yet of what WPS can do and can’t do, but I do love the WPS way to organize projects, folders and files (including souse files):

[![WPS_SAS][3]][3]

WPS uses a lite version of [Eclipse][3] as GUI(WPS Workbench; the “lite” means WPS Workbench can’t be extensible as the original Eclipse but really with shorter response time). Besides its Project Explore for folders and files management(left panel), I also love its Outline in right panel to show the SAS programming elements and errors information in log window: 

[![WPS_LOG][5]][5] 

Then I’d like to switch to SAS itself. Frankly speaking, at least in IDE part, WPS looks pretty better than the current corresponding SAS:

[![SAS_GUI][6]][6]

Of course I hold the principle of “substance over form”, but if available, the form itself also make people comfortable and enjoyable (for example, the Apple products…). As far as I know, the new version of SAS DI Studio and Enterprise Miner both have pretty much improvement in GUI from ergonomic point of view. Even for code editor, Enterprise Guide Editor  is now more superior than so called SAS Enhanced Editor. But as a SAS programmer (not only the SAS user), I may spend all my day in the Base SAS window! 

I also spent some time to configure VIM as a relative simple SAS IDE as a temporally replacement (F3 to run, F5 to jump to program window, F6 to log window, F7 to output window just as the same as in SAS IDE):

[![VIM_SAS][7]][7] It’s simple but always can do the job as SAS itself while looks really cool to comfort myself as a programmer. So, what’s going on in the next release? Still wait.

 [1]: http://www.teamwpc.co.uk/products/wps
 []: http://dl.dropbox.com/u/69732603/WPS_SAS.png
 [3]: http://www.eclipse.org/
 []: http://dl.dropbox.com/u/69732603/WPS_LOG.png
 []: http://dl.dropbox.com/u/69732603/SAS_GUI.png
 []: http://dl.dropbox.com/u/69732603/VIM_SAS.png