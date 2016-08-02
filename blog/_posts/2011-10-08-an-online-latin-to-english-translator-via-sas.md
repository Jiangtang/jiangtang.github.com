---
author: Jiangtang Hu
title: >
  An Online Latin to English Translator
  via SAS
excerpt:
layout: post
category:
  - SAS
tags:
  - Google
  - Latin
  - SAS
  - Translate
post_format: [ ]
---
Last month I submitted piece of SAS codes for a monthly programming challenge hosted by [Jian Dai][1] to [translate the Latin motto of Hogwarts School in Harry Potter][2] into English**:

> *draco dormiens nunquam titillandus*

You can get the meaning using Google search of course—but not in Google Translator (Google Translator can’t recognize all of such Latin words!). Jian posted a concise [Perl way to parse webs][3] which contain this Latin phrase and key words “mean”,  “means” and such and you can always find [page][4] like

> “draco dormiens nunquam titillandus,” which means “never tickle a sleeping dragon.”

My [SAS approach][5] can’t return a human readable sentence like this one but a 100% word to word machine translation and you can use it to translate any Latin sentence which happens not appear in any singe web page. The usage is also very simple:

> filename L2E url ‘[http://jiangtanghu.com/docs/en/Latin2Eng.sas’;][5]  
> %include L2E;
> 
> %Latin2Eng(draco dormiens nunquam titillandus)

and you get:

**Obs   draco         dormiens                               nunquam                         titillandus** 

1    dragon    sleep, rest                 at no time, never            tickle, titillate, provoke  
2     snake     be/fall asleep          not in any circumstances     stimulate sensually  
3                   behave as if asleep  
4                   be idle, do nothing

and also (2\*4\*2*2=) 32 Cartesian combinations to feel the meaning if needed.

Then you can also test the words by Julius Caesar:

> %Latin2Eng(Veni Vidi Vici)

and get:

**Obs   Veni       Vidi                                                                     Vici**

1     come    see, look at                                                     conquer, defeat, excel  
2                 consider                                                           outlast  
3                (PASS) seem, seem good, appear, be seen      succeed

This SAS translator is based on [WORDS (version 1.97FC) by William Whitaker][6] and the codes still needs some modifications when any unexpected special symbols popped up in the translating page.

 [1]: http://www.jiangtanghu.com/blog/2011/08/15/sas-bloggers-in-action-2-jian-dai-and-his-sas-academy/
 [2]: http://blog.clinovo.com/programming-challenge-6-motto-of-hogwarts-school/
 [3]: http://blog.clinovo.com/october-programming-challenge-ranking-american-heroes/
 [4]: http://www.ehow.com/about_6530758_meaning-__draco-dormiens___.html
 [5]: http://jiangtanghu.com/docs/en/Latin2Eng.sas
 [6]: http://users.erols.com/whitaker/words.htm