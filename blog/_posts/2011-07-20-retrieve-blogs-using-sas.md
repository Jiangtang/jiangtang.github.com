---
author: Jiangtang Hu
title: Retrieve blogs using SAS
excerpt:
layout: post
category:
  - SAS
tags:
  - Blog
  - IML
  - Rick Wicklin
  - SAS
post_format: [ ]
---
Recently I posted a [frequency analysis][1] on Rick Wicklin’s popular [SAS/IML blog][2]. Sanjay Matange also produced a nice [heatmap on Rick’s blogging history][3] using the summary data I published. Here just release the ideas and SAS codes to get data from Rick’s blog dynamically. You may modify the codes slightly to obtain data from all other SAS in-house blogs (<http://blogs.sas.com/index.php>) since they share the same template. For other blogs, you should research the web pages accordingly to get the best suitable methods and this post can also serve as an example.

# **First step: define the scope**

For my purpose, I only need the titles and publish dates of Rick’s posts. It is so called the “metadata” of the blog. I do not need all the post contents. By the way, if all information needed, you can use a blog backup tool, or write codes to retrieve all the pages of <http://blogs.sas.com/iml> at the maximum depth, or simply, you can write to Rick and say: hey Rick, could you please send me all the contents of your blog? And Rick may go to the management console of his own blog, export all the contents to an XML file and get back to you.

# **Second step: analyze the web pages**

Browse to the right panel of Rick’s blog, in the ARCHIVES frame, click “[Older][4]”:

[][5][![clip_image002][7]][7]</a></a>

And you get 

[][7][![clip_image003][9]][9]</a></a>

This page just gives a big picture of Rick’s blog (ARCHIVE section is always a good place to get such metadata, for example, [archives for my blog][9]). But we need more. Click “[view topics][10]” for example of September, 2010:

[][11][![clip_image004][13]][13]</a></a>

This page is exactly what we want with titles and dates. Open an editor to write codes immediately to read all the information in this page?—wait. Currently this blog has posts across 11 months and you can expect the increase. You should design a dynamic method to read all the topics pages: Sep 2010, Oct 2010, … and, today().

Return to the [archives page][4]. RCM (right click your mouse) and select “View page source” if you use Google Chrome web browser (“View Source” in IE; “View Page Source” in Firefox) and you get all the HTML scripts (**Note: you DO not need any knowledge of HTML to understand this post**). Copy and paste them into a text editor supporting HTML syntax highlighting (such as Notepad++). Search all instances of “view topics” we mentioned before:

[][13][![clip_image006][15]][15]</a></a>

We are lucky. They are 11 instances of “view topics” accompanying with 11 hyperlinks for the currently 11 months’ archives of Rick’s blog. We can read such 11 hyperlinks to a macro array for dynamic retrieval.

Then we return to the single [topics page][10], for example of September, 2010. Review the HTML source file. Search for “posted\_by\_date” and we get 14 instances which is same as the number of posts in September 2010:

[][15][![clip_image008][17]][17]</a></a>

We should also need to locate all the instances of titles. Search “/iml/index.php?/archives/” and we get 17 responses:

[][17][![clip_image010][19]][19]</a></a>

We see 3 instances at end of the finding results don’t contain any titles. You can check other pages to confirm such pattern. Yes we can use regular expressions to parse the HTML pages to locate more exactly for the titles. But for a quick job and due to the relative simple HTML pages, some basic SAS character functions are enough for our purpose. In the following codes, limited regular expressions are used only to remove HTML tags such as “<a href=”.

After such explorative search of HTML scripts, we can get the basic idea where can we find the interested information. Then we begin to coding work.

# **Third step: Coding at last!**

For our purpose, we should first read the archive page to get all the topics links to a macro array, then read the all the topics pages dynamically. Finally, we should also add the all the calendar dates with holidays. Some friends may find that they met piece of the following codes before. Yes, such codes just assembled some skills what I learned from Art Carpenter, Richard DeVenezia, Jian Dai and lots of programmers before!

### 3-1: read archive page

> %let URL=<http://blogs.sas.com/iml/index.php?/archive;>
> 
> filename archive URL "&URL"; 
> 
> data archive;   
>     length text $1024;   
>     infile archive lrecl=1024;   
>     input text $;   
>     text= \_infile\_;   
>     if index(text, ">view topics<") then output;   
> run; 
> 
> data  archive1;   
>     set archive;   
>     summary=scan(text,4,’"’);   
> run;

### 3-2: read all topics pages

> data \_null\_;   
>     set  archive1 end=eof;   
>     I+1;   
>     II=left(put(I,2.));   
>     call symputx(‘summary’||II,summary);   
>     if eof then call symputx(‘total’,II);   
> run; 
> 
> %macro readit;   
>     %do i=1 %to &total;   
>         filename f&i URL "&&summary&i";    
> 
>         data f&i;   
>             length text $1024;   
>             infile f&i lrecl=1024;   
>             input text $;   
>             text= \_infile\_;   
>             if index(text, "/iml/index.php?/archives/") or index(text, "posted\_by\_date") then output;   
>         run; 
> 
>     /*remove HTML tags;*/   
>     data ff&i;   
>         set f&i;    
>         prx=prxparse("s/<.*?>//");   
>           call prxchange(prx,99,text);   
>         drop prx; 
> 
>         flag=ifn(mod(\_n\_,2),1,2);   
>         grpn=&i;   
>         if index(text,"201") and length(text)<10 then delete;/*be carefull! hard coding;*/   
>         seq=\_n\_;   
>      run; 
> 
>      /*transpose data;*/   
>      data fff&i;   
>          set ff&i;   
>         by grpn seq flag; 
> 
>         retain title;   
>         if first.flag then title=lag(text);   
>         if flag=1 then delete;   
>      run; 
> 
>     %end; 
> 
> %mend readit;   
> %readit 
> 
> %macro getall;   
>     data Rick;   
>         set %do i=1 %to &total; fff&i %end; ;   
>         seq=seq/2;      
>         drop flag;   
>     run;      
> %mend getall;   
> %getall 
> 
> data rick2;   
>     set rick; 
> 
>     datetime=scan(text,2,",");        
>     year=scan(text,2,".");          
>     month=scan(scan(text,2,","),1);   
>     day=scan(scan(text,2,","),2);        
>     week=scan(text,6);               
>     dt=compress(catx("",day,substr(month,1,3),year));     
>     worddat=input(dt,date9.);                           
>     format worddat  ddmmyy10.;                         
> 
>     m=scan(put(worddat,ddmmyy10.),2);                
>     my=compress(catx("",year,m));                        
> run; 
> 
> proc sort ;   
>     by  worddat descending seq ;   
> run;

It is also interesting to add additional information for further analysis, such as all calendar dates during Rick’s blogging history and holidays.

### 3-3: get all calendar dates

> proc sort data=rick2 out=rick3 nodupkey;   
>     by my;   
> run; 
> 
> data \_null\_;   
>     set rick3 end=eof;   
>     I+1;   
>     II=left(put(I,2.));   
>     call symputx(‘year’||II,year);   
>     call symputx(‘month’||II,m);   
>     if eof then call symputx(‘total’,II);   
> run; 
> 
> %macro getCalendar;   
>     %do i=1 %to &total;   
>         data calendar&i;   
>             date1 = mdy (&&month&i,1,&&year&i);   
>             date2 = intnx (‘month’, date1, 1) – 1; 
> 
>             do worddat = date1 to date2;   
>                   wim = intck (‘week’, date1, worddat);   
>                   dim = worddat-date1+1;                  
>                   output;   
>             end; 
> 
>             format worddat  ddmmyy10.;              
>             keep   worddat  dim ;   
>       run;   
>     %end;   
> %mend getCalendar;   
> %getCalendar; 
> 
> %macro allCalendar;   
>     data Calendar;   
>         set %do i=1 %to &total; calendar&i %end; ;      
>     run;      
> %mend allCalendar;   
> %allCalendar

### 3-4: get holidays

I have no specific idea about US holidays and just referenced the two pages:

> [http://support.sas.com/kb/24/655.html  ][19]
> 
> [http://www.opm.gov/Operating\_Status\_Schedules/fedhol/2011.asp][20]

Also, the holidays and observances should manully modified according to personal working schedule. So this section serves only for demonstration.

> filename hld url "<http://jiangtanghu.com/docs/en/US_holiday.sas";>
> 
> %include hld; 
> 
> %US_holiday(2010)   
> %US_holiday(2011) 
> 
> data holiday;   
>     set holiday2010 holiday2011;   
> run;
> 
> proc sort ;   
>     by  worddat;   
> run;

### 3-5: put all together

> data rick_all;   
>     merge rick2 calendar holiday;   
>     by worddat;    
>     if worddat <’03Sep2010′d then delete;       
>     if worddat >’15Jul2011′d then delete;   
>     drop today;   
> run;
> 
> 









A pooled version (beta) also available at 

> <http://jiangtanghu.com/docs/en/SAS_Blogs.sas>

 [1]: http://www.jiangtanghu.com/blog/2011/07/17/sas-bloggers-in-action1-rick-wicklin-sasiml-and-color-revolution/
 [2]: http://blogs.sas.com/iml/
 [3]: https://sites.google.com/site/smatange/ods-graphics/rick-s-blog-history-heatmap
 [4]: http://blogs.sas.com/iml/index.php?/archive
 [5]: http://dl.dropbox.com/u/69732603/clip_image0025.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image0026.jpg
 [7]: http://dl.dropbox.com/u/69732603/clip_image0034.gif
 []: http://dl.dropbox.com/u/69732603/clip_image0035.gif
 [9]: http://www.jiangtanghu.com/blog/archives/
 [10]: http://blogs.sas.com/iml/index.php?/archives/2010/09/summary.html
 [11]: http://dl.dropbox.com/u/69732603/clip_image0044.gif
 []: http://dl.dropbox.com/u/69732603/clip_image0045.gif
 [13]: http://dl.dropbox.com/u/69732603/clip_image0066.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image0067.jpg
 [15]: http://dl.dropbox.com/u/69732603/clip_image0085.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image0086.jpg
 [17]: http://dl.dropbox.com/u/69732603/clip_image0105.jpg
 []: http://dl.dropbox.com/u/69732603/clip_image0106.jpg
 [19]: http://support.sas.com/kb/24/655.html  "http://support.sas.com/kb/24/655.html  "
 [20]: http://www.opm.gov/Operating_Status_Schedules/fedhol/2011.asp "http://www.opm.gov/Operating_Status_Schedules/fedhol/2011.asp"