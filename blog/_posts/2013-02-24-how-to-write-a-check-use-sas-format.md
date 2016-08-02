---
id: 1158
title: How to Write a Check? Use SAS Format!
date: 2013-02-24T21:59:02+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1158
permalink: /2013/02/24/how-to-write-a-check-use-sas-format/
categories:
  - SAS
tags:
  - format
  - Perl Regular Expression
  - SAS
---
[<font size="1"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="5write_a_check_step5_sign_memo" border="0" alt="5write_a_check_step5_sign_memo" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/5write_a_check_step5_sign_memo_thumb.jpg" width="441" height="208" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/5write_a_check_step5_sign_memo.jpg)

<font size="1">During my initial stay in US last year, one of the interesting exercises was </font>[<font size="1">to write a check</font>](http://banking.about.com/od/checkingaccounts/ig/How-to-Write-a-Check/How-to-Write-a-Check---Step-7.htm)<font size="1">. The Arabic numerals (<em>the universal language!</em>) were pretty intuitive while I didn’t feel much comfortable on spelling the face value in words: I never played the game! </font>

<font size="1">But the good side of this story was, as a SAS programmer and I used a </font>[<font size="1">WORDFw. Format</font>](http://support.sas.com/documentation/cdl/en/leforinforref/63324/HTML/default/viewer.htm#n1ncdkav4uqfwin1k5mow7z69avw.htm)<font size="1">:</font>

> <font size="1" face="Courier New">data _null_; <br />&#160;&#160;&#160; money=8.15; <br />&#160;&#160;&#160; put money <font color="#ff0000">wordf</font>100.; <br />run;</font>

<font size="1">and got:</font>

[<font size="1"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="SAS_Format_Check" border="0" alt="SAS_Format_Check" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/SAS_Format_Check_thumb.png" width="395" height="158" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/SAS_Format_Check.png)

<font size="1">Another check with a bigger value:</font>

[<font size="1"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="SAS_Format_Check2" border="0" alt="SAS_Format_Check2" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/SAS_Format_Check2_thumb.png" width="410" height="157" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/SAS_Format_Check2.png)

## <font size="1"><strong>2</strong></font>

<font size="1">I paid specially interested on SAS Format recently because of the introducing Perl Regular Expression into PROC FORMAT invalue statement since SAS 9.3(<em>an old procedure plays a new game!</em>). For example, a labeled TIME8. informat created by</font>

> <font size="1" face="Courier New">proc format; <br />&#160;&#160;&#160; invalue xxx (default=20) <br />&#160;&#160;&#160;&#160;&#160; &#8216;<font color="#ff0000">/(\d+):(\d\d)(?:\.(\d+))?/</font>&#8216; (REGEXP) = [time8.]; <br />run;</font>

<font size="1">For more, see Rick Langston’s paper, <em><a href="http://support.sas.com/resources/papers/proceedings12/245-2012.pdf">Using the New Features in PROC FORMAT</a></em> (2012).</font>