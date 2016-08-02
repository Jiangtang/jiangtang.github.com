---
author: Jiangtang Hu
title: 'Logics in mathematics and in daily life: a statistical programming example'
excerpt:
layout: post
category:
  - Logic
  - SAS
tags:
  - Logic
  - SAS
post_format: [ ]
---
Refresh some [basic logical propositions][1] (or statements):

> implication:       if       P then       Q (P**—**>Q)
> 
> inverse:            if not P then not Q (-P**—**>-Q)
> 
> converse:         if       Q then       P (Q**—**>P)
> 
> contrapositive: if not Q then not P (-Q**—**>-P)
> 
> contradition:    if       P then not Q (P**—**>-Q)

Mathematically or logically speaking, if the implication statement holds, then the contrapositive holds, but the inverse does not hold, i.e., *if P then Q*, then we can get *if not Q then not P*, but we can not get *if not P then not Q*.

That’s all logics needed here and Let’s turn to the ambiguous English in daily life. [James R. Munkres][2] of MIT gave an example in *[Topology][3]* (2nd edition, 2000, P.7):

> Mr. Jones, if  you get a grade below  70 on  the final, you are going to flunk  this course.

We adapt it in a logical implication form:

> Mr. Jones, if P then Q, where
> 
> P: you get a grade below  70 on  the final
> 
> Q: you are going to flunk  this course

Considering the context, we can also get that the inverse holds: if you get a grade above er or equal to 70, then you are going to pass this course(if not P then not Q ).

Question: when do statistical programming, what types of logics you use? 

Answer: Not all mathematically. *see*

> if score<70 then grade="flunk";  ****if P then Q***;   
> else                    grade="pass";  ****if not P then not Q***;

 [1]: http://en.wikipedia.org/wiki/Contraposition
 [2]: http://en.wikipedia.org/wiki/James_Munkres
 [3]: http://www.amazon.com/Topology-2nd-James-Munkres/dp/0131816292/ref=sr_1_1?s=books&ie=UTF8&qid=1286432430&sr=1-1