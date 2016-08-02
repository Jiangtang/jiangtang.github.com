---
author: Jiangtang Hu
title: 'DoW-Loop: A Quick Note from SESUG 2012'
excerpt:
layout: post
category:
  - SAS
tags:
  - Do loop
  - DoW-Loop
  - SAS
post_format: [ ]
---
[![DoW][2]][2]

> ######     Once upon a midnight dreary,
> 
> ###### While I pondered, weak and weary, 
> 
> ######    Over many a quaint and curious
> 
> ######         Volume of SAS-L galore,
> 
> ######     While I coded, nearly snapping,
> 
> ######     Suddenly there came a tapping
> 
> ######     As of someone gently wrapping
> 
> ######       Code around my mental core.
> 
> ###### “’Tis’ Do-Whitlock Loop”, I muttered,
> 
> ######   “Wrapped around my brain core” -
> 
> ######      This it was, and so much more!  
> 
> ######   –[Paul Dorfman][2], *A Bit of DoW-History*

It’s great to have Paul Dorfman’s demo of DoW-loop (with a poem!* Thanks to Paul to send me a copy.*) in this [SESUG 2012 conference][3]. First posted in SAS-L by Whitlock, promoted by Dorfman,  DoW-loop is widely known as “[Whitlock Do Loop][4]” or ” Dorfman-Whitlock Do Loop”. In Dorfman’s presentation, the following three forms of DoW-loop were constructed:

*   Henderson-Whitlock Original Form of DoW-loop

*   Dorfman’s Short Form of DoW-loop

*   Double DoW-loop: the DeVenezia-Schreier Form

Using a test data set

> data a;   
>     input id $ var;   
> datalines;   
> A 1   
> A 2   
> B 3   
> B 4   
> B 5   
> ;

the Henderson-Whitlock Original Form of DoW-loop looks like:

> data b;   
>     count= 0;   
>     sum = 0 ;
> 
>     do until ( last.id ) ;   
>         set a ;   
>         by id ;
> 
>         count+1;   
>         sum+var;   
>     end ;
> 
>     mean = sum / count ;   
> run ;

Ian Whitlock first used such kind of do loop in [a SAS-L post][5] and after its rising, Paul Dorfman, the main promoter of DoW-loop, [found][6] that Don Henderson also made use such *DO UNTIL()* structure in a NESUG 1988 paper, *[The SAS Supervisor][7]*. That’s why he named it as Henderson-Whitlock form of DoW-loop. I then read from a [DoW-loop page in sascommunity.org][8] that Don Henderson taught such concept in class where Ian Whitlock was a student. This is a nice story.

Paul Dorfman himself also contributed a short form:

> data c ;   
>     do n = 1 by 1 until ( last.id ) ;   
>         set a ;   
>         by id ;
> 
>         count = sum (count, 1) ;   
>         sum = sum (sum, var) ;   
>     end ;
> 
>     mean = sum / count ;   
> run ;

or even shorter:

> data c ;   
>     do \_n\_ = 1 by 1 until ( last.id ) ;   
>         set a ;   
>         by id ;
> 
>         sum = sum (sum, var) ;   
>     end ;
> 
>     mean = sum / \_n\_ ;   
> run ;

These kinds of form of DoW-loop utilizes the SUM function, automatic variable \_N\_ and an increment trick in *DO UNTIL()* structure then the initializations before the loop are not needed any more. Besides such a short form, Paul Dorfman’s work on DoW-loop includes the invention of the dynamic file splitting method combining the DoW-loop and the hash object (also showed up in the meeting).

The double DoW-loop is under the name Howard Schreier and Richard DeVenezia (DeVenezia-Schreier Form; I should do more literature research on it!):

> data d ;   
>     do n = 1 by 1 until ( last.id ) ;   
>         set a ;   
>         by id ;
> 
>         count = sum (count, 1) ;   
>         sum = sum (sum, var) ;   
>     end ;
> 
>     mean = sum / count ;
> 
>     do n = 1 by 1 until ( last.id ) ;   
>         set a ;   
>         by id ;   
>         output;   
>     end ;   
> run ;

/\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\*\*\*|\\***|/

/\*\*\*|\*\***update 1**\*\*\*|\\*\*\*|\\***|/

Thanks to Quentin’s message, Don Henderson’s [*The SAS Supervisor*][7]* *can be even traced back to [1983][9].

/\*\*\*|\*\***update 2**\*\*\*|\\*\*\*|\\***|/

I used a Star Wars style of opening crawl to render Paul Dorfman’s DoW-loop verses simply because the finding of Don Henderson looks slightly like a prequel for me (although I have no intention to make up a Star Wars parody). Actually, as Paul stated, the honor belongs to an American author, Edgar Allan Poe and one of his poems, *[The Raven][10]*:

> Once upon a midnight dreary, while I pondered, weak and weary,   
> Over many a quaint and curious volume of forgotten lore —   
> While I nodded, nearly napping, suddenly there came a tapping,   
> As of some one gently rapping, rapping at my chamber door.   
> "’Tis some visiter," I muttered, "tapping at my chamber door —   
>             Only this and nothing more."

/\*\*\*|\*\***update 3**\*\*\*|\\*\*\*|\\***|/

[A double DoW demo][11] in recent SAS-L(Sat, 27 Oct 2012).

 []: http://dl.dropbox.com/u/69732603/DoW.png
 [2]: http://www.linkedin.com/in/pauldorfman
 [3]: http://www.sesug.org/SESUG2012/AcademicSections.php
 [4]: http://www.listserv.uga.edu/cgi-bin/wa?A2=ind0206B&L=sas-l&F=&S=&P=45520
 [5]: http://www.listserv.uga.edu/cgi-bin/wa?A2=ind0002C&L=sas-l&P=R5155
 [6]: http://support.sas.com/resources/papers/proceedings12/156-2012.pdf
 [7]: http://www.lexjansen.com/nesug/nesug88/sas_supervisor.pdf
 [8]: http://www.sascommunity.org/wiki/Do_until_last.var
 [9]: http://www.sascommunity.org/sugi/SUGI83/Sugi-83-171%20Henderson.pdf
 [10]: http://en.wikipedia.org/wiki/The_Raven
 [11]: http://listserv.uga.edu/cgi-bin/wa?A2=ind1210d&L=sas-l&T=0&P=20341