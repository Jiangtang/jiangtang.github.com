---
author: Jiangtang Hu
title: 'Work With Oracle: A Quick Sheet for SAS Programmers'
excerpt:
layout: post
category:
  - Database
  - SAS
tags:
  - Oracle
  - Oracle Database 10g Express Edition
  - SAS
  - SAS SQL Pass-Through Facility
  - SQL
post_format: [ ]
---
(Note: All the followings are tested on Windows XP environment.)

**0. Install Oracle Database 10g Express Edition**

Fast (and free) to download, easy to deploy and simple to admin–for learning and testing purpose, Oracle Database 10g Express Edition (Oracle Database XE, a mini version of Oracle Database 10*g* Release 2) are strongly recommended:

0.1 Download it at [its homepage][1](206MB);

0.2 Install it following default settings;

0.3 Unlock accounts for HR and SCOTT. In a windows DOS prompt, using the following scripts: 

>     sqlplus sys/*YourSysPassword* as sysdba
> 
>     alter user HR account unlock
> 
>     alter user HR identified by *YourHRPassword*
> 
>     alter user SCOTT account unlock
> 
>     alter user SCOTT identified by TIGER

    Or you can accomplish these tasks within the Oracle web application:

>     [http://localhost:8081/apex][2]

**1. Connect Oracle using SAS libname engine**

> *libname SCOTT oracle user=”SCOTT” password=”TIGER” path=’xe’ ;*

    Note: *xe* is the default path for Oracle Database XE.

**2. Connect Oracle using SQL Procedure Pass-Through Facility**

> *proc sql ;  
> connect to oracle as orcl   
> (user=”SCOTT” password=”TIGER” path=’xe’);*
> 
> * select *   
> from connection to orcl *
> 
> * (*
> 
> * **SELECT …***
> 
> *** ) ;***
> 
> * disconnect from orcl;</p> 
> quit;</em></blockquote> 
> 
> Note: 1) In this approach, Oracle, instead of SAS, processes the SQL statement (i.e., you use the more powerful and flexible Oracle SQL syntax instead of SAS Proc SQL procedure for querying. For more, se*e [SAS Doc][3]*)*.*
> 
> * * 2) Your Oracle SQL codes should be placed in the RED blocks, and end without a semicolon(;):
> 
> > *select *</p> 
> > from emp</em></blockquote> 
> > 
> > 3) Only basic Oracle SQL statements (*select, create table*, . . .)can pass through this facility.
> > 
> > **3. Load SAS datasets to Oracle database**
> > 
> > > proc copy in=sashelp  
> > > out=scott;  
> > > select class;  
> > > run;
> > 
> > **4. Misc: Some differences between Oracle SQL and SAS Proc SQL**
> > 
> > **4.1 Table aliases**
> > 
> > Oracle: *from employees a;*
> > 
> > SAS:* from employees a;* or
> > 
> > > *from employees as a;*
> > 
> > **4.2 Column aliases**
> > 
> > Oracle: don’t use single quotation marks(‘’).
> > 
> > > *select job_id as job, job_id job, job_id as “job” , <strike>job_id as ‘job’</strike>*
> > 
> > SAS:
> > 
> > > *select job_id as job, job_id “job” , job_id ‘job’, <strike>job_id job</strike>*
> > 
> > **4.3 Literal Character Strings**
> > 
> > Oracle: Date and character literal values must be enclosed within single quotation marks(‘’).
> > 
> > SAS: Use both single and double quotation marks.
> > 
> > **4.4 Order the null value**
> > 
> > Oracle: Null values are displayed last for ascending sequences and first for descending sequences.
> > 
> > SAS: Null values are displayed first for ascending sequences and last for descending sequences.
> > 
> > **4.5 Nesting Group Functions**
> > 
> > > *select max(avg(salary))  
> > > from employees  
> > > group by department_id*
> > 
> > SAS log:
> > 
> > > ERROR: Summary functions nested in this way are not supported.
> > 
> > Optional approach for SAS:  
> > > *select max(avg) as max  
> > > from(  
> > > select avg(salary) as avg  
> > > from employees  
> > > group by department_id )*
> > 
> > **4.6 row number(\_n\_)**
> > 
> > Oracle:
> > 
> > > select rownum  
> > > from employees
> > 
> > SAS:
> > 
> > > select monotonic()  
> > > from employees
> > 
> > Note: monotonic() is an undocumented function of SAS, *see<http://www2.sas.com/proceedings/sugi29/040-29.pdf>*

 [1]: http://www.oracle.com/technology/software/products/database/xe/index.html
 [2]: http://localhost:8081/apex "http://localhost:8081/apex"
 [3]: http://support.sas.com/documentation/cdl/en/lrcon/61722/HTML/default/a001044413.htm