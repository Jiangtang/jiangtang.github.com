---
author: Jiangtang Hu
title: >
  Recursive Referencing and Binomial
  Proportion Interval
excerpt:
layout: post
category:
  - Logic
  - misc
  - statistics
tags:
  - Binomial proportion inverval
  - Inception
  - Newcombe
  - recursion
post_format: [ ]
---
To understand [recursion][1], one of the most important concepts in programming languages, you could watch the movie, Chris Nolan’s *[Inception][2]*: it is about a dream within a dream within a dream, …and, read two statistical papers by Professor [Robert Newcombe][3], one of the most [prolific statisticians][4]:

*   [**Two-sided confidence intervals for the single proportion: comparison of seven methods.**][5]    
    Newcombe RG, Stat Med , Volume 17 , 8 (April 1998) pp.857-**872**** **
*   [**Interval estimation for the difference between independent proportions: comparison of eleven methods.**][6]    
    Newcombe RG, Stat Med , Volume 17 , 8 (April 1998) pp.**873**-890 

These two widely cited papers evaluate 7 and 11 methods to calculate single proportion (paper A) and the difference between proportions (paper B), respectively. Further more, they were in the same issue of [*Statistics in Medicine*][7](Volume 17, 1998), and, they were also cross referenced! So here is a live story about recursive referencing(thanks to Prof. Newcombe):

[![megamonalisa_recursion][9]][9]

*   An author writes two papers, A and B;
*   Paper B is in the  bibliographic reference session of paper A;
*   Paper A is also in the  bibliographic reference session of paper B;
*   Paper A and paper B are in the same issue of a journal.

Note that for Prof. Newcombe’s two linked papers, it is common and acceptable in publication practices. Recently I used these two wonderful papers to learn CI calculation and this post just want to lead to the concept of “recursion”  (reference in reference in reference).

 [1]: http://en.wikipedia.org/wiki/Recursion
 [2]: www.inceptionmovie.com
 [3]: http://medicine.cf.ac.uk/en/person/prof-robert-gordon-newcombe/
 [4]: http://medicine.cf.ac.uk/en/person/prof-robert-gordon-newcombe/publications/
 [5]: http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?cmd=Retrieve&db=pubmed&dopt=Abstract&list_uids=9595616&query_hl=1
 [6]: http://www.ncbi.nlm.nih.gov/entrez/query.fcgi?cmd=Retrieve&db=pubmed&dopt=Abstract&list_uids=9595617&query_hl=1
 [7]: http://onlinelibrary.wiley.com/journal/10.1002/(ISSN)1097-0258
 []: http://dl.dropbox.com/u/69732603/megamonalisa_recursion.jpg