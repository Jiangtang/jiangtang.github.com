---
id: 69
title: 'Work With Oracle: A Quick Sheet for SAS Programmers'
date: 2009-12-04T09:33:00+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2009/12/04/work-with-oracle-a-quick-sheet-for-sas-programmers-2/
permalink: /2009/12/04/work-with-oracle-a-quick-sheet-for-sas-programmers-2/
blogger_blog:
  - jiangtanghu.blogspot.com
  - jiangtanghu.blogspot.com
blogger_author:
  - John(Jiangtang) Huhttp://www.blogger.com/profile/04383471478195804254JiangtangHu@gmail.com
  - John(Jiangtang) Huhttp://www.blogger.com/profile/04383471478195804254JiangtangHu@gmail.com
blogger_permalink:
  - /2009/12/work-with-oracle-quick-sheet-for-sas.html
  - /2009/12/work-with-oracle-quick-sheet-for-sas.html
categories:
  - Database
  - SAS
tags:
  - Oracle
  - Oracle Database 10g Express Edition
  - SAS
  - SAS SQL Pass-Through Facility
  - SQL
---
(Note: All the followings are tested on Windows XP environment.)

**0. Install Oracle Database 10g Express Edition**

Fast (and free) to download, easy to deploy and simple to admin&#8211;for learning and testing purpose, Oracle Database 10g Express Edition (Oracle Database XE, a mini version of Oracle Database 10_g_ Release 2) are strongly recommended:

0.1 Download it at [its homepage](http://www.oracle.com/technology/software/products/database/xe/index.html)(206MB);

0.2 Install it following default settings;

0.3 Unlock accounts for HR and SCOTT. In a windows DOS prompt, using the following scripts: 

> <pre>sqlplus sys/<span style="color:#ff0000;"><em>YourSysPassword</em> </span>as sysdba</pre>
> 
> <pre>alter user HR account unlock</pre>
> 
> <pre>alter user HR identified by <em><span style="color:#ff0000;">YourHRPassword</span></em></pre>
> 
> <pre>alter user SCOTT account unlock</pre>
> 
> <pre>alter user SCOTT identified by TIGER</pre>

<pre>Or you can accomplish these tasks within the Oracle web application:</pre>

> <pre><a title="http://localhost:8081/apex" href="http://localhost:8081/apex">http://localhost:8081/apex</a></pre>

**1. Connect Oracle using SAS libname engine**

> _libname SCOTT oracle user=&#8221;SCOTT&#8221; password=&#8221;TIGER&#8221; path=&#8217;xe&#8217; ;_

<pre>Note: <em>xe</em> is the default path for Oracle Database XE.</pre>

**2. Connect Oracle using SQL Procedure Pass-Through Facility**

> _proc sql ;      
> connect to oracle as orcl       
> (user=&#8221;SCOTT&#8221; password=&#8221;TIGER&#8221; path=&#8217;xe&#8217;);_
> 
>     _select *       
> from connection to orcl_ 
> 
> <span style="color:#ff0000;"><em> (</em></span>
> 
> <span style="color:#ff0000;"><em> <strong>SELECT …</strong></em></span>
> 
> <span style="color:#ff0000;"><em><strong><span class="Apple-style-span" style="font-weight: normal; "> ) ;</span></strong></em></span>
> 
>     _disconnect from orcl;</p> 
> 
> quit;</em></blockquote> 
> 
> Note: 1) In this approach, Oracle, instead of SAS, processes the SQL statement (i.e., you use the more powerful and flexible Oracle SQL syntax instead of SAS Proc SQL procedure for querying. For more, se_e [SAS Doc](http://support.sas.com/documentation/cdl/en/lrcon/61722/HTML/default/a001044413.htm)_)_._
> 
>           __ 2) Your Oracle SQL codes should be placed in the <span style="color:#ff0000;">RED</span> blocks, and end without a semicolon(;):
> 
> > _select *</p> 
> > 
> > from emp</em></blockquote> 
> > 
> > 3) Only basic Oracle SQL statements (_select, create table_, . . .)can pass through this facility.
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
> > Oracle: _from employees a;_
> > 
> > SAS: _from employees a;_ or
> > 
> > > _from employees <span style="color:#ff0000;">as</span> a;_
> > 
> > **4.2 Column aliases**
> > 
> > Oracle: don’t use single quotation marks(‘’).
> > 
> > > _select job_id <span style="color:#ff0000;">as job</span>, job_id <span style="color:#ff0000;">job</span>, job_id <span style="color:#ff0000;">as &#8220;job&#8221; <span style="color:#000000;">,</span> <strike>job_id <span style="color:#ff0000;">as ‘job’</span></strike></span>_
> > 
> > SAS:
> > 
> > > _select job_id <span style="color:#ff0000;">as job</span>, job_id <span style="color:#ff0000;">&#8220;job&#8221;</span> , job_id <span style="color:#ff0000;">&#8216;job&#8217;</span>, <strike><span style="color:#ff0000;">job_id job</span></strike>_
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
> > > _select max(avg(salary))  
> > > from employees  
> > > group by department_id_
> > 
> > SAS log:
> > 
> > > ERROR: Summary functions nested in this way are not supported.
> > 
> > Optional approach for SAS:
  
> > 
> > 
> > > _select max(avg) as max  
> > > from(      
> > > select avg(salary) as avg      
> > > from employees      
> > > group by department_id )_
> > 
> > **4.6 row number(\_n\_)**
> > 
> > Oracle:
> > 
> > > select <span style="color:#ff0000;">rownum</span>  
> > > from employees
> > 
> > SAS:
> > 
> > > select <span style="color:#ff0000;">monotonic()</span>  
> > > from employees
> > 
> > Note: <span style="color:#ff0000;">monotonic()</span> is an undocumented function of SAS, _see<span class="Apple-style-span" style="font-style: normal; "><a href="http://www2.sas.com/proceedings/sugi29/040-29.pdf">http://www2.sas.com/proceedings/sugi29/040-29.pdf</a></span>_