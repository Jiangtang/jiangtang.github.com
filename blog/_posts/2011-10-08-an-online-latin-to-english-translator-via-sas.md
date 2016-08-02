---
id: 382
title: An Online Latin to English Translator via SAS
date: 2011-10-08T21:47:59+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/10/08/an-online-latin-to-english-translator-via-sas/
permalink: /2011/10/08/an-online-latin-to-english-translator-via-sas/
categories:
  - SAS
tags:
  - Google
  - Latin
  - SAS
  - Translate
---
Last month I submitted piece of SAS codes for a monthly programming challenge hosted by <a href="http://www.jiangtanghu.com/blog/2011/08/15/sas-bloggers-in-action-2-jian-dai-and-his-sas-academy/" target="_blank">Jian Dai</a> to <a href="http://blog.clinovo.com/programming-challenge-6-motto-of-hogwarts-school/" target="_blank">translate the Latin motto of Hogwarts School in Harry Potter</a> into English__:

> _draco dormiens nunquam titillandus_

You can get the meaning using Google search of course—but not in Google Translator (Google Translator can’t recognize all of such Latin words!). Jian posted a concise <a href="http://blog.clinovo.com/october-programming-challenge-ranking-american-heroes/" target="_blank">Perl way to parse webs</a> which contain this Latin phrase and key words “mean”,  “means” and such and you can always find <a href="http://www.ehow.com/about_6530758_meaning-__draco-dormiens___.html" target="_blank">page</a> like

> &#8220;draco dormiens nunquam titillandus,&#8221; which means &#8220;never tickle a sleeping dragon.&#8221;

My <a href="http://jiangtanghu.com/docs/en/Latin2Eng.sas" target="_blank">SAS approach</a> can’t return a human readable sentence like this one but a 100% word to word machine translation and you can use it to translate any Latin sentence which happens not appear in any singe web page. The usage is also very simple:

> filename L2E url &#8216;[http://jiangtanghu.com/docs/en/Latin2Eng.sas&#8217;;](http://jiangtanghu.com/docs/en/Latin2Eng.sas)
  
> %include L2E;
> 
> %Latin2Eng(<span style="color: #ff0000;">draco dormiens nunquam titillandus</span>)

and you get:

<p align="left">
  <span style="font-size: xx-small;"><strong>Obs   draco         dormiens                               nunquam                         titillandus</strong> </span>
</p>

<p align="left">
  <span style="font-size: xx-small;">1    dragon    sleep, rest                 at no time, never            tickle, titillate, provoke<br /> 2     snake     be/fall asleep          not in any circumstances     stimulate sensually<br /> 3                   behave as if asleep<br /> 4                   be idle, do nothing</span>
</p>

<p align="left">
  and also (2*4*2*2=) 32 Cartesian combinations to feel the meaning if needed.
</p>

<p align="left">
  Then you can also test the words by Julius Caesar:
</p>

> <p align="left">
>   %Latin2Eng(<span style="color: #ff0000;">Veni Vidi Vici</span>)
> </p>

and get:

**Obs   Veni       Vidi                                                                     Vici**

1     come    see, look at                                                     conquer, defeat, excel
  
2                 consider                                                           outlast
  
3                (PASS) seem, seem good, appear, be seen      succeed

This SAS translator is based on <a href="http://users.erols.com/whitaker/words.htm " target="_blank">WORDS (version 1.97FC) by William Whitaker</a> and the codes still needs some modifications when any unexpected special symbols popped up in the translating page.