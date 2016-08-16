---
id: 1169
title: 'New Game in Town: SAS Metadata Administration'
date: 2013-03-13T21:46:35+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1169
permalink: /2013/03/13/new-game-in-town-sas-metadata-administration/
categories:
  - Business Intelligence
  - SAS
tags:
  - Blog
  - Metadata
  - SAS
---
<span style="font-size: xx-small;">You might also read that there were constant (although still not frequent) posts on SAS metadata querying and other administration tasks in SAS blogosphere since 2012 (<em>when I started to play with it^</em>). It is yet another evidence that more and more SAS programmers switched from SAS foundation to the so called SAS intelligent platform. In the traditional SAS foundation world, a nice source of metadata is the Dictionary table (or V datasets in SASHELP library); In SAS intelligent platform, a much more comprehensive metadata is stored in a SAS Metadata Server (<a href="http://www.guardian.co.uk/news/datablog/2010/jul/16/data-plural-singular"><em>Is &#8220;Data&#8221; singular or plural?</em></a>). </span>

<span style="font-size: xx-small;">To get started, <a href="http://blogs.sas.com/content/sgf/author/wendymchenry"><span style="font-size: xx-small;">Wendy McHenry</span></a> posted a nice introductory blog, <span style="font-size: xx-small;"><a href="http://blogs.sas.com/content/sgf/2012/12/05/why-i-love-sas-metadata/"><em>Why I love SAS metadata</em></a> and <a href="http://blogs.sas.com/content/bi/author/angelahall"><span style="font-size: xx-small;">Angela Hall</span></a>, <span style="font-size: xx-small;"><em><a href="http://blogs.sas.com/content/bi/2012/06/12/using-metabrowse-to-find-metadata/">How did you find that metadata?</a>, <a href="http://blogs.sas.com/content/sgf/author/jenniferparks"><span style="font-size: xx-small;">Jennifer Parks</span></a>, <span style="font-size: xx-small;"><a href="http://blogs.sas.com/content/sgf/2013/02/06/two-methods-for-editing-sas-metadata/">Two methods for editing SAS metadata</a>.</span></em></span></span></span>

<span style="font-size: xx-small;">To communicate with SAS Metadata Server programmingly, you can use </span>[<span style="font-size: xx-small;">Java</span>](http://support.sas.com/documentation/cdl/en/omaref/63063/HTML/default/viewer.htm#titlepage.htm) <span style="font-size: xx-small;">or </span>[<span style="font-size: xx-small;">Base SAS</span>](http://support.sas.com/documentation/cdl/en/lrmeta/63180/HTML/default/viewer.htm#titlepage.htm)<span style="font-size: xx-small;">  which are both well documented. </span>[<span style="font-size: xx-small;">Chris Hemedinger</span>](http://blogs.sas.com/content/sasdummy/author/chrishemedinger) <span style="font-size: xx-small;">recently shared bunch of posts on how to </span>[<span style="font-size: xx-small;">use PowerShell to talk with SAS Metadata Server</span>](http://blogs.sas.com/content/sasdummy/tag/sas-integration-technologies/)<span style="font-size: xx-small;">.</span>

<span style="font-size: xx-small;">Industry gurus </span>[<span style="font-size: xx-small;">Paul Homes</span>](http://blogs.sas.com/content/sgf/author/paulhomes) <span style="font-size: xx-small;">and </span>[<span style="font-size: xx-small;">Gregory Nelson</span>](http://blogs.sas.com/content/sgf/author/gregorynelson) <span style="font-size: xx-small;">also begin to blog in </span>[_<span style="font-size: xx-small;">SAS User Groups</span>_](http://blogs.sas.com/content/sgf/)<span style="font-size: xx-small;"><em> </em>on this subject (</span>[<span style="font-size: xx-small;">Paul’s own website</span>](http://platformadmin.com/blogs/paul/) <span style="font-size: xx-small;">is a great source too). </span>

<span style="font-size: xx-small;">A</span> <span style="font-size: xx-small;">community blog “<em><a href="http://www.bi-notes.com/">BI Notes</a></em>” also has some interesting posts on SAS metadata. Check it out.</span>

&#8212;&#8212;&#8212;update20140718: Useful Docs&#8212;&#8212;&#8212;

_SAS 9.3 Metadata Model: Reference ([HTML](http://support.sas.com/documentation/cdl/en/omamodref/63903/HTML/default/viewer.htm#titlepage.htm))_

_SAS 9.4 Open Metadata Interface: Reference and Usage ([PDF](http://support.sas.com/documentation/cdl/en/omaref/64859/PDF/default/omaref.pdf), [HTML](http://support.sas.com/documentation/cdl/en/omaref/64859/HTML/default/viewer.htm#titlepage.htm))_

_SAS 9.4 Language Interfaces to Metadata ([PDF](http://support.sas.com/documentation/cdl/en/lrmeta/64857/PDF/default/lrmeta.pdf), [HTML](http://support.sas.com/documentation/cdl/en/lrmeta/64857/HTML/default/viewer.htm#titlepage.htm))_

_SAS 9.4 Intelligence Platform: Security Administration Guide ([HTML](http://support.sas.com/documentation/cdl/en/bisecag/67045/HTML/default/titlepage.htm), [PDF](http://support.sas.com/documentation/cdl/en/bisecag/67045/PDF/default/bisecag.pdf))_

&nbsp;