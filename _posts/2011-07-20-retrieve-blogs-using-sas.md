---
id: 354
title: Retrieve blogs using SAS
date: 2011-07-20T21:47:46+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/07/20/retrieve-blogs-using-sas/
permalink: /2011/07/20/retrieve-blogs-using-sas/
categories:
  - SAS
tags:
  - Blog
  - IML
  - Rick Wicklin
  - SAS
---
<span style="font-size: small;">Recently I posted a </span><a href="http://www.jiangtanghu.com/blog/2011/07/17/sas-bloggers-in-action1-rick-wicklin-sasiml-and-color-revolution/" target="_blank"><span style="font-size: small;">frequency analysis</span></a> <span style="font-size: small;">on Rick Wicklin’s popular </span><a href="http://blogs.sas.com/iml/" target="_blank"><span style="font-size: small;">SAS/IML blog</span></a><span style="font-size: small;">. Sanjay Matange also produced a nice </span><a href="https://sites.google.com/site/odsgraphics/general/rick-s-blog-history-heatmap" target="_blank"><span style="font-size: small;">heatmap on Rick’s blogging history</span></a> <span style="font-size: small;">using the summary data I published. Here just release the ideas and SAS codes to get data from Rick’s blog dynamically. You may modify the codes slightly to obtain data from all other SAS in-house blogs (</span>[<span style="font-size: small;">http://blogs.sas.com/index.php</span>](http://blogs.sas.com/index.php)<span style="font-size: small;">) since they share the same template. For other blogs, you should research the web pages accordingly to get the best suitable methods and this post can also serve as an example.</span>

# **First step: define the scope**

<span style="font-size: small;">For my purpose, I only need the titles and publish dates of Rick’s posts. It is so called the “metadata” of the blog. I do not need all the post contents. By the way, if all information needed, you can use a blog backup tool, or write codes to retrieve all the pages of </span>[<span style="font-size: small;">http://blogs.sas.com/iml</span>](http://blogs.sas.com/iml) at the maximum depth<span style="font-size: small;">, or simply, you can write to Rick and say: hey Rick, could you please send me all the contents of your blog? And Rick may go to the management console of his own blog, export all the contents to an XML file and get back to you.</span>

# **Second step: analyze the web pages**

<span style="font-size: small;">Browse to the right panel of Rick’s blog, in the ARCHIVES frame, click “<a href="http://blogs.sas.com/iml/index.php?/archive" target="_blank">Older</a>”</span><span style="font-size: small;">:</span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image002" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image002_thumb1.jpg" alt="clip_image002" width="235" height="298" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0026.jpg)

<span style="font-size: small;">And you get </span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image003" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image003_thumb.gif" alt="clip_image003" width="362" height="274" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0035.gif)

<span style="font-size: small;">This page just gives a big picture of Rick’s blog (ARCHIVE section is always a good place to get such metadata, for example, <a href="http://www.jiangtanghu.com/blog/archives/" target="_blank">archives for my blog</a></span><span style="font-size: small;">). But we need more. Click “<a href="http://blogs.sas.com/iml/index.php?/archives/2010/09/summary.html" target="_blank">view topics</a>” for example of September, 2010:</span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image004" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image004_thumb.gif" alt="clip_image004" width="372" height="443" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0045.gif)

<span style="font-size: small;">This page is exactly what we want with titles and dates. Open an editor to write codes immediately to read all the information in this page?—wait. Currently this blog has posts across 11 months and you can expect the increase. You should design a dynamic method to read all the topics pages: Sep 2010, Oct 2010, … and, <span style="font-family: 'Courier New';">today()</span>.</span>

<span style="font-size: small;">Return to the <a href="http://blogs.sas.com/iml/index.php?/archive" target="_blank">archives page</a>. RCM (right click your mouse) and select “View page source” if you use Google Chrome web browser (“View Source” in IE; “View Page Source” in Firefox) and you get all the HTML scripts (<strong>Note: you DO not need any knowledge of HTML to understand this post</strong>). Copy and paste them into a text editor supporting HTML syntax highlighting (such as Notepad++). Search all instances of “view topics” we mentioned before:</span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image006" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image006_thumb2.jpg" alt="clip_image006" width="519" height="312" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0067.jpg)

<span style="font-size: small;">We are lucky. They are 11 instances of “view topics” accompanying with 11 hyperlinks for the currently 11 months’ archives of Rick’s blog. We can read such 11 hyperlinks to a macro array for dynamic retrieval.</span>

<span style="font-size: small;">Then we return to the single <a href="http://blogs.sas.com/iml/index.php?/archives/2010/09/summary.html" target="_blank">topics page</a>, for example of September, 2010</span><span style="font-size: small;">. Review the HTML source file. Search for “posted_by_date” and we get 14 instances which is same as the number of posts in September 2010:</span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image008" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image008_thumb1.jpg" alt="clip_image008" width="518" height="307" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0086.jpg)

<span style="font-size: small;">We should also need to locate all the instances of titles. Search “/iml/index.php?/archives/” and we get 17 responses:</span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image010" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image010_thumb1.jpg" alt="clip_image010" width="517" height="298" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0106.jpg)

<span style="font-size: small;">We see 3 instances at end of the finding results don’t contain any titles. You can check other pages to confirm such pattern. Yes we can use regular expressions to parse the HTML pages to locate more exactly for the titles. But for a quick job and due to the relative simple HTML pages, some basic SAS character functions are enough for our purpose. In the following codes, limited regular expressions are used only to remove HTML tags such as “<a href=”.</span>

<span style="font-size: small;">After such explorative search of HTML scripts, we can get the basic idea where can we find the interested information. Then we begin to coding work.</span>

# **Third step: Coding at last!**

<span style="font-size: small;">For our purpose, we should first read the archive page to get all the topics links to a macro array, then read the all the topics pages dynamically. Finally, we should also add the all the calendar dates with holidays. Some friends may find that they met piece of the following codes before. Yes, such codes just assembled some skills what I learned from Art Carpenter, Richard DeVenezia, Jian Dai and lots of programmers before!</span>

### 3-1: read archive page

> <span style="font-family: 'Courier New';">%let URL=</span>[<span style="font-family: 'Courier New';">http://blogs.sas.com/iml/index.php?/archive;</span>](http://blogs.sas.com/iml/index.php?/archive;)
> 
> <span style="font-family: 'Courier New';">filename archive URL &#8220;&URL&#8221;; </span>
> 
> <span style="font-family: 'Courier New';">data archive;<br /> length text $1024;<br /> infile archive lrecl=1024;<br /> input text $;<br /> text= _infile_;<br /> if index(text, &#8220;>view topics<&#8220;) then output;<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">data  archive1;<br /> set archive;<br /> summary=scan(text,4,'&#8221;&#8216;);<br /> run;</span>

### 3-2: read all topics pages

> <span style="font-family: 'Courier New';">data _null_;<br /> set  archive1 end=eof;<br /> I+1;<br /> II=left(put(I,2.));<br /> call symputx(&#8216;summary&#8217;||II,summary);<br /> if eof then call symputx(&#8216;total&#8217;,II);<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">%macro readit;<br /> %do i=1 %to &total;<br /> filename f&i URL &#8220;&&summary&i&#8221;;    </span>
> 
> <span style="font-family: 'Courier New';">        data f&i;<br /> length text $1024;<br /> infile f&i lrecl=1024;<br /> input text $;<br /> text= _infile_;<br /> if index(text, &#8220;/iml/index.php?/archives/&#8221;) or index(text, &#8220;posted_by_date&#8221;) then output;<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">    <span style="color: #ff0000;">/*remove HTML tags;*/</span><br /> data ff&i;<br /> set f&i;<br /> prx=prxparse(&#8220;s/<.*?>//&#8221;);<br /> call prxchange(prx,99,text);<br /> drop prx; </span>
> 
> <span style="font-family: 'Courier New';">        flag=ifn(mod(_n_,2),1,2);<br /> grpn=&i;<br /> if index(text,&#8221;201&#8243;) and length(text)<10 then delete;<span style="color: #ff0000;">/*be carefull! hard coding;*/<br /> </span>        seq=_n_;<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">     /*transpose data;*/<br /> data fff&i;<br /> set ff&i;<br /> by grpn seq flag; </span>
> 
> <span style="font-family: 'Courier New';">        <span style="color: #ff0000;">retain</span> title;<br /> if first.flag then title=lag(text);<br /> if flag=1 then delete;<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">    %end; </span>
> 
> <span style="font-family: 'Courier New';">%mend readit;<br /> %readit </span>
> 
> <span style="font-family: 'Courier New';">%macro getall;<br /> data Rick;<br /> set %do i=1 %to &total; fff&i %end; ;<br /> seq=seq/2;<br /> drop flag;<br /> run;<br /> %mend getall;<br /> %getall </span>
> 
> <span style="font-family: 'Courier New';">data rick2;<br /> set rick; </span>
> 
> <span style="font-family: 'Courier New';">    datetime=scan(text,2,&#8221;,&#8221;);<br /> year=scan(text,2,&#8221;.&#8221;);<br /> month=scan(scan(text,2,&#8221;,&#8221;),1);<br /> day=scan(scan(text,2,&#8221;,&#8221;),2);<br /> week=scan(text,6);<br /> dt=compress(catx(&#8220;&#8221;,day,substr(month,1,3),year));<br /> worddat=input(dt,date9.);<br /> format worddat  ddmmyy10.;                         </span>
> 
> <span style="font-family: 'Courier New';">    m=scan(put(worddat,ddmmyy10.),2);<br /> my=compress(catx(&#8220;&#8221;,year,m));<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">proc sort ;<br /> by  worddat descending seq ;<br /> run;</span>

<!--more-->

It is also interesting to add additional information for further analysis, such as all calendar dates during Rick’s blogging history and holidays.

### 3-3: get all calendar dates

> <span style="font-family: 'Courier New';">proc sort data=rick2 out=rick3 nodupkey;<br /> by my;<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">data _null_;<br /> set rick3 end=eof;<br /> I+1;<br /> II=left(put(I,2.));<br /> call symputx(&#8216;year&#8217;||II,year);<br /> call symputx(&#8216;month&#8217;||II,m);<br /> if eof then call symputx(&#8216;total&#8217;,II);<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">%macro getCalendar;<br /> %do i=1 %to &total;<br /> data calendar&i;<br /> date1 = mdy (&&month&i,1,&&year&i);<br /> date2 = intnx (&#8216;month&#8217;, date1, 1) &#8211; 1; </span>
> 
> <span style="font-family: 'Courier New';">            do worddat = date1 to date2;<br /> wim = intck (&#8216;week&#8217;, date1, worddat);<br /> dim = worddat-date1+1;<br /> output;<br /> end; </span>
> 
> <span style="font-family: 'Courier New';">            format worddat  ddmmyy10.;<br /> keep   worddat  dim ;<br /> run;<br /> %end;<br /> %mend getCalendar;<br /> %getCalendar; </span>
> 
> <span style="font-family: 'Courier New';">%macro allCalendar;<br /> data Calendar;<br /> set %do i=1 %to &total; calendar&i %end; ;<br /> run;<br /> %mend allCalendar;<br /> %allCalendar</span>

### 3-4: get holidays

<span style="font-size: small;">I have no specific idea about US holidays and just referenced the two pages:</span>

> [<span style="font-size: small;">Recently I posted a </span><a href="http://www.jiangtanghu.com/blog/2011/07/17/sas-bloggers-in-action1-rick-wicklin-sasiml-and-color-revolution/" target="_blank"><span style="font-size: small;">frequency analysis</span></a> <span style="font-size: small;">on Rick Wicklin’s popular </span><a href="http://blogs.sas.com/iml/" target="_blank"><span style="font-size: small;">SAS/IML blog</span></a><span style="font-size: small;">. Sanjay Matange also produced a nice </span><a href="https://sites.google.com/site/odsgraphics/general/rick-s-blog-history-heatmap" target="_blank"><span style="font-size: small;">heatmap on Rick’s blogging history</span></a> <span style="font-size: small;">using the summary data I published. Here just release the ideas and SAS codes to get data from Rick’s blog dynamically. You may modify the codes slightly to obtain data from all other SAS in-house blogs (</span>[<span style="font-size: small;">http://blogs.sas.com/index.php</span>](http://blogs.sas.com/index.php)<span style="font-size: small;">) since they share the same template. For other blogs, you should research the web pages accordingly to get the best suitable methods and this post can also serve as an example.</span>

# **First step: define the scope**

<span style="font-size: small;">For my purpose, I only need the titles and publish dates of Rick’s posts. It is so called the “metadata” of the blog. I do not need all the post contents. By the way, if all information needed, you can use a blog backup tool, or write codes to retrieve all the pages of </span>[<span style="font-size: small;">http://blogs.sas.com/iml</span>](http://blogs.sas.com/iml) at the maximum depth<span style="font-size: small;">, or simply, you can write to Rick and say: hey Rick, could you please send me all the contents of your blog? And Rick may go to the management console of his own blog, export all the contents to an XML file and get back to you.</span>

# **Second step: analyze the web pages**

<span style="font-size: small;">Browse to the right panel of Rick’s blog, in the ARCHIVES frame, click “<a href="http://blogs.sas.com/iml/index.php?/archive" target="_blank">Older</a>”</span><span style="font-size: small;">:</span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image002" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image002_thumb1.jpg" alt="clip_image002" width="235" height="298" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0026.jpg)

<span style="font-size: small;">And you get </span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image003" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image003_thumb.gif" alt="clip_image003" width="362" height="274" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0035.gif)

<span style="font-size: small;">This page just gives a big picture of Rick’s blog (ARCHIVE section is always a good place to get such metadata, for example, <a href="http://www.jiangtanghu.com/blog/archives/" target="_blank">archives for my blog</a></span><span style="font-size: small;">). But we need more. Click “<a href="http://blogs.sas.com/iml/index.php?/archives/2010/09/summary.html" target="_blank">view topics</a>” for example of September, 2010:</span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image004" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image004_thumb.gif" alt="clip_image004" width="372" height="443" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0045.gif)

<span style="font-size: small;">This page is exactly what we want with titles and dates. Open an editor to write codes immediately to read all the information in this page?—wait. Currently this blog has posts across 11 months and you can expect the increase. You should design a dynamic method to read all the topics pages: Sep 2010, Oct 2010, … and, <span style="font-family: 'Courier New';">today()</span>.</span>

<span style="font-size: small;">Return to the <a href="http://blogs.sas.com/iml/index.php?/archive" target="_blank">archives page</a>. RCM (right click your mouse) and select “View page source” if you use Google Chrome web browser (“View Source” in IE; “View Page Source” in Firefox) and you get all the HTML scripts (<strong>Note: you DO not need any knowledge of HTML to understand this post</strong>). Copy and paste them into a text editor supporting HTML syntax highlighting (such as Notepad++). Search all instances of “view topics” we mentioned before:</span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image006" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image006_thumb2.jpg" alt="clip_image006" width="519" height="312" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0067.jpg)

<span style="font-size: small;">We are lucky. They are 11 instances of “view topics” accompanying with 11 hyperlinks for the currently 11 months’ archives of Rick’s blog. We can read such 11 hyperlinks to a macro array for dynamic retrieval.</span>

<span style="font-size: small;">Then we return to the single <a href="http://blogs.sas.com/iml/index.php?/archives/2010/09/summary.html" target="_blank">topics page</a>, for example of September, 2010</span><span style="font-size: small;">. Review the HTML source file. Search for “posted_by_date” and we get 14 instances which is same as the number of posts in September 2010:</span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image008" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image008_thumb1.jpg" alt="clip_image008" width="518" height="307" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0086.jpg)

<span style="font-size: small;">We should also need to locate all the instances of titles. Search “/iml/index.php?/archives/” and we get 17 responses:</span>

[<img style="display: block; float: none; margin-left: auto; margin-right: auto; border-width: 0px;" title="clip_image010" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image010_thumb1.jpg" alt="clip_image010" width="517" height="298" border="0" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/07/clip_image0106.jpg)

<span style="font-size: small;">We see 3 instances at end of the finding results don’t contain any titles. You can check other pages to confirm such pattern. Yes we can use regular expressions to parse the HTML pages to locate more exactly for the titles. But for a quick job and due to the relative simple HTML pages, some basic SAS character functions are enough for our purpose. In the following codes, limited regular expressions are used only to remove HTML tags such as “<a href=”.</span>

<span style="font-size: small;">After such explorative search of HTML scripts, we can get the basic idea where can we find the interested information. Then we begin to coding work.</span>

# **Third step: Coding at last!**

<span style="font-size: small;">For our purpose, we should first read the archive page to get all the topics links to a macro array, then read the all the topics pages dynamically. Finally, we should also add the all the calendar dates with holidays. Some friends may find that they met piece of the following codes before. Yes, such codes just assembled some skills what I learned from Art Carpenter, Richard DeVenezia, Jian Dai and lots of programmers before!</span>

### 3-1: read archive page

> <span style="font-family: 'Courier New';">%let URL=</span>[<span style="font-family: 'Courier New';">http://blogs.sas.com/iml/index.php?/archive;</span>](http://blogs.sas.com/iml/index.php?/archive;)
> 
> <span style="font-family: 'Courier New';">filename archive URL &#8220;&URL&#8221;; </span>
> 
> <span style="font-family: 'Courier New';">data archive;<br /> length text $1024;<br /> infile archive lrecl=1024;<br /> input text $;<br /> text= _infile_;<br /> if index(text, &#8220;>view topics<&#8220;) then output;<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">data  archive1;<br /> set archive;<br /> summary=scan(text,4,'&#8221;&#8216;);<br /> run;</span>

### 3-2: read all topics pages

> <span style="font-family: 'Courier New';">data _null_;<br /> set  archive1 end=eof;<br /> I+1;<br /> II=left(put(I,2.));<br /> call symputx(&#8216;summary&#8217;||II,summary);<br /> if eof then call symputx(&#8216;total&#8217;,II);<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">%macro readit;<br /> %do i=1 %to &total;<br /> filename f&i URL &#8220;&&summary&i&#8221;;    </span>
> 
> <span style="font-family: 'Courier New';">        data f&i;<br /> length text $1024;<br /> infile f&i lrecl=1024;<br /> input text $;<br /> text= _infile_;<br /> if index(text, &#8220;/iml/index.php?/archives/&#8221;) or index(text, &#8220;posted_by_date&#8221;) then output;<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">    <span style="color: #ff0000;">/*remove HTML tags;*/</span><br /> data ff&i;<br /> set f&i;<br /> prx=prxparse(&#8220;s/<.*?>//&#8221;);<br /> call prxchange(prx,99,text);<br /> drop prx; </span>
> 
> <span style="font-family: 'Courier New';">        flag=ifn(mod(_n_,2),1,2);<br /> grpn=&i;<br /> if index(text,&#8221;201&#8243;) and length(text)<10 then delete;<span style="color: #ff0000;">/*be carefull! hard coding;*/<br /> </span>        seq=_n_;<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">     /*transpose data;*/<br /> data fff&i;<br /> set ff&i;<br /> by grpn seq flag; </span>
> 
> <span style="font-family: 'Courier New';">        <span style="color: #ff0000;">retain</span> title;<br /> if first.flag then title=lag(text);<br /> if flag=1 then delete;<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">    %end; </span>
> 
> <span style="font-family: 'Courier New';">%mend readit;<br /> %readit </span>
> 
> <span style="font-family: 'Courier New';">%macro getall;<br /> data Rick;<br /> set %do i=1 %to &total; fff&i %end; ;<br /> seq=seq/2;<br /> drop flag;<br /> run;<br /> %mend getall;<br /> %getall </span>
> 
> <span style="font-family: 'Courier New';">data rick2;<br /> set rick; </span>
> 
> <span style="font-family: 'Courier New';">    datetime=scan(text,2,&#8221;,&#8221;);<br /> year=scan(text,2,&#8221;.&#8221;);<br /> month=scan(scan(text,2,&#8221;,&#8221;),1);<br /> day=scan(scan(text,2,&#8221;,&#8221;),2);<br /> week=scan(text,6);<br /> dt=compress(catx(&#8220;&#8221;,day,substr(month,1,3),year));<br /> worddat=input(dt,date9.);<br /> format worddat  ddmmyy10.;                         </span>
> 
> <span style="font-family: 'Courier New';">    m=scan(put(worddat,ddmmyy10.),2);<br /> my=compress(catx(&#8220;&#8221;,year,m));<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">proc sort ;<br /> by  worddat descending seq ;<br /> run;</span>

<!--more-->

It is also interesting to add additional information for further analysis, such as all calendar dates during Rick’s blogging history and holidays.

### 3-3: get all calendar dates

> <span style="font-family: 'Courier New';">proc sort data=rick2 out=rick3 nodupkey;<br /> by my;<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">data _null_;<br /> set rick3 end=eof;<br /> I+1;<br /> II=left(put(I,2.));<br /> call symputx(&#8216;year&#8217;||II,year);<br /> call symputx(&#8216;month&#8217;||II,m);<br /> if eof then call symputx(&#8216;total&#8217;,II);<br /> run; </span>
> 
> <span style="font-family: 'Courier New';">%macro getCalendar;<br /> %do i=1 %to &total;<br /> data calendar&i;<br /> date1 = mdy (&&month&i,1,&&year&i);<br /> date2 = intnx (&#8216;month&#8217;, date1, 1) &#8211; 1; </span>
> 
> <span style="font-family: 'Courier New';">            do worddat = date1 to date2;<br /> wim = intck (&#8216;week&#8217;, date1, worddat);<br /> dim = worddat-date1+1;<br /> output;<br /> end; </span>
> 
> <span style="font-family: 'Courier New';">            format worddat  ddmmyy10.;<br /> keep   worddat  dim ;<br /> run;<br /> %end;<br /> %mend getCalendar;<br /> %getCalendar; </span>
> 
> <span style="font-family: 'Courier New';">%macro allCalendar;<br /> data Calendar;<br /> set %do i=1 %to &total; calendar&i %end; ;<br /> run;<br /> %mend allCalendar;<br /> %allCalendar</span>

### 3-4: get holidays

<span style="font-size: small;">I have no specific idea about US holidays and just referenced the two pages:</span>

>](http://support.sas.com/kb/24/655.html  "http://support.sas.com/kb/24/655.html  ") 
> 
> [http://www.opm.gov/Operating\_Status\_Schedules/fedhol/2011.asp](http://www.opm.gov/Operating_Status_Schedules/fedhol/2011.asp "http://www.opm.gov/Operating_Status_Schedules/fedhol/2011.asp")

<span style="font-size: small;">Also, the holidays and observances should manully modified according to personal working schedule. So this section serves only for demonstration.</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">filename hld url &#8220;</span>[<span style="font-family: 'Courier New'; font-size: xx-small;">http://jiangtanghu.com/docs/en/US_holiday.sas&#8221;;</span>](http://jiangtanghu.com/docs/en/US_holiday.sas";)
> 
> <span style="font-family: 'Courier New';">%include hld; </span>
> 
> <span style="font-family: 'Courier New';">%US_holiday(2010)<br /> %US_holiday(2011) </span>
> 
> <span style="font-family: 'Courier New';">data holiday;<br /> set holiday2010 holiday2011;<br /> run;</span>
> 
> <span style="font-family: 'Courier New';">proc sort ;<br /> by  worddat;<br /> run;</span>

### 3-5: put all together

> <span style="font-family: 'Courier New';">data rick_all;<br /> merge rick2 calendar holiday;<br /> by worddat;<br /> </span><span style="font-family: 'Courier New';">if worddat <&#8217;03Sep2010&#8217;d then delete;<br /> <span style="color: #ff0000;">if worddat >&#8217;15Jul2011&#8217;d then delete;</span><br /> drop today;<br /> run;</span>
> 
> &nbsp;

&nbsp;

&nbsp;

&nbsp;

&nbsp;

A pooled version (beta) also available at

> <http://jiangtanghu.com/docs/en/SAS_Blogs.sas>