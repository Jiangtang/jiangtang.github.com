---
id: 607
title: 'Sublime Text 2 for SAS Programmers: A Quick Note'
date: 2012-07-13T00:27:57+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=607
permalink: /2012/07/13/sublimetext2-sas/
categories:
  - SAS
tags:
  - Notepad++
  - SAS
  - Sublime Text 2
  - VIM
---
<span style="font-size: xx-small;">I’m playing with a new text editor, </span><a href="http://www.sublimetext.com/" target="_blank"><span style="font-size: xx-small;">Sublime Text 2</span></a><span style="font-size: xx-small;">, and it has much potentials to replace my current handy </span><a href="http://support.sas.com/resources/papers/proceedings11/211-2011.pdf" target="_blank"><span style="font-size: xx-small;">Notepad++</span></a> <span style="font-size: xx-small;">and </span><a href="http://www.jiangtanghu.com/blog/2011/11/13/vim-as-a-sas-ide/" target="_blank"><span style="font-size: xx-small;">VIM</span></a><span style="font-size: xx-small;">. A quick note for further exploration(<em>will keep update</em>).</span>

/\****update: 2012-10-16, Roy  Pardee maintains a nice bundle (<a href="http://implementing-vdw.blogspot.com/2012/10/new-sublime-text-package-available-for.html" target="_blank"><em>here</em></a>), so the following bundle will be not updated any more.\***\***\*****/

<span style="font-size: xx-small;">Also created a Github repository to hold all my SAS configuration files for Sublime Text 2. Fork me at</span>

> <span style="font-size: xx-small;"><a href="https://github.com/Jiangtang/sas.tmbundle">https://github.com/Jiangtang/sas.tmbundle</a></span>

# <span style="font-weight: bold;">1. SAS syntax highlighting</span>

<span style="font-size: xx-small;">Sublime Text 2 doesn’t support SAS syntax natively. I got a workaround so I didn’t need to write my own to play with it in the validation stage. Since  Sublime Text 2 supports </span><a href="http://macromates.com/" target="_blank"><span style="font-size: xx-small;">TextMate</span></a><span style="font-size: xx-small;">’s syntax configuration, Just borrowed a </span><a href="https://github.com/jakob-stoeck/sas.tmbundle" target="_blank"><span style="font-size: xx-small;">Textmate’s SAS syntax coloring theme</span></a> <span style="font-size: xx-small;">from </span><a href="https://github.com/jakob-stoeck" target="_blank"><span style="font-size: xx-small;">Jakob Stoeck</span></a> <span style="font-size: xx-small;">(thanks a lot man!).</span>

<span style="font-size: xx-small;">This SAS coloring theme is Github hosted, so you can clone the files to the user created “SAS” folder (C:Program FilesSublime Text 2dataPackagesSAS; I use a Win 7 machine) if your Git is installed properly:</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">git clone git://github.com/jakob-stoeck/sas.tmbundle SAS.tmbundle</span>

<span style="font-size: xx-small;">or you can just simply save and copy this file to the SAS folder above:</span>

> [<span style="font-size: xx-small;">https://raw.github.com/jakob-stoeck/sas.tmbundle/master/Syntaxes/SAS.tmLanguage</span>](https://raw.github.com/jakob-stoeck/sas.tmbundle/master/Syntaxes/SAS.tmLanguage)

<span style="font-size: xx-small;">Also can get from my repository forked from Jakob:</span>

> <https://github.com/Jiangtang/sas.tmbundle/tree/master/Syntaxes>

<span style="font-size: xx-small;">Then you get</span>

[<span style="font-size: xx-small;"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="Sublime_SAS" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/Sublime_SAS_thumb.png" alt="Sublime_SAS" width="528" height="396" border="0" /></span>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/Sublime_SAS.png)

<span style="font-size: xx-small;">Pretty nice, isn’t it? One of the neat functionalities of Sublime Text 2 is to open a folder as a project (showed in the left panel).</span>

# <span style="font-weight: bold;">2. VI(M) Emulation</span>

<span style="font-size: xx-small;">We can also easily launch Vi(M) mode in Sublime Text 2, see</span>

> [<span style="font-size: xx-small;">http://www.sublimetext.com/docs/2/vintage.html</span>](http://www.sublimetext.com/docs/2/vintage.html)
> 
> [<span style="font-size: xx-small;">https://github.com/SublimeText/VintageEx</span>](https://github.com/SublimeText/VintageEx)

# <span style="font-weight: bold;">3. Add Comments</span>

<span style="font-size: xx-small;">Use this file from <a href="https://github.com/Jiangtang/sas.tmbundle" target="_blank">my repository</a>, <em><a href="https://github.com/Jiangtang/sas.tmbundle/blob/master/Comments%20(SAS).tmPreferences" target="_blank">Comments (SAS).tmPreferences</a></em>, then you can use the Sublime Text 2 default key shortcuts </span>

[<img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="comments" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/comments_thumb.png" alt="comments" width="492" height="240" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/comments.png)

> <span style="font-size: xx-small;"><strong>Ctrl+/</strong> to add <span style="color: #ff0000;">*comment;</span> style comments(toggle), and</span>
> 
> <span style="font-size: xx-small;"><strong>Shift + </strong><span style="font-size: xx-small;"><strong>Ctrl+/</strong>  to add <span style="color: #ff0000;">/*comment*/</span> style comments (toggle block)</span></span>

<span style="font-size: xx-small;">Note that in SAS Enhanced Editor, we use <span style="font-size: xx-small;"><strong>Ctrl+/ </strong></span>to add toggle block comments.</span>

# <span style="font-weight: bold;">4. Code Autocomplete</span>

<span style="font-size: xx-small;">I added a few snippets in <a href="https://github.com/Jiangtang/sas.tmbundle" target="_blank">my repository</a> to support some code autocomplete. </span>

<span style="font-size: xx-small;"><a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/snippets.png"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="snippets" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/snippets_thumb.png" alt="snippets" width="500" height="279" border="0" /></a></span>

<span style="font-size: xx-small;">For example, when type “s” and few alternatives show up,</span>

<span style="font-size: xx-small;"><a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/sql.png"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="sql" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/sql_thumb.png" alt="sql" width="384" height="265" border="0" /></a></span>

<span style="font-size: xx-small;">Hit RETURN and get</span>

[<img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="sql_auto" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/sql_auto_thumb.png" alt="sql_auto" width="430" height="233" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/sql_auto.png)

<span style="font-size: xx-small;">The neat thing is that your cursor is just in the shadow area /* variable(s)*/ after hitting RETURN where you can overwrite.</span>

# 5. Run SAS within Sublime Text 2

<span style="font-size: xx-small;">Copy the following system build file to SAS package folder (mine, <em>C:UsersjhuAppDataRoamingSublime Text 2PackagesSAS</em>):</span>

> <span style="font-family: 'Courier New';">{<br /> &#8220;cmd&#8221;: [&#8220;SAS&#8221;,&#8221;-sysin&#8221;,&#8221;$file&#8221;],<br /> &#8220;selector&#8221;: &#8220;source.sas&#8221;<br /> }<br /> </span>

> <https://github.com/Jiangtang/sas.tmbundle/blob/master/SAS.sublime-build>

<span style="font-size: xx-small;">Then you can run SAS code in Sublime Text 2 (by clicking “<strong>Build</strong>” or using shortcut <strong>Ctrl+B</strong>):</span>

[<img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border: 0px;" title="SublimeText2_SAS_build" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/08/SublimeText2_SAS_build_thumb.png" alt="SublimeText2_SAS_build" width="485" height="384" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/08/SublimeText2_SAS_build.png)

<span style="font-size: xx-small;">Actually it is batch run mode and you will get all the output files (.log, .lst and .pdf, .png and such) in the same folder you hold you SAS codes.</span>

<span style="font-size: xx-small;">I’m still working on how to set up interactive run mode and please leave any suggestions, comments and hints!</span>