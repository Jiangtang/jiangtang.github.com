---
author: Jiangtang Hu
title: 'Sublime Text 2 for SAS Programmers: A Quick Note'
excerpt:
layout: post
category:
  - SAS
tags:
  - Notepad++
  - SAS
  - Sublime Text 2
  - VIM
post_format: [ ]
---
I’m playing with a new text editor, [Sublime Text 2][1], and it has much potentials to replace my current handy [Notepad++][2] and [VIM][3]. A quick note for further exploration(*will keep update*).

/\**\*|\*update: 2012-10-16, Roy  Pardee maintains a nice bundle ([*here*][4]), so the following bundle will be not updated any more.\*\*\*|\\*\*\*|\\*\*\*|\*\*/

Also created a Github repository to hold all my SAS configuration files for Sublime Text 2. Fork me at

> <https://github.com/Jiangtang/sas.tmbundle>

# 1. SAS syntax highlighting

Sublime Text 2 doesn’t support SAS syntax natively. I got a workaround so I didn’t need to write my own to play with it in the validation stage. Since  Sublime Text 2 supports [TextMate][5]’s syntax configuration, Just borrowed a [Textmate’s SAS syntax coloring theme][6] from [Jakob Stoeck][7] (thanks a lot man!).

This SAS coloring theme is Github hosted, so you can clone the files to the user created “SAS” folder (C:Program FilesSublime Text 2dataPackagesSAS; I use a Win 7 machine) if your Git is installed properly:

> git clone git://github.com/jakob-stoeck/sas.tmbundle SAS.tmbundle

or you can just simply save and copy this file to the SAS folder above:

> <https://raw.github.com/jakob-stoeck/sas.tmbundle/master/Syntaxes/SAS.tmLanguage>

Also can get from my repository forked from Jakob:

> <https://github.com/Jiangtang/sas.tmbundle/tree/master/Syntaxes>

Then you get

[![Sublime_SAS][9]][9]

Pretty nice, isn’t it? One of the neat functionalities of Sublime Text 2 is to open a folder as a project (showed in the left panel).

# 2. VI(M) Emulation

We can also easily launch Vi(M) mode in Sublime Text 2, see

> <http://www.sublimetext.com/docs/2/vintage.html>
> 
> <https://github.com/SublimeText/VintageEx>

# 3. Add Comments

Use this file from [my repository][9], *[Comments (SAS).tmPreferences][10]*, then you can use the Sublime Text 2 default key shortcuts 

[![comments][12]][12]

> **Ctrl+/** to add *comment; style comments(toggle), and
> 
> **Shift + ****Ctrl+/**  to add /\*comment\*/ style comments (toggle block)

Note that in SAS Enhanced Editor, we use **Ctrl+/ **to add toggle block comments.

# 4. Code Autocomplete

I added a few snippets in [my repository][9] to support some code autocomplete. 

[![snippets][13]][13]

For example, when type “s” and few alternatives show up,

[![sql][14]][14]

Hit RETURN and get

[![sql_auto][15]][15]

The neat thing is that your cursor is just in the shadow area /* variable(s)*/ after hitting RETURN where you can overwrite.

# 5. Run SAS within Sublime Text 2

Copy the following system build file to SAS package folder (mine, *C:UsersjhuAppDataRoamingSublime Text 2PackagesSAS*):

> {  
> “cmd”: ["SAS","-sysin","$file"],  
> “selector”: “source.sas”  
> }  
> 

> <https://github.com/Jiangtang/sas.tmbundle/blob/master/SAS.sublime-build>

Then you can run SAS code in Sublime Text 2 (by clicking “**Build**” or using shortcut **Ctrl+B**):

[![SublimeText2_SAS_build][16]][16]

Actually it is batch run mode and you will get all the output files (.log, .lst and .pdf, .png and such) in the same folder you hold you SAS codes.

I’m still working on how to set up interactive run mode and please leave any suggestions, comments and hints!

 [1]: http://www.sublimetext.com/
 [2]: http://support.sas.com/resources/papers/proceedings11/211-2011.pdf
 [3]: http://www.jiangtanghu.com/blog/2011/11/13/vim-as-a-sas-ide/
 [4]: http://implementing-vdw.blogspot.com/2012/10/new-sublime-text-package-available-for.html
 [5]: http://macromates.com/
 [6]: https://github.com/jakob-stoeck/sas.tmbundle
 [7]: https://github.com/jakob-stoeck
 []: http://dl.dropbox.com/u/69732603/Sublime_SAS.png
 [9]: https://github.com/Jiangtang/sas.tmbundle
 [10]: https://github.com/Jiangtang/sas.tmbundle/blob/master/Comments%20(SAS).tmPreferences
 []: http://dl.dropbox.com/u/69732603/comments.png
 []: http://dl.dropbox.com/u/69732603/snippets.png
 []: http://dl.dropbox.com/u/69732603/sql.png
 []: http://dl.dropbox.com/u/69732603/sql_auto.png
 []: http://dl.dropbox.com/u/69732603/SublimeText2_SAS_build.png