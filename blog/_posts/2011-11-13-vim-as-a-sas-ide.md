---
id: 438
title: Vim as A SAS IDE
date: 2011-11-13T11:11:14+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/11/13/vim-as-a-sas-ide/
permalink: /2011/11/13/vim-as-a-sas-ide/
categories:
  - SAS
tags:
  - IDE
  - SAS
  - VIM
---
Few configurations (just copy this <a href="http://jiangtanghu.com/docs/en/sas.vim" target="_blank"><em>sas.vim</em></a> file to _C:\Program Files\vim\vim73\syntax_ if you also use <a href="ftp://ftp.vim.org/pub/vim/pc/gvim73_46.ex" target="_blank">gVIM 7.3</a> at Windows) to make Vim as a simple <a href="http://www.jiangtanghu.com/blog/2011/11/05/get-start-with-wps-and-call-for-an-elegant-sas-ide/" target="_blank">SAS IDE</a> where

> F3: run SAS codes (in batch mode)
  
> F4: close other two windows (the current active window is Log window after F3 running; F4 jump to SAS file with full window)
> 
> F5: jump to SAS file
  
> F6: jump to Log file
  
> F7: jump to lst file (list output)
  
> F8: keep only the current window (full window)

<img style="display: block; float: none; margin-left: auto; margin-right: auto;" alt="" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/11/VIM_SAS.png" />

\***\***\***\***\****

Details and Credits

1. The first post on Vim and SAS I read is by <a href="http://www.blog496.org/2011-7-17-win-use-vim-as-sas-r-editor.html" target="_blank">Xiaowei Wang</a> in Chinese.

The original SAS syntax file took from <a href="http://www.vim.org/scripts/script.php?script_id=3522" target="_blank">Zhenhuan Hu</a>.

<a href="http://www-personal.umich.edu/~knassen/vim/sasfns.html" target="_blank">Kent Nassen</a> also maintains some Vim functions to run SAS codes and check log.

2. To run SAS codes using F3:

> <span style="font-family: 'Courier New';">map <F3> :w<CR>:!SAS % -CONFIG &#8220;<span style="color: #ff0000;">C:\Program Files\SAS\SASFoundation\9.2\nls\en\SASV9.CFG</span>&#8220;<CR>:sp  %<.lst<CR>:sp  %<.log<CR></span>

3. Close other windows using F4:

> <span style="font-family: 'Courier New';">map <F4> :close<CR>:close<CR></span>

4. Keep only current window using F8:

> <span style="font-family: 'Courier New';">map <F8> : only<CR></span>

5. Jump to SAS file using F5:

> <span style="font-family: 'Courier New';">map <F5> :e %<.sas<CR></span>

6. Jump to Log file using F6:

> <span style="font-family: 'Courier New';">map <F6> :e %<.log<CR></span>

7. Jump to Lst file using F7:

> <span style="font-family: 'Courier New';">map <F7> :e %<.lst<CR></span>