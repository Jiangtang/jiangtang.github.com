---
author: Jiangtang Hu
title: 'Power of Logic Operators: a trick'
excerpt:
layout: post
category:
  - Logic
  - SAS
tags:
  - logic operator
post_format: [ ]
---
Suppose you should group people based on their ages as follows:

> | ID  | Age | agegrp |
> ||
> | 001 | 1   | 1      |
> | 002 | 4   | 2      |
> | 003 | 5   | 2      |
> | 004 | 5   | 2      |
> | 005 | 2   | 1      |
> | 006 | 4   | 2      |
> | 007 | 5   | 2      |
> | 008 | 2   | 1      |
> | 009 | 9   | 3      |
> | 010 | 8   | 3      |

and the rules:

> age<4,           group 1
> 
> 4<=age<6,     group 2
> 
> 6<=age<10,  group 3

It is a very simple question and you could use the **if/else **statement without thinking:

> data age;  
> input ID $ age;  
> datalines;  
> 001 1  
> 002 4  
> 003 5  
> 004 5  
> 005 2  
> 006 4  
> 007 5  
> 008 2  
> 009 9  
> 010 8  
> ; 
> 
> data age1;  
> set age;  
> if age<4   then agegrp=1;  
> else if age<6   then agegrp=2;  
> else agegrp=3;  
> run;  
> proc print;run;

or, you could use **proc format** to map data:

> proc format;  
> value agegrp  
> low-<4=”1″  
> 4-<7  =”2″  
> 7-<10 =”3″  
> other =”"  
> ;  
> run; 
> 
> data age2;  
> set age;  
>  agegrp2=put(age,agegrp1.);  
> run;  
> proc print;run;

And try to use logic operators. It is a **ONE-LINE-OF-CODE** approach:

> data age3;  
> set age;  
>  agegrp3=1+(age>3)+(age>5);  
> run;  
> proc print;run;

In SAS, a logic express returns to 1 or 0 according the true of false of the express. The logic behind the above statement is:

*   age group is set to 1 at the beginning;
*   if age>3, age group adds 1;
*   if age>5, add 1.

This easy-to-follow logic can apply to other scenarios(flags, for example):

 flag=value>50;

 select value>50 as flag    *(in proc sql)*