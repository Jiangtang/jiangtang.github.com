---
id: 1141
title: LearningR!
date: 2013-02-08T23:37:49+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1141
permalink: /2013/02/08/learningr/
categories:
  - Computer
  - R
  - SAS
  - statistics
tags:
  - Coursera
  - MOOC
  - plyr
  - R
  - RStudio
  - SAS
  - SQL
  - sqldf
---
[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="Computing_for_data_analysis_Coursera" border="0" alt="Computing_for_data_analysis_Coursera" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/Computing_for_data_analysis_Coursera_thumb.png" width="475" height="422" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/02/Computing_for_data_analysis_Coursera.png)

<font size="1">I spent almost all of my blogging time last month to follow an online course in </font>[<font size="1">Coursera</font>](https://www.coursera.org)<font size="1">, <em><a href="https://www.coursera.org/course/compdata">Computing for Data Analysis</a></em> (with R) by Dr. </font>[<font size="1">Roger&#160; Peng</font>](http://simplystatistics.org/) <font size="1">of Johns Hopkins, Biostatistics Department. I already checked out bunch of Coursera courses just to take a look at what else </font>[<font size="1">MOOC</font>](http://en.wikipedia.org/wiki/Massive_open_online_course) <font size="1">look like, this R course was the first and only one I took seriously: I reviewed all slides (although didn’t watch the videos since I didn’t have enough time) and most important, finished all programming assignments(and got full score!).</font>

<font size="1">Not a frequent R user, I used some R packages for learning purpose (mostly in </font>[<font size="1">data mining</font>](http://www.jiangtanghu.com/blog/2011/01/15/feature-selection-collections-for-self-study/)<font size="1">). This <em><a href="https://www.coursera.org/course/compdata">Computing for Data Analysis</a></em> course focused mostly on data manipulation and that’s why I chose it to dig into R. R by design is not a tool for data management (where SAS excels), but it’s nice to have (no hurt since it’s free). Those days I put most of my efforts on R data structures(vector, matrix, array, list, data frame) and by grouping processing(*ply functions). Few resource I found extremely useful as a starter:</font>

  * [<font size="1">http://stackoverflow.com/questions/tagged/r</font>](http://stackoverflow.com/questions/tagged/r "http://stackoverflow.com/questions/tagged/r")<font size="1">&#160; when I google a specific R programming technique, mostly I will reach to stackoverflow website, a new generation Q&A hub to replace user forum, mailing list.</font>
  * _[<font size="1">An introduction to R</font>](https://www.google.com/url?sa=t&rct=j&q=&esrc=s&source=web&cd=1&cad=rja&ved=0CDIQFjAA&url=http%3A%2F%2Fcran.r-project.org%2Fdoc%2Fcontrib%2FLam-IntroductionToR_LHL.pdf&ei=O84VUfK7HIue8gSr5YGYBQ&usg=AFQjCNGmMLsnqaHAxGH368m32E8s4STNTA&sig2=Gz7gjUqiPqD-nq_Sg5X57w&bvm=bv.42080656,d.eWU)_ <font size="1">by Longhow Lam, a free book. I like its Chapter 2,<em> Data Objects</em>, including R data types and data structures.</font>
  * <font size="1"><em>Data Manipulation with R</em> by Phil Spector, one of the Use R! books. I used its Chapter 8, <em>Data Aggregation </em>on R by group processing.</font>
  * [<font size="1">RStudio</font>](http://www.rstudio.com/ide/)<font size="1">, a must have R IDE, the best of best. </font>
  * <font size="1">Package </font>[<font size="1">plyr</font>](http://cran.r-project.org/web/packages/plyr/index.html)<font size="1">, tools for splitting, applying and combining data. Actually, it is awful to use R to manipulate data from a SAS programmer point of view. Use plyr to alleviate the pain.</font>
  * <font size="1">Package </font>[<font size="1">sqldf</font>](http://code.google.com/p/sqldf/)<font size="1">, like SAS Proc SQL against data frame. Reason, ibid. Use sqldf won’t enhance your R programming skill, but sometime when you feel down at R, you may want to launch piece of SQL scripts you really like.</font>