---
id: 137
title: 'Play Matrix within SAS(1): basic files processing'
date: 2010-10-29T21:02:31+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2010/10/29/sas-iml-basic/
permalink: /2010/10/29/sas-iml-basic/
categories:
  - SAS
tags:
  - IML
  - Matrix
  - SAS
---
Recently I read Rick Wicklin’s [IML blog](http://blogs.sas.com/iml/index.php) with great interests(and anticipation for his fore-coming IML book,&#160; _[Statistical Programming with SAS/IML Software](http://support.sas.com/publishing/authors/wicklin.html)_). SAS programmers have the following programming tools to facilitate their daily work:

  * SAS data step: the basic SAS; a generation IV programming language, similar with other procedural languages such as C. 
  * SAS Proc SQL: SAS’s implementation of standard SQL([SQL-92](http://en.wikipedia.org/wiki/SQL-92)). 
  * SAS IML(Interactive Matrix Language): SAS’s matrix manipulation language(like R and Matlab).&#160; SAS IML Studio also supply IMLPlus programming language(IML+), an enhanced version of IML. 
  * SAS SCL(SAS Component Language): build in SAS/AF software, an object oriented programming(OOP) language for applications development. 

I am a heavy user of data steps and SQL and want to invest some bit on matrix manipulation. Although other wonderful languages available(such as R and Matlab), I found IML is a good choice for SAS programmers like me. It is well integrated within SAS system, and very important, almost all of the SAS Base functions and call routines are also supported by IML. Here some notes of IML 101(codes are self explanatory from a SAS Base point of view):

# **1. IML style of ‘hello world’** 

> <font face="Courier New"><font color="#ff0000">proc iml</font>; <br />&#160;&#160;&#160; text="Hello World!"; <br />&#160;&#160;&#160; <font color="#ff0000">print</font> "IML saying" text; <br /><font color="#ff0000">quit</font>;</font>

and you got in output window:

> IML saying Hello World!

Like Proc SQL, IML begins with “<font face="Courier New"><font color="#ff0000">proc iml</font></font>” , end with ”<font color="#ff0000">quit</font>”, and every statements end with a semicolon. The key word “<font color="#ff0000">print</font>” (an IML statement), just like “put” statement in data steps.

An enhanced version of Hello World: 

> <font face="Courier New"><font color="#ff0000">options </font>nocenter nodate nonumber; </font>
> 
> <font face="Courier New">proc iml; <br />&#160;&#160;&#160; <font color="#ff0000">reset</font> printall; </font>
> 
> <font face="Courier New">&#160;&#160;&#160; text="Hello World!"; <br />&#160;&#160;&#160; print "in &sysdate. IML saying" text; <br />quit;</font>

Some SAS global options added(“<font face="Courier New">nocenter nodate nonumber</font>”). The IML statement “<font color="#ff0000">reset</font>", works like “<font face="Courier New"><font color="#ff0000">options</font></font>” statement to set some processing options within the IML(and you can guess the meaning of the options “printall”, just print all. . . it is your turn to check the output window).

A SAS system macro variable “&sysdate” is presented to encourage you to add any programming elements in SAS Base to IML. 

# **2. How to create a matrix manually**

Actually, we have already create a matrix named “text” in the previous hello-world codes. It is a character <font color="#ff0000">scalar</font>(matrix with only one element). If we want to avoid the SAS data steps’ style of assignment,&#160; we can use <font color="#ff0000"><em>{}</em></font> to enclose matrix elements:

> a={“a”};&#160; /\*a \_char\_ scalar \*/   
> b={1};&#160;&#160;&#160;&#160; /\*a \_num\_ scalar\*/

and a 2*3 matrix:

> c={1 2 3<font color="#ff0000">, <br /></font>&#160;&#160;&#160;&#160;&#160; 2 3 4}; /\*2 rows, 3 cols\*/

Commas(<font color="#ff0000">,</font>) are used to separate rows.

# 3. How to create a matrix by functions

Some matrix reshaping functions:

> <font face="Courier New">a=<font color="#ff0000">I</font>(3);&#160;&#160;&#160;&#160; /*creates a 3*3 identity matrix*/ <br />b=<font color="#ff0000">J</font>(2,3,5); /*creates a 2*3 matrix of identical values*/ <br />e=<font color="#ff0000">do</font>(1,9,2); /*produces series, from 1 to 9, by increment 2*/ <br />c=<font color="#ff0000">block</font>(a,b);/*forms a block-diagonal matrice*/ <br />d=<font color="#ff0000">diag</font>(a);&#160;&#160; /*creates a diagonal matrix*/ <br />m=<font color="#ff0000">repeat</font>(a,4,3); /*create a (3*4)*(3*3) matrix by repeating*/ <br />n=<font color="#ff0000">T</font>(b);&#160;&#160; /*transpose*/</font>

# 4. How to create a matrix by reading a SAS data set

> <font face="Courier New">proc iml; <br />&#160;&#160;&#160; <font color="#ff0000">use</font> sashelp.class; <br />&#160;&#160;&#160; <font color="#ff0000">read</font> all var <font color="#ff0000">_char_</font>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <font color="#ff0000">into</font> class_char; <br />&#160;&#160;&#160; read all var <font color="#ff0000">_num_</font>&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; into class_num; <br />&#160;&#160;&#160; read all var <font color="#ff0000">{"Age" "Height" "Weight"}</font> into class_num2; <br />&#160;&#160;&#160; <font color="#ff0000">close</font> sashelp.class; </font>
> 
> <font face="Courier New">&#160;&#160;&#160; print class_char class_num class_num2; <br />quit;</font>

Note that it is a good habit to close the data file after reading or using it(_see_ Rick Wicklin’s _[Five Reasons to CLOSE Your Data Sets](http://blogs.sas.com/iml/index.php?/archives/8-Five-Reasons-to-CLOSE-Your-Data-Sets.html)_).

# 5. How to output a matrix to SAS dataset

> <font face="Courier New">proc iml; <br />&#160;&#160;&#160; use sashelp.class; <br />&#160;&#160;&#160; read all var _num_ into class_num; <br />&#160;&#160;&#160; close sashelp.class; </font>
> 
> <font face="Courier New">&#160;&#160;&#160; <font color="#ff0000">create</font> work.class_num <font color="#ff0000">from</font> class_num; <br />&#160;&#160;&#160; <font color="#ff0000">append</font> <font color="#ff0000">from</font> class_num; <br />&#160;&#160;&#160; <font color="#ff0000">show datasets</font>; <br />quit;</font>

# &#160;

# 6. How to format a matrix

/\*version I: use matrix options\*/

> <font face="Courier New">proc iml; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; use sashelp.class; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; col={"Age" "Height" "Weight"}; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; read all var col into class; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; read all var{name} into row; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; close sashelp.class; </font>
> 
> <font face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; print class[<font color="#ff0000">rowname</font>=row <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <font color="#ff0000">colname</font>=col <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <font color="#ff0000">format</font>=5.2 <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <font color="#ff0000">label</font>="test, label"]; <br />quit;</font> 

/\*version II: use mattib statement\*/

> <font face="Courier New">proc iml; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; use sashelp.class; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; col={"Age" "Height" "Weight"}; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; read all var col into class; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; read all var{name} into row; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; close sashelp.class; </font>
> 
> <font face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; <font color="#ff0000">mattrib</font> class rowname=row <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; colname=col <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; label="test, label" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; format=5.2; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; print class; <br />quit;</font> 

/\*version III: avoid hardcoding—use IML function and operations\*/

> <font face="Courier New">proc iml; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; use sashelp.class; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; <font color="#ff0000">col=T(contents(sashelp,class)[3:5]);</font> <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; read all var col into class; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; read all var{name} into row; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; close sashelp.class; </font>
> 
> <font face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; mattrib class rowname=row <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; colname=col <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; label="test, label" <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; format=5.2; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; print class; <br />quit;</font>

<font face="Courier New"><em><strong>(IML matrix operations: to be continued)</strong></em></font>