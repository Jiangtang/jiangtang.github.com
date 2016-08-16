---
id: 143
title: Recursive Referencing and Binomial Proportion Interval
date: 2010-11-03T20:47:44+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2010/11/03/recursive-referencing/
permalink: /2010/11/03/recursive-referencing/
categories:
  - Logic
  - misc
  - statistics
tags:
  - Binomial proportion inverval
  - Inception
  - Newcombe
  - recursion
---
To understand [recursion](http://en.wikipedia.org/wiki/Recursion), one of the most important concepts in programming languages, you could watch the movie, Chris Nolan’s _[Inception](www.inceptionmovie.com)_: it is about a dream within a dream within a dream, …and, read two statistical papers by Professor [Robert Newcombe](http://medicine.cf.ac.uk/en/person/prof-robert-gordon-newcombe/), one of the most [prolific statisticians](http://medicine.cf.ac.uk/en/person/prof-robert-gordon-newcombe/publications/):

  * <cite><a href="http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?cmd=Retrieve&db=pubmed&dopt=Abstract&list_uids=9595616&query_hl=1"><strong>Two-sided confidence intervals for the single proportion: comparison of seven methods.</strong></a> </cite>   
    Newcombe RG, <font color="#ff0000"><cite>Stat Med</cite> , Volume 17 , 8 (April 1998) pp.857-<strong>872</strong></font> ****
  * <cite><a href="http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?cmd=Retrieve&db=pubmed&dopt=Abstract&list_uids=9595617&query_hl=1"><strong>Interval estimation for the difference between independent proportions: comparison of eleven methods.</strong></a> </cite>   
    Newcombe RG, <font color="#ff0000"><cite>Stat Med</cite> , Volume 17 , 8 (April 1998) pp.<strong>873</strong>-890</font> 

These two widely cited papers evaluate 7 and 11 methods to calculate single proportion (paper <font color="#ff0000">A</font>) and the difference between proportions (paper <font color="#ff0000">B</font>), respectively. Further more, they were in the same issue of [_Statistics in Medicine_](http://onlinelibrary.wiley.com/journal/10.1002/(ISSN)1097-0258)(Volume 17, 1998), and, they were also cross referenced! So here is a live story about recursive referencing(thanks to Prof. Newcombe):

[<img style="border-bottom: 0px; border-left: 0px; display: block; float: none; margin-left: auto; border-top: 0px; margin-right: auto; border-right: 0px" title="megamonalisa_recursion" border="0" alt="megamonalisa_recursion" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2010/11/megamonalisa_recursion_thumb.jpg" width="245" height="371" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2010/11/megamonalisa_recursion.jpg)

  * An author writes two papers, A and B;
  * Paper B is in the&#160; bibliographic reference session of paper A;
  * Paper A is also in the&#160; bibliographic reference session of paper B;
  * Paper A and paper B are in the same issue of a journal.

<font color="#ff0000">Note</font> that for Prof. Newcombe’s two linked papers, it is common and acceptable in publication practices. Recently I used these two wonderful papers to learn CI calculation and this post just want to lead to the concept of “recursion”&#160; (reference in reference in reference).