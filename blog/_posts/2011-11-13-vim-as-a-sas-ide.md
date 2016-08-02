---
author: Jiangtang Hu
title: Vim as A SAS IDE
excerpt:
layout: post
category:
  - SAS
tags:
  - IDE
  - SAS
  - VIM
post_format: [ ]
---
Few configurations (just copy this [*sas.vim*][1] file to *C:Program Filesvimvim73syntax* if you also use [gVIM 7.3][2] at Windows) to make Vim as a simple [SAS IDE][3] where

> F3: run SAS codes (in batch mode)  
> F4: close other two windows (the current active window is Log window after F3 running; F4 jump to SAS file with full window)
> 
> F5: jump to SAS file  
> F6: jump to Log file  
> F7: jump to lst file (list output)  
> F8: keep only the current window (full window)

![][4]

\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\**\*|\*

Details and Credits

1. The first post on Vim and SAS I read is by [Xiaowei Wang][5] in Chinese.

The original SAS syntax file took from [Zhenhuan Hu][6].

[Kent Nassen][7] also maintains some Vim functions to run SAS codes and check log.

2. To run SAS codes using F3:

> map <F3> :w<CR>:!SAS % -CONFIG “C:Program FilesSASSASFoundation9.2nlsenSASV9.CFG“<CR>:sp  %<.lst<CR>:sp  %<.log<CR>

3. Close other windows using F4:

> map <F4> :close<CR>:close<CR>

4. Keep only current window using F8:

> map <F8> : only<CR>

5. Jump to SAS file using F5:

> map <F5> :e %<.sas<CR>

6. Jump to Log file using F6:

> map <F6> :e %<.log<CR>

7. Jump to Lst file using F7:

> map <F7> :e %<.lst<CR>

 [1]: http://jiangtanghu.com/docs/en/sas.vim
 [2]: ftp://ftp.vim.org/pub/vim/pc/gvim73_46.ex
 [3]: http://www.jiangtanghu.com/blog/2011/11/05/get-start-with-wps-and-call-for-an-elegant-sas-ide/
 [4]: http://dl.dropbox.com/u/69732603/VIM_SAS.png
 [5]: http://www.blog496.org/2011-7-17-win-use-vim-as-sas-r-editor.html
 [6]: http://www.vim.org/scripts/script.php?script_id=3522
 [7]: http://www-personal.umich.edu/~knassen/vim/sasfns.html