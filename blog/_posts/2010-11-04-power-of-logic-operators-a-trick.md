---
id: 146
title: 'Power of Logic Operators: a trick'
date: 2010-11-04T07:09:12+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=146
permalink: /2010/11/04/power-of-logic-operators-a-trick/
categories:
  - Logic
  - SAS
tags:
  - logic operator
---
Suppose you should group people based on their ages as follows:

> <div>
>   <table border="0" cellspacing="0" cellpadding="2" width="155" align="center">
>     <tr>
>       <td width="51" valign="top">
>         ID
>       </td>
>       
>       <td width="57" valign="top">
>         Age
>       </td>
>       
>       <td width="45" valign="top">
>         agegrp
>       </td>
>     </tr>
>     
>     <tr>
>       <td width="51" valign="top">
>         001
>       </td>
>       
>       <td width="57" valign="top">
>         1
>       </td>
>       
>       <td width="45" valign="top">
>         1
>       </td>
>     </tr>
>     
>     <tr>
>       <td width="51" valign="top">
>         002
>       </td>
>       
>       <td width="57" valign="top">
>         4
>       </td>
>       
>       <td width="45" valign="top">
>         2
>       </td>
>     </tr>
>     
>     <tr>
>       <td width="51" valign="top">
>         003
>       </td>
>       
>       <td width="57" valign="top">
>         5
>       </td>
>       
>       <td width="45" valign="top">
>         2
>       </td>
>     </tr>
>     
>     <tr>
>       <td width="51" valign="top">
>         004
>       </td>
>       
>       <td width="57" valign="top">
>         5
>       </td>
>       
>       <td width="45" valign="top">
>         2
>       </td>
>     </tr>
>     
>     <tr>
>       <td width="51" valign="top">
>         005
>       </td>
>       
>       <td width="57" valign="top">
>         2
>       </td>
>       
>       <td width="45" valign="top">
>         1
>       </td>
>     </tr>
>     
>     <tr>
>       <td width="51" valign="top">
>         006
>       </td>
>       
>       <td width="57" valign="top">
>         4
>       </td>
>       
>       <td width="45" valign="top">
>         2
>       </td>
>     </tr>
>     
>     <tr>
>       <td width="51" valign="top">
>         007
>       </td>
>       
>       <td width="57" valign="top">
>         5
>       </td>
>       
>       <td width="45" valign="top">
>         2
>       </td>
>     </tr>
>     
>     <tr>
>       <td width="51" valign="top">
>         008
>       </td>
>       
>       <td width="57" valign="top">
>         2
>       </td>
>       
>       <td width="45" valign="top">
>         1
>       </td>
>     </tr>
>     
>     <tr>
>       <td width="51" valign="top">
>         009
>       </td>
>       
>       <td width="57" valign="top">
>         9
>       </td>
>       
>       <td width="45" valign="top">
>         3
>       </td>
>     </tr>
>     
>     <tr>
>       <td width="51" valign="top">
>         010
>       </td>
>       
>       <td width="60" valign="top">
>         8
>       </td>
>       
>       <td width="56" valign="top">
>         3
>       </td>
>     </tr>
>   </table>
> </div>

and the rules:

> age<4,           group 1
> 
> 4<=age<6,     group 2
> 
> 6<=age<10,  group 3

It is a very simple question and you could use the **if/else** statement without thinking:

> <span style="font-family: 'Courier New';">data age;<br /> input ID $ age;<br /> datalines;<br /> 001 1<br /> 002 4<br /> 003 5<br /> 004 5<br /> 005 2<br /> 006 4<br /> 007 5<br /> 008 2<br /> 009 9<br /> 010 8<br /> ; </span>
> 
> <span style="font-family: 'Courier New';">data age1;<br /> set age;<br /> <span style="color: #ff0000;">if </span>age<4   then agegrp=1;<br /> <span style="color: #ff0000;">else if</span> age<6   then agegrp=2;<br /> else agegrp=3;<br /> run;<br /> proc print;run;</span>

or, you could use **proc format** to map data:

> <span style="font-family: 'Courier New';">proc <span style="color: #ff0000;">format</span>;<br /> value agegrp<br /> low-<4=&#8221;1&#8243;<br /> 4-<7  =&#8221;2&#8243;<br /> 7-<10 =&#8221;3&#8243;<br /> other =&#8221;&#8221;<br /> ;<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">data age2;<br /> set age;<br /> <span style="color: #ff0000;"> agegrp2=put(age,agegrp1.);</span><br /> run;<br /> proc print;run;</span>

And try to use logic operators. It is a **ONE-LINE-OF-CODE** approach:

> <span style="font-family: 'Courier New';">data age3;<br /> set age;<br /> <span style="color: #ff0000;"> agegrp3=1+(age>3)+(age>5);</span><br /> run;<br /> proc print;run;</span>

In SAS, a logic express returns to 1 or 0 according the true of false of the express. The logic behind the above statement is:

  * age group is set to 1 at the beginning;
  * if age>3, age group adds 1;
  * if age>5, add 1.

This easy-to-follow logic can apply to other scenarios(flags, for example):

 <span style="font-size: 13.1944px;">flag=value>50;</span>

 <span style="font-size: 13.1944px;">select value>50 as flag    <em>(in proc sql)</em></span>