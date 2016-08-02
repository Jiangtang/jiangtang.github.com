---
id: 1177
title: 'List Processing With SAS: A Github Repository'
date: 2013-03-31T22:24:02+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1177
permalink: /2013/03/31/list-processing-with-sas-a-github-repository/
categories:
  - SAS
tags:
  - GIThub
  - List
  - Macro
  - SAS
---
I have [a function like macro (recursive version) to create a sequence](http://jiangtanghu.com/docs/en/Latin2Eng.sas):

> <span style="font-family: 'Courier New';">%macro _list(n,pre=ff);<br /> %if &n=1 %then &pre.1;<br /> %else %_list(%eval(&n-1)),&pre.&n;<br /> %mend _list;</span>
> 
> <span style="font-family: 'Courier New';">%put %_list(3); *produces ff1, ff2, ff3;</span>

But when I read one of Ian Whitlock’s papers, _Names, Names, Names &#8211; Make Me a List_ ([SGF 2007](http://www2.sas.com/proceedings/forum2007/052-2007.pdf), [SESUG 2008](http://analytics.ncsu.edu/sesug/2008/SBC-128.pdf)),  I say: stop! I&#8217;m gonna use Ian’s %range and I create <a href="https://github.com/Jiangtang/SAS_ListProcessing/" target="_blank">Github </a>page to hold it (with minimum modifications due to personal preference).

I once posted [_My Collection of SAS Macro Repositories_](http://www.jiangtanghu.com/blog/2011/11/08/my-collection-of-sas-macro-repositories/)_ _credited to some SAS gurus like Richard DeVenezia. When facing a programming challenge, there is always a trade-off: should I take a look at what others wrote, or I just write from the scratch? Searching also needs lots of efforts, so I plan to utilize Github pages to minimum my own searching efforts and hope it would be helpful for you (no _intelligence waste anymore!_). I begin with SAS list processing:

<https://github.com/Jiangtang/SAS_ListProcessing/>

I got most of such utilities macros (with detailed comments, examples and sources) from papers, blogs and other websites and honors belong to their authors! Sometimes I will also add <a href="https://github.com/Jiangtang/SAS_ListProcessing/blob/master/slice.sas" target="_blank">my own</a> if I think there are some holes to fill up. To get start, you may read a _<a href="https://github.com/Jiangtang/SAS_ListProcessing/blob/master/README.md" target="_blank">READ ME </a>(will keep updated)_ first. Besides the individual macros, <a href="https://github.com/Jiangtang/SAS_ListProcessing/blob/master/_ListProcessing" target="_blank">a combined file</a> (trigged by <a href="https://github.com/Jiangtang/SAS_ListProcessing/blob/master/_ListProcessing_Combine.bat" target="_blank">a simple Dos command</a>) is also available.