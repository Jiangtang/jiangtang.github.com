---
author: Jiangtang Hu
title: Current Working Folder in SAS
excerpt:
layout: post
category:
  - Uncategorized
tags:
  - CMD
  - current folder
  - Powershell
  - SAS
  - Shell
post_format: [ ]
---
[![whereamI][2]][2]

The concept of [current working directory in SAS][2] is not as important as it sounds. Most SAS users point to file reference (fileref) and library reference (libname, a “namespace”-like mechanism to access files ), which are much convenient in large project with multiple folders.

Sometimes I push files to the current folder in relatively small task because I don’t want to

*   jump to *C:UsersjhuappdataLocalTempSAS Temporary Files\_TD2820\_*like folder to get the temporary datasets (in WORK library) 
*   hard code a folder to receive ODS outputs.

The demo codes(a SAS system autocall macro %xlog used):

> /*display current directory in LOG window*/   
> %xlog(cd);
> 
> /*change current working directory */   
> x "cd a:test";
> 
> /*display current directory in LOG window*/   
> %xlog(cd);
> 
> /*output a dataset in current directory */   
> data "iris";   
>     set sashelp.iris;   
> run;
> 
> /*output a pdf file in current directory */   
> ods pdf file="iris.pdf";   
> proc print data="iris";   
> run;   
> ods pdf close;
> 
> /*show files in current directory */   
> %xlog(dir);

And the LOG window may like:

> Path   
> —-   
> C:Usersjhu
> 
> Path   
> —-   
> A:test
> 
>     Directory: A:test   
> Mode        LastWriteTime   Length Name   
> —-        ————-   —— —-   
> -a— 10/8/2012  12:49 PM   113665 iris.pdf   
> -a— 10/8/2012  12:49 PM    13312 iris.sas7bdat

# NOTES:

*   You can get autocall macro %xlog in (if SAS 9.3 in Windows 7)

> C:Program FilesSASHomeSASFoundation9.3coresasmacro

An equivalent macro %xlst generates the shell command outputs to LIST window.

*   If prefer Windows Powershell, a similar macro can be used (put it to autocall if needed):

> %macro pslog(cmd);   
>   option nonotes;   
>   filename pslogcmd pipe "powershell &cmd";   
>   data \_null\_;   
>      file log;   
>      infile pslogcmd;   
>      input;   
>      put \_INFILE\_;   
>   run;   
>   option notes;   
> %mend pslog;

Test the following commands:

> %pslog(gl);   
> %pslog(get-location);   
> %pslog(get-host)

 []: http://dl.dropbox.com/u/69732603/whereamI.jpg
 [2]: http://support.sas.com/documentation/cdl/en/hostwin/63047/HTML/default/viewer.htm#p16esisc4nrd5sn1ps5l6u8f79k6.htm