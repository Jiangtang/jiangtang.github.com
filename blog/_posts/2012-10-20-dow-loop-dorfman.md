---
id: 761
title: 'DoW-Loop: A Quick Note from SESUG 2012'
date: 2012-10-20T23:26:57+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=761
permalink: /2012/10/20/dow-loop-dorfman/
categories:
  - SAS
tags:
  - Do loop
  - DoW-Loop
  - SAS
---
<p align="justify">
  <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/DoW.png"><img style="background-image: none; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; padding-top: 0px; border-width: 0px;" title="DoW" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/DoW_thumb.png" alt="DoW" width="455" height="220" border="0" /></a>
</p>

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
> ###### “&#8217;Tis’ Do-Whitlock Loop”, I muttered,
> 
> ######   “Wrapped around my brain core” &#8211;
> 
> ######      This it was, and so much more!
> 
> ######   &#8212;<a href="http://www.linkedin.com/in/pauldorfman" target="_blank">Paul Dorfman</a>, _A Bit of DoW-History_

<p align="justify">
  <span style="font-size: xx-small;">It’s great to have Paul Dorfman’s demo of DoW-loop (with a poem!<em> Thanks to Paul to send me a copy.</em>) in this </span><a href="http://www.sesug.org/SESUG2012/AcademicSections.php" target="_blank"><span style="font-size: xx-small;">SESUG 2012 conference</span></a><span style="font-size: xx-small;">. First posted in SAS-L by Whitlock, promoted by Dorfman,  DoW-loop is widely known as “<span style="color: #ff0000;"><a href="http://www.listserv.uga.edu/cgi-bin/wa?A2=ind0206B&L=sas-l&F=&S=&P=45520" target="_blank">Whitlock Do Loop</a></span>” or ” <span style="color: #ff0000;">Do</span>rfman-<span style="color: #ff0000;">W</span>hitlock Do Loop”. In Dorfman’s presentation, the following three forms of DoW-loop were constructed:</span>
</p>

  * <div align="justify">
      <span style="font-size: xx-small;">Henderson-Whitlock Original Form of DoW-loop</span>
    </div>

  * <div align="justify">
      <span style="font-size: xx-small;">Dorfman’s Short Form of DoW-loop</span>
    </div>

  * <div align="justify">
      <span style="font-size: xx-small;">Double DoW-loop: the DeVenezia-Schreier Form</span>
    </div>

<p align="justify">
  <span style="font-size: xx-small;">Using a test data set</span>
</p>

> <span style="font-family: 'Courier New'; font-size: xx-small;">data a;<br /> input id $ var;<br /> datalines;<br /> A 1<br /> A 2<br /> B 3<br /> B 4<br /> B 5<br /> ;</span>

<p align="justify">
  <span style="font-size: xx-small;">the <span style="font-size: xx-small;">Henderson-Whitlock Original Form of DoW-loop looks like:</span></span>
</p>

> <span style="font-family: 'Courier New'; font-size: xx-small;">data b;<br /> count= 0;<br /> sum = 0 ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">    <span style="color: #ff0000;">do until ( last.id )</span> ;<br /> set a ;<br /> by id ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">        count+1;<br /> sum+var;<br /> end ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">    mean = sum / count ;<br /> run ;</span>

<p align="justify">
  <span style="font-size: xx-small;">Ian Whitlock first used such kind of do loop in <a href="http://www.listserv.uga.edu/cgi-bin/wa?A2=ind0002C&L=sas-l&P=R5155" target="_blank">a SAS-L post</a> and after its rising, Paul Dorfman, the main promoter of DoW-loop, <a href="http://support.sas.com/resources/papers/proceedings12/156-2012.pdf" target="_blank">found</a> that Don Henderson also made use such <em>DO UNTIL()</em> structure in a NESUG 1988 paper, <em><a href="http://www.lexjansen.com/nesug/nesug88/sas_supervisor.pdf" target="_blank">The SAS Supervisor</a></em>. That’s why he named it as <span style="font-size: xx-small;">Henderson-Whitlock form of DoW-loop. I then read from a <a href="http://www.sascommunity.org/wiki/Do_until_last.var" target="_blank">DoW-loop page in sascommunity.org</a> that Don Henderson taught such concept in class where Ian Whitlock was a student. This is a nice story.</span></span>
</p>

<p align="justify">
  <span style="font-size: xx-small;">Paul Dorfman himself also contributed a short form:</span>
</p>

> <span style="font-family: 'Courier New'; font-size: xx-small;">data c ;<br /> <span style="color: #ff0000;">do n = 1 by 1 until ( last.id )</span> ;<br /> set a ;<br /> by id ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">        count = <span style="color: #ff0000;">sum</span> (count, 1) ;<br /> sum = sum (sum, var) ;<br /> end ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">    mean = sum / count ;<br /> run ;</span>

<p align="justify">
  <span style="font-size: xx-small;">or even shorter:</span>
</p>

> <span style="font-family: 'Courier New'; font-size: xx-small;">data c ;<br /> do <span style="color: #ff0000;">_n_</span> = 1 by 1 until ( last.id ) ;<br /> set a ;<br /> by id ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">        sum = sum (sum, var) ;<br /> end ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">    mean = sum / _n_ ;<br /> run ;</span>

<p align="justify">
  <span style="font-size: xx-small;">These kinds of form of DoW-loop utilizes the SUM function, automatic variable _N_ and an increment trick in <em>DO UNTIL()</em> structure then the initializations before the loop are not needed any more. Besides such a short form, Paul Dorfman’s work on DoW-loop includes the invention of the dynamic file splitting method combining the DoW-loop and the hash object (also showed up in the meeting).</span>
</p>

<p align="justify">
  <span style="font-size: xx-small;">The double DoW-loop is under the name Howard Schreier and Richard DeVenezia (DeVenezia-Schreier Form; I should do more literature research on it!):</span>
</p>

> <span style="font-family: 'Courier New'; font-size: xx-small;">data d ;<br /> <span style="color: #ff0000;">do n = 1 by 1 until ( last.id )</span> ;<br /> set a ;<br /> by id ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">        count = sum (count, 1) ;<br /> sum = sum (sum, var) ;<br /> end ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">    mean = sum / count ;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">    <span style="color: #ff0000;">do n = 1 by 1 until ( last.id ) </span>;<br /> set a ;<br /> by id ;<br /> output;<br /> end ;<br /> run ;</span>

/\***\***\***\***\***\***\***/

<span style="font-size: xx-small;">/*****<strong>update 1</strong>*********/</span>

<span style="font-size: xx-small;">Thanks to Quentin’s message, Don Henderson’s </span>[_<span style="font-size: xx-small;">The SAS Supervisor</span>_](http://www.lexjansen.com/nesug/nesug88/sas_supervisor.pdf)<span style="font-size: xx-small;"><em> </em>can be even traced back to </span><a href="http://www.sascommunity.org/sugi/SUGI83/Sugi-83-171%20Henderson.pdf" target="_blank"><span style="font-size: xx-small;">1983</span></a><span style="font-size: xx-small;">.</span>

<span style="font-size: xx-small;">/*****<strong>update 2</strong>*********/</span>

<span style="font-size: xx-small;">I used a Star Wars style of opening crawl to render Paul Dorfman’s DoW-loop verses simply because the finding of Don Henderson looks slightly like a prequel for me (although I have no intention to make up a Star Wars parody). Actually, as Paul stated, the honor belongs to an American author, Edgar Allan Poe and one of his poems, <em><a href="http://en.wikipedia.org/wiki/The_Raven" target="_blank">The Raven</a></em>:</span>

> <span style="font-size: xx-small;">Once upon a midnight dreary, while I pondered, weak and weary,<br /> Over many a quaint and curious volume of forgotten lore —<br /> While I nodded, nearly napping, suddenly there came a tapping,<br /> As of some one gently rapping, rapping at my chamber door.<br /> &#8220;&#8216;Tis some visiter,&#8221; I muttered, &#8220;tapping at my chamber door —<br /> Only this and nothing more.&#8221;</span>

<span style="font-size: xx-small;">/*****<strong>update 3</strong>*********/</span>

<span style="font-size: xx-small;"><a href="https://listserv.uga.edu/cgi-bin/wa?A2=ind1210D&L=SAS-L&P=R11823" target="_blank">A double DoW demo</a> in recent SAS-L(</span>Sat, 27 Oct 2012<span style="font-size: xx-small;">).</span>