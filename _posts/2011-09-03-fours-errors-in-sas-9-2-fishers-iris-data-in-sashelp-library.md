---
id: 375
title: 'Fours Errors in SAS 9.2 Fisher&#8217;s Iris Data in SASHELP Library'
date: 2011-09-03T21:13:42+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/09/03/fours-errors-in-sas-9-2-fishers-iris-data-in-sashelp-library/
permalink: /2011/09/03/fours-errors-in-sas-9-2-fishers-iris-data-in-sashelp-library/
categories:
  - misc
  - SAS
tags:
  - Fisher
  - Iris
  - SAS
---
[<img style="border-bottom: 0px; border-left: 0px; display: block; float: none; margin-left: auto; border-top: 0px; margin-right: auto; border-right: 0px" title="iris" border="0" alt="iris" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/09/iris_thumb.gif" width="240" height="237" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/09/iris.gif)

In the <a href="http://www.jiangtanghu.com/blog/2011/08/31/who-is-alfred/" target="_blank">previous post</a>, I just mentioned that <a href="http://en.wikipedia.org/wiki/Iris_flower_data_set" target="_blank">Fisher&#8217;s Iris Data</a> is embedded officially in SASHELP library in SAS 9.2. Note that even in SAS 9.1.3, you can also find this data with several instances from some demos in user guide (just search "Iris" in "SAS Help and Documentation" accompany with you SAS product), for example, in <a href="http://support.sas.com/onlinedoc/913/getDoc/en/imlug.hlp/graphstart_sect13.htm" target="_blank">SAS 9.1.3 IML</a>.

Iris dataset is so important and popular that researchers round the world use it as benchmark to test and compare their algorithms and also as pedagogical purpose. It is also the overwhelming No. 1 dataset considering popularity in <a href="http://archive.ics.uci.edu/ml/" target="_blank">UCI Machine Learning Repository</a>. Here 4 errors in SASHELP.iris listed for your consideration if interested and if you find some slightly differences in outputs following some demos out of SAS using this data:

> Error 1: Line 35, the PetalWidth of Setosa should be 2 mm, not 1 mm;
> 
> Error 2: Line 38, the SepalWidth of Setosa should be 36 mm, not 31 mm;
> 
> Error 3: Line 38, the PetalLength of Setosa should be 14 mm, not 15 mm;
> 
> Error 4: Line 119, the PetalLength of Virginica should be 69 mm, not 70 mm.

For errors 1-3, there is also an interesting story in statistical literature. In 1936, Fisher the Great published his famous paper, _<a href="http://rcs.chph.ras.ru/Tutorials/classification/Fisher.pdf" target="_blank">The use of multiple measurements in taxonomic problems</a>_ and the Iris data also attached (called <font color="#ff0000">Fisher Version</font> in this post). In the following years (until today), people <a href="http://archive.ics.uci.edu/ml/datasets/Iris" target="_blank">cited</a> this paper and the Iris data Fisher Version is also replicated and distributed worldwide and then a version with above errors 1-3 might gain a very dominant popularity (I don’t know the source of there errors). In UCI Machine Learning Repository, the dataset <a href="http://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data" target="_blank">iris.data</a> is the one with such 3 errors (called <font color="#ff0000">UCI Version</font> as well).

We could see that the duplicated UCI Version is even more popular in some extension than its original Fisher Version (SASHELP.iris also seems to be copied from UCI Version). Story goes on. In 1998, James Bezdek and other scholars just found the three discrepancies between Iris Fisher Version and UCI Version (and in some published papers using the same version of data). You can read it in _<a href="http://pages.bangor.ac.uk/~mas00a/papers/jbjkrklknptfs99.pdf" target="_blank">Will the Real Iris Data Please Stand Up?</a>_ 

Bezdek then proposed to use the original Fisher Version of Iris, and UCI Machine Learning Repository also <a href="http://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.names" target="_blank">documented these three errors</a> and added new dataset called <a href="http://archive.ics.uci.edu/ml/machine-learning-databases/iris/bezdekIris.data" target="_blank">bezdekIris.data</a> (<font color="#ff0000">Bezdek Version</font>) which is exactly Fisher Version (iris.data kept and I think it is because now the so called error version is also valuable).

Return to error 4 and I can’t figure out why and I might as well call it Iris <font color="#ff0000">SAS Version</font>. Note that the unit in SAS Version is millimeter (mm), while others version all use centimeter (cm). 

The interesting part is that I also check the <a href="http://support.sas.com/onlinedoc/913/getDoc/en/imlug.hlp/graphstart_sect13.htm" target="_blank">Iris data in SAS 9.1.3 IML</a> mentioned before and not surprising, it is exactly the Fisher Version (you can also find a right one in a demo from <a href="http://support.sas.com/documentation/cdl/en/imlsug/62558/HTML/default/viewer.htm#ugappdatasets_sect11.htm" target="_blank">SAS 9.2 IML Studio 3.2</a>).

The following codes generate several Iris versions:

> iris_uci: <font color="#ff0000">UCI Version</font> with both CM and MM as unit
> 
> bezdekiris_uci: <font color="#ff0000">Bezdek Version</font> or <font color="#ff0000">Fisher Version</font> with both CM and MM as unit
> 
> iris_mm: <font color="#ff0000">UCI Version</font> with MM as unit and attributes alike SASHELP.iris, <font color="#ff0000">SAS Version</font>
> 
> bezdekiris_mm: <font color="#ff0000">Bezdek Version</font> or <font color="#ff0000">Fisher Version</font> with MM as unit and attributes alike SASHELP.iris, <font color="#ff0000">SAS Version</font>

<!--more-->


  


> <font face="Courier New">filename iris URL "</font>[<font face="Courier New">http://archive.ics.uci.edu/ml/machine-learning-databases/iris/";</font>](http://archive.ics.uci.edu/ml/machine-learning-databases/iris/";)
> 
> <font face="Courier New">%macro getIris(input); <br />data &input._uci; <br />&#160;&#160;&#160; length _Species $15.; <br />&#160;&#160;&#160; length&#160; Species $10.; <br />&#160;&#160;&#160; infile iris(&input..data) dlm=&#8217;,&#8217;; <br />&#160;&#160;&#160; input _SepalLength _SepalWidth _PetalLength _PetalWidth _Species $; </font>
> 
> <font face="Courier New">&#160;&#160;&#160; Species=propcase(scan(_Species,2)); </font>
> 
> <font face="Courier New">&#160;&#160;&#160; array iris {*}&#160; _SepalLength _SepalWidth _PetalLength _PetalWidth; <br />&#160;&#160;&#160; array iris_mm{4} SepalLength&#160; SepalWidth&#160; PetalLength&#160; PetalWidth; </font>
> 
> <font face="Courier New">&#160;&#160;&#160; do i=1 to dim(iris); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; iris_mm{i}=iris{i}*10; <br />&#160;&#160;&#160; end; </font>
> 
> <font face="Courier New">&#160;&#160;&#160; drop i; </font>
> 
> <font face="Courier New">&#160;&#160;&#160; label&#160;&#160; _sepallength=&#8217;Sepal Length (cm)&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; _sepalwidth =&#8217;Sepal Width (cm)&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; _petallength=&#8217;Petal Length (cm)&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; _petalwidth =&#8217;Petal Width (cm)&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; _Species =&#8217;Iris Species&#8217;; </font>
> 
> <font face="Courier New">&#160;&#160;&#160; label&#160;&#160; sepallength=&#8217;Sepal Length (mm)&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; sepalwidth =&#8217;Sepal Width (mm)&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; petallength=&#8217;Petal Length (mm)&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; petalwidth =&#8217;Petal Width (mm)&#8217; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; Species =&#8217;Iris Species&#8217;; <br />run; </font>
> 
> <font face="Courier New">data &input._mm (label="Fisher&#8217;s Iris Data (1936)"); <br />&#160;&#160;&#160; set &input._uci; <br />&#160;&#160;&#160; drop _:; <br />run; </font>
> 
> <font face="Courier New">%mend getIris; </font>
> 
> <font face="Courier New">%getIris(iris) <br />%getIris(bezdekIris)</font>