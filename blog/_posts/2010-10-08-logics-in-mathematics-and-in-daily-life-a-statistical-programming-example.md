---
id: 131
title: 'Logics in mathematics and in daily life: a statistical programming example'
date: 2010-10-08T22:47:00+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2010/10/08/logics-in-mathematics-and-in-daily-life-a-statistical-programming-example/
permalink: /2010/10/08/logics-in-mathematics-and-in-daily-life-a-statistical-programming-example/
categories:
  - Logic
  - SAS
tags:
  - Logic
  - SAS
---
Refresh some [basic logical propositions](http://en.wikipedia.org/wiki/Contraposition) (or statements):

> <font color="#ff0000">implication</font>:&#160;&#160;&#160;&#160;&#160;&#160; if&#160;&#160;&#160;&#160;&#160;&#160; P then&#160;&#160;&#160;&#160;&#160;&#160; Q (P**—**>Q)
> 
> <font color="#ff0000">inverse</font>:&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; if not P then not Q (-P**—**>-Q)
> 
> converse:&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; if&#160;&#160;&#160;&#160;&#160;&#160; Q then&#160;&#160;&#160;&#160;&#160;&#160; P (Q**—**>P)
> 
> <font color="#ff0000">contrapositive</font>: if not Q then not P (-Q**—**>-P)
> 
> contradition:&#160;&#160;&#160; if&#160;&#160;&#160;&#160;&#160;&#160; P then not Q (P**—**>-Q)

Mathematically or logically speaking, if the <font color="#ff0000">implication</font> statement holds, then the <font color="#ff0000">contrapositive</font> holds, but the <font color="#ff0000">inverse</font> does not hold, i.e., _if P then Q_, then we can get _if not Q then not P_, but we can not get _if not P then not Q_.

That’s all logics needed here and Let’s turn to the ambiguous English in daily life. [James R. Munkres](http://en.wikipedia.org/wiki/James_Munkres) of MIT gave an example in _[Topology](http://www.amazon.com/Topology-2nd-James-Munkres/dp/0131816292/ref=sr_1_1?s=books&ie=UTF8&qid=1286432430&sr=1-1)_ (2nd edition, 2000, P.7):

> Mr. Jones, if&#160; you get a grade below&#160; 70 on&#160; the final, you are going to flunk&#160; this course.

We adapt it in a logical <font color="#ff0000">implication</font> form:

> Mr. Jones, if <font color="#ff0000">P </font>then <font color="#ff0000">Q</font>, where
> 
> <font color="#ff0000">P</font>: you get a grade below&#160; 70 on&#160; the final
> 
> <font color="#ff0000">Q</font>: you are going to flunk&#160; this course

Considering the context, we can also get that the <font color="#ff0000">inverse</font> holds: if you get a grade above er or equal to 70, then you are going to pass this course(if not P then not Q ).

Question: when do statistical programming, what types of logics you use? 

Answer: Not all mathematically. _see_

> if score<70 then grade="flunk";&#160; ***_if <font color="#ff0000">P</font> then <font color="#ff0000">Q</font>_**;   
> else&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; grade="pass";&#160; ***_if not P then not Q_**;