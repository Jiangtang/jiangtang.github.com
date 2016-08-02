---
author: Jiangtang Hu
title: Set Up R (for SAS Programmers)
excerpt:
layout: post
category:
  - R
tags:
  - IML
  - R
  - RStudio
  - SAS
post_format: [ ]
---
> # Yep, I am a SAS programmer: during the day time, I use SAS for my work; at the evening, I use R for entertainment.—
> 
> # [Charlie Huang][1]

Getting start to play with R (it is really a wonderful learning tool):

##### 12. [SAS IML Studio and R Integration][2] (*not tested*)

##### 11. [SAS IML and R Integration][3] (*not tested*)

##### 10. [SAS Base and R Integration: PROC R][4]

also [a blog post][5].

##### 9. Data transfer among R and SAS(xpt)

SAS: *[SAS Macros that Convert a Directory of Transport Files][6]*

R: use [read.xport][7] function in Foreign package and write.xport in [SASXport][8] package to read/write xpt file

##### 8. Data transfer among R and SAS(CSV)

SAS: use [%DS2CSV Macro][9] to export SAS dataset to CSV file

R: use [read.csv][10] /[write.csv][11] function to read/write CSV file

##### 7. [The R Graph Gallery][12]

##### 6. [R blogs][13]

##### 5. [R search][14]

##### 4. [R Task View][15]: packages recommended

##### 3. [All R packages][16]

##### 2. Install [RStudio][17], a much better R IDE

##### 1. Get [R software][18]

 [1]: http://www.sasanalysis.com/2011/05/support-vector-machine-for.html
 [2]: http://support.sas.com/documentation/cdl/en/imlsstat/65548/HTML/default/viewer.htm#imlsstat_statr_toc.htm
 [3]: http://support.sas.com/documentation/cdl/en/imlug/65547/HTML/default/viewer.htm#imlug_r_sect001.htm
 [4]: http://www.jstatsoft.org/v46/c02
 [5]: http://sas-and-r.blogspot.com/2012/01/sas-macro-simplifies-sas-and-r.html
 [6]: http://www.sas.com/industry/government/fda/macro.html
 [7]: http://stat.ethz.ch/R-manual/R-devel/library/foreign/html/read.xport.html
 [8]: http://cran.cnr.berkeley.edu/web/packages/SASxport/index.html
 [9]: http://support.sas.com/documentation/cdl/en/lebaseutilref/63492/HTML/default/viewer.htm#n0yo3bszlrh0byn1j4fxh4ndei8u.htm
 [10]: http://stat.ethz.ch/R-manual/R-devel/library/utils/html/read.table.html
 [11]: http://stat.ethz.ch/R-manual/R-devel/library/utils/html/write.table.html
 [12]: http://gallery.r-enthusiasts.com/
 [13]: http://www.r-bloggers.com/
 [14]: http://www.r-project.org/search.html
 [15]: http://cran.r-project.org/web/views/
 [16]: http://cran.cnr.berkeley.edu/web/packages/available_packages_by_name.html
 [17]: http://www.rstudio.org/download/
 [18]: http://cran.cnr.berkeley.edu/