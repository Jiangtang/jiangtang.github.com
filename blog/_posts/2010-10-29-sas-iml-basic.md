---
author: Jiangtang Hu
title: 'Play Matrix within SAS(1): basic files processing'
excerpt:
layout: post
category:
  - SAS
tags:
  - IML
  - Matrix
  - SAS
post_format: [ ]
---
Recently I read Rick Wicklin’s [IML blog][1] with great interests(and anticipation for his fore-coming IML book,  *[Statistical Programming with SAS/IML Software][2]*). SAS programmers have the following programming tools to facilitate their daily work:

*   SAS data step: the basic SAS; a generation IV programming language, similar with other procedural languages such as C. 
*   SAS Proc SQL: SAS’s implementation of standard SQL([SQL-92][3]). 
*   SAS IML(Interactive Matrix Language): SAS’s matrix manipulation language(like R and Matlab).  SAS IML Studio also supply IMLPlus programming language(IML+), an enhanced version of IML. 
*   SAS SCL(SAS Component Language): build in SAS/AF software, an object oriented programming(OOP) language for applications development. 

I am a heavy user of data steps and SQL and want to invest some bit on matrix manipulation. Although other wonderful languages available(such as R and Matlab), I found IML is a good choice for SAS programmers like me. It is well integrated within SAS system, and very important, almost all of the SAS Base functions and call routines are also supported by IML. Here some notes of IML 101(codes are self explanatory from a SAS Base point of view):

# **1. IML style of ‘hello world’** 

> proc iml;   
>     text="Hello World!";   
>     print "IML saying" text;   
> quit;

and you got in output window:

> IML saying Hello World!

Like Proc SQL, IML begins with “proc iml” , end with ”quit”, and every statements end with a semicolon. The key word “print” (an IML statement), just like “put” statement in data steps.

An enhanced version of Hello World: 

> options nocenter nodate nonumber; 
> 
> proc iml;   
>     reset printall; 
> 
>     text="Hello World!";   
>     print "in &sysdate. IML saying" text;   
> quit;

Some SAS global options added(“nocenter nodate nonumber”). The IML statement “reset", works like “options” statement to set some processing options within the IML(and you can guess the meaning of the options “printall”, just print all. . . it is your turn to check the output window).

A SAS system macro variable “&sysdate” is presented to encourage you to add any programming elements in SAS Base to IML. 

# **2. How to create a matrix manually**

Actually, we have already create a matrix named “text” in the previous hello-world codes. It is a character scalar(matrix with only one element). If we want to avoid the SAS data steps’ style of assignment,  we can use *{}* to enclose matrix elements:

> a={“a”};  /*a \_char\_ scalar */   
> b={1};     /*a \_num\_ scalar*/

and a 2*3 matrix:

> c={1 2 3,   
>       2 3 4}; /*2 rows, 3 cols*/

Commas(,) are used to separate rows.

# 3. How to create a matrix by functions

Some matrix reshaping functions:

> a=I(3);     /*creates a 3*3 identity matrix*/   
> b=J(2,3,5); /*creates a 2*3 matrix of identical values*/   
> e=do(1,9,2); /*produces series, from 1 to 9, by increment 2*/   
> c=block(a,b);/*forms a block-diagonal matrice*/   
> d=diag(a);   /*creates a diagonal matrix*/   
> m=repeat(a,4,3); /*create a (3\*4)\*(3*3) matrix by repeating*/   
> n=T(b);   /\*transpose\*/

# 4. How to create a matrix by reading a SAS data set

> proc iml;   
>     use sashelp.class;   
>     read all var \_char\_                    into class_char;   
>     read all var \_num\_                     into class_num;   
>     read all var {"Age" "Height" "Weight"} into class_num2;   
>     close sashelp.class; 
> 
>     print class\_char class\_num class_num2;   
> quit;

Note that it is a good habit to close the data file after reading or using it(*see* Rick Wicklin’s *[Five Reasons to CLOSE Your Data Sets][4]*).

# 5. How to output a matrix to SAS dataset

> proc iml;   
>     use sashelp.class;   
>     read all var \_num\_ into class_num;   
>     close sashelp.class; 
> 
>     create work.class_num from class_num;   
>     append from class_num;   
>     show datasets;   
> quit;

#  

# 6. How to format a matrix

/*version I: use matrix options*/

> proc iml;   
>         use sashelp.class;   
>         col={"Age" "Height" "Weight"};   
>         read all var col into class;   
>         read all var{name} into row;   
>         close sashelp.class; 
> 
>         print class[rowname=row   
>                     colname=col   
>                     format=5.2   
>                     label="test, label"];   
> quit; 

/*version II: use mattib statement*/

> proc iml;   
>         use sashelp.class;   
>         col={"Age" "Height" "Weight"};   
>         read all var col into class;   
>         read all var{name} into row;   
>         close sashelp.class; 
> 
>         mattrib class rowname=row   
>                       colname=col   
>                       label="test, label"   
>                      format=5.2;   
>         print class;   
> quit; 

/*version III: avoid hardcoding—use IML function and operations*/

> proc iml;   
>         use sashelp.class;   
>         col=T(contents(sashelp,class)[3:5]);   
>         read all var col into class;   
>         read all var{name} into row;   
>         close sashelp.class; 
> 
>         mattrib class rowname=row   
>                       colname=col   
>                       label="test, label"   
>                       format=5.2;   
>         print class;   
> quit;

***(IML matrix operations: to be continued)***

 [1]: http://blogs.sas.com/iml/index.php
 [2]: http://support.sas.com/publishing/authors/wicklin.html
 [3]: http://en.wikipedia.org/wiki/SQL-92
 [4]: http://blogs.sas.com/iml/index.php?/archives/8-Five-Reasons-to-CLOSE-Your-Data-Sets.html