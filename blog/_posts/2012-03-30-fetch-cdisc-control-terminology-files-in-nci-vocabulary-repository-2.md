---
author: Jiangtang Hu
title: 'Fetch CDISC Control Terminology Files in NCI Vocabulary Repository: All in One Click'
excerpt:
layout: post
category:
  - CDISC
  - SAS
tags:
  - CDISC
  - Control Terminology
  - GNU
  - NCI
  - Wget
post_format: [ ]
---
[CDISC Control Terminology][1] is the most frequent updated model among CDISC standards. Take SDTM as example, the latest SDTM terminologies released at 23 March 2012; and from 2009 to 2011, there were 15 different SDTM terminology versions! If you just rely on your own local repository, you might miss the pace somehow.

Here is a simple approach. Just submit the following one line of codes in a shell,

> wget <http://evs.nci.nih.gov/ftp1/CDISC/> -r –no-parent  -l 3

and you will get all the CDISC Control Terminology files (plus historical versions) with proper folder structures in your local driver (the current directory of your shell).

For syntax details, you can refer to its [online manual][2]:

> -r: recursive retrieving
> 
> –no-parent: only fetch files under the URL
> 
> -l 3: set maximum depth level of 3  

If you are a Windows user, you might install [Wget for Windows][3] (it is a native tool in Unix/Linux under GNU)and add it* *into your environmental variable, *Path*. You can also save the above scripts in a notepad and save it as a .bat file(*test.bat* for example). Next time you just click the *test.bat* to get all the updates.

Wget is a very powerful tool. For me, the download speed is pretty acceptable (depends on internet connection) and almost no difference between a Windows 7 and a Ubuntu 11 machine:

[![Wget_Win7][5]][5]

[![Wget_ubuntu11][6]][6]

 [1]: http://www.cdisc.org/terminology
 [2]: http://www.gnu.org/software/wget/manual/wget.html
 [3]: http://gnuwin32.sourceforge.net/packages/wget.htm
 []: http://dl.dropbox.com/u/69732603/Wget_Win7.png
 []: http://dl.dropbox.com/u/69732603/Wget_ubuntu11.png