---
author: Jiangtang Hu
title: 'Extract the Version of SAS and OS of a SAS Format or Macro Catalog: A Little Bit of Perl Regular Expression'
excerpt:
layout: post
category:
  - Computer
  - SAS
tags:
  - format
  - Macro
  - Perl Regular Expression
  - SAS
post_format: [ ]
---
SAS Sample 34444(*[Determine the operating system in which a format catalog was created][1]*) posts piece of codes to get the version of SAS and OS of a SAS format catalog. It is useful since a SAS catalog can be only read in the operating systems same to its source machine.

2 cents add to this note:

First, we do not need to write codes to get to know the machine version for a catalog(***formats.sas7bcat ***or** *sasmacr.sas7bcat***). Just open the catalog using a text editor, Notepad++, then you get

> a SAS format catalog created by SAS 9.1 in a Windows XP Pro machine:

[![SAS_Format][3]][3]

> and a SAS macro catalog by SAS 9.3 in a 64 bits Windows 7 Pro machine:

[![SAS_Macro][4]][4]

Second, if do want programming (for curiosity purpose; I like this idea), we can also improve the sample codes since the position and length information were hard coded in Line 21 (the question is: how can we know that?):

> test=substr(theline,210,20);

To get rid of hard coding, I use Perl Regular Expression. Just copy the archived codes for [my SESUG 2012 talk][4] with tiny modification (I always use the same programming blocks if possible):

[https://github.com/Jiangtang/SESUG2012/blob/master/read_SAP.sas][5]

The following codes can be also used to run against SAS macro catalog:

> filename fmt "a:formats.sas7bcat";
> 
> data fmt;   
>    infile fmt lrecl=1000 truncover;   
>    input line $1000.;   
> run;
> 
> data \_null\_;   
>     set fmt;   
>          if \_n\_=1 then do;   
>             retain queVer;
> 
>             ver="/(d+).[dw]+_[dw]+/";   
>             queVer  = prxparse(ver);
> 
>             if missing(queVer) then do;   
>                putlog "ERROR: Invalid regexp" ver;   
>                stop;   
>             end;   
>       end;
> 
>       queVerN  = prxmatch(queVer ,line);
> 
>       if queVerN > 0  then do ;   
>               call PRXsubstr(queVer,line,position,length);   
>             version = compress(substr(line, position, length));   
>             output;   
>       end;    
> 
>       put position= length=;   
>       put version=;   
> run;   
> 

Test it against five Windows machines: 

> position=221 length=16   
> version=9.0301M1X64_7PRO
> 
> position=217 length=15   
> version=9.0202M2NET_SRV 
> 
> position=221 length=17   
> version=9.0202M3X64_SRV08 
> 
> position=217 length=14   
> version=9.0100A0XP_PRO
> 
> position=217 length=15   
> version=9.0101M3NET_SRV 



P.S.: The pattern **(d+).[dw]+_[dw]+**  can be read as

> number(s)                       +   
> .                                      +   
> some digits and words     +   
> _                                     +   
> some digits and words

Since the underscore “_” is also included in meta-character **w**, it seems OK to simplify the pattern above to 

> **(d+).[dw]+ **

But in a Window Server 2003 machine with SAS 9.2, it also returns the following unrelated information:

> position=998 length=3   
> version=2.S

 [1]: http://support.sas.com/kb/34/443.html
 []: http://dl.dropbox.com/u/69732603/SAS_Format.png
 []: http://dl.dropbox.com/u/69732603/SAS_Macro.png
 [4]: http://www.sesug.org/SESUG2012/abstract.html#BB-04
 [5]: https://github.com/Jiangtang/SESUG2012/blob/master/read_SAP.sas "https://github.com/Jiangtang/SESUG2012/blob/master/read_SAP.sas"