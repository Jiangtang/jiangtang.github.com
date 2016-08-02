---
author: Jiangtang Hu
title: Incorporate SAS/IML to Base SAS?
excerpt:
layout: post
category:
  - R
  - SAS
  - statistics
tags:
  - BASE SAS
  - IML
  - Matrix
  - R
  - SAS
post_format: [ ]
---
Since SAS 9.3, ODS Graphics was moved into Base SAS and other statistical procedures, which means the SAS/Graph license is not needed anymore to access ODS Graphics facilities. It’s definitely nice, but from customers’ point of view, it is not critical necessary: since the “minimum set of SAS system” in most SAS sessions includes the Base SAS, SAS/Stat and SAS/Graph, there is almost no impact for SAS users to switch the license of ODS Graphics. Actually, I do think SAS/IML is better to be included in BASE SAS (play Proc IML in BASE SAS; a MATRIX statement in data step is definitely another bonus) :

*   IML itself, seems have no intention to replace SAS/Stat, SAS/ETS, SAS/QC and other SAS statistical facilities in matrix way like R or Matlab. Instead, by enhancing the abilities to call SAS data steps(including macros), SAS Procedures and R inside,  IML seems to be glad as glue to leverage multiple programming elements. 
*   BASE SAS is a collection of lots of programming elements: data step, macro, SQL, array, hash, Java objects, ODS, XML and bunches of procedures. IML is clearly a programming tool rather than a specific application(SAS/Stat and such) and if it is added to BASE SAS, then the SAS programmers  will have one more data structure (matrix) to play with besides SAS table (R copies this idea as data frame), array and hash table (dictionary).
*   Actually it is an emergent need (for a matrix). Processing different rows in variable(s) is not an easy task in SAS data steps. Mostly SAS programmers utilize arrays (plus some tricky functions like LAG and DIF) and Dow-loop after its advent. There are really advanced programming techniques, but in matrix with index, such manipulation is pretty easy and straightforward (and saving your loops).
*   Although IML can communicate with BASE SAS, but for portable purpose (IML is not expected in every SAS session), most SAS programmers prefer to submit pure BASE codes for data processing. Furthermore, we can even understand why SAS programmers in general invest less in IML. It’s not good: just think about a BASE SAS programmer without a handy matrix manipulation tool (*and think about R*)!

Personally I played IML for a while and still keep eyes on its updates. But since I had some SAS machines without IML, I realize that IML can’t be used as a production language in my clinical SAS programming life: just can’t afford the latency  to ask IT administrators (including in clients side) to manage it!