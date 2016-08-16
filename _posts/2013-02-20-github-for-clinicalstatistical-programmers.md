---
id: 1151
title: Github for Clinical/Statistical Programmers
date: 2013-02-20T22:01:03+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1151
permalink: /2013/02/20/github-for-clinicalstatistical-programmers/
categories:
  - CDISC
  - Industry Review
  - misc
  - R
  - SAS
  - statistics
tags:
  - CDISC
  - CVS
  - FDA
  - Git
  - GIThub
  - GOOGLE Code
  - PhUSE
  - R
  - SAS
  - social coding
  - SVN
  - version control
---
<font size="1">PhUSE-FDA Working Group 5 (</font>[<font size="1">Development of Standard Scripts for Analysis and Programming</font>](http://www.phusewiki.org/wiki/index.php?title=Development_of_Standard_Scripts_for_Analysis_and_Programming)<font size="1">) just adopted </font>[<font size="1">Google Code</font>](http://code.google.com/p/phuse-scripts/) <font size="1">as collaborative programming platform. </font>[<font size="1">Google Code</font>](http://code.google.com/) <font size="1">is one of the most popular and respected open source software hosting sites in the world and it is definitely a good choice for PhUSE-FDA WG5.</font>

<font size="1">But after viewing one of WG5’s working reports, <em><a href="http://www.phusewiki.org/wiki/index.php?title=Platform_for_Standard_Script_Development:_Progress_as_of_September_18_2012">Sharing Standard Statistical Scripts</a></em> and getting to know why they finally chose Google Code (rather than </font>[<font size="1">Github</font>](https://github.com/) <font size="1">which was also tested by WG5 members), I think it’s necessary to clarify some misunderstanding against Github where I’m also <a href="https://github.com/Jiangtang">an occasional user</a>. </font>

<font size="1">As stated in </font>[<font size="1">Slide 11</font>](http://www.phusewiki.org/wiki/index.php?title=Platform_for_Standard_Script_Development:_Progress_as_of_September_18_2012) <font size="1">in the report mentioned before, Github,</font>

> <font size="1">Too complicated an interface <br />Too much overhead for simple development <br />Too much training and education needed</font>
> 
> <font size="1">designed for classic programming languages like C and Java (not for things like R and SAS)</font>

<font size="1">For the first point regarding <strong>interface</strong>, it seems only </font>[<font size="1">Git</font>](http://git-scm.com/) <font size="1">command line tested, and it may be too complicated to “<strong>classic</strong> statistical programming users”. Actually, Github offers a great GUI tool, for example, <em><a href="http://windows.github.com/">GitHub for Windows</a></em> to help users visually clone repositories, commit changes and other management tasks without typing Git commands: </font>

[<font size="1"><img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="Github_GUI" border="0" alt="Github_GUI" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/Github_GUI_thumb.png" width="487" height="427" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/Github_GUI.png)

<font size="1">It’s also worthy to mention that with </font>[_<font size="1">GitHub for Windows</font>_](http://windows.github.com/)<font size="1"><em>, </em>users don’t need to install any separated version control software like Git, CVS or SVN. </font>[_<font size="1">GitHub for Windows</font>_](http://windows.github.com/) <font size="1">already includes a fully functional version of </font>[<font size="1">msysGit</font>](http://msysgit.github.com/)<font size="1">. It just makes users’ life much simpler. To use Google Code, you must install and configure something like TortoiseSVN.</font>

<font size="1">The second, is Github suitable for “<strong>things like R and SAS</strong>”? It’s true that all hosts including </font>[<font size="1">Github</font>](https://github.com/languages) <font size="1">are dominated by “classic programming languages like C and Java”. For SAS, SAS programmers as a whole are just not active in&#160; any social coding activities, but for </font>[<font size="1">R</font>](https://github.com/languages/R)<font size="1">, actually it is </font>[<font size="1">one of the mostly used languages in Github</font>](https://www.google.com/webhp?sourceid=chrome-instant&ion=1&ie=UTF-8#q=github+top+languages+R&hl=en&ei=T4QlUeH-HJP62AXxqYGAAQ&start=10&sa=N&bav=on.2,or.r_gc.r_pw.r_cp.r_qf.&fp=50b26647ad5972f8&ion=1&biw=1536&bih=784)<font size="1">.</font>

<font size="1">Google Code is good and a “Google Code vs Github” question is just mostly subjective. It seems to me the pickup of Google Code by WG5 rather than Github was based on incomplete information. I personally prefer Github and there are also some good reasons:</font>

  * <font size="1">Use the GUI tool, </font>[_<font size="1">GitHub for Windows</font>_](http://windows.github.com/) <font size="1">to maintain a minimum Git/SVN/CVS setup.</font>
  * <font size="1">Github supplies much richer statistics reports, including charts.</font>
  * <font size="1">Github is more social oriented which makes it cool in this Web2.0 world.</font>