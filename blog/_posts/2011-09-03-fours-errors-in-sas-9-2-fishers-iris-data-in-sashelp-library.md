---
author: Jiangtang Hu
title: "Fours Errors in SAS 9.2 Fisher's Iris Data in SASHELP Library"
excerpt:
layout: post
category:
  - misc
  - SAS
tags:
  - Fisher
  - Iris
  - SAS
post_format: [ ]
---
[![iris][2]][2]

In the [previous post][2], I just mentioned that [Fisher’s Iris Data][3] is embedded officially in SASHELP library in SAS 9.2. Note that even in SAS 9.1.3, you can also find this data with several instances from some demos in user guide (just search "Iris" in "SAS Help and Documentation" accompany with you SAS product), for example, in [SAS 9.1.3 IML][4].

Iris dataset is so important and popular that researchers round the world use it as benchmark to test and compare their algorithms and also as pedagogical purpose. It is also the overwhelming No. 1 dataset considering popularity in [UCI Machine Learning Repository][5]. Here 4 errors in SASHELP.iris listed for your consideration if interested and if you find some slightly differences in outputs following some demos out of SAS using this data:

> Error 1: Line 35, the PetalWidth of Setosa should be 2 mm, not 1 mm;
> 
> Error 2: Line 38, the SepalWidth of Setosa should be 36 mm, not 31 mm;
> 
> Error 3: Line 38, the PetalLength of Setosa should be 14 mm, not 15 mm;
> 
> Error 4: Line 119, the PetalLength of Virginica should be 69 mm, not 70 mm.

For errors 1-3, there is also an interesting story in statistical literature. In 1936, Fisher the Great published his famous paper, *[The use of multiple measurements in taxonomic problems][6]* and the Iris data also attached (called Fisher Version in this post). In the following years (until today), people [cited][7] this paper and the Iris data Fisher Version is also replicated and distributed worldwide and then a version with above errors 1-3 might gain a very dominant popularity (I don’t know the source of there errors). In UCI Machine Learning Repository, the dataset [iris.data][8] is the one with such 3 errors (called UCI Version as well).

We could see that the duplicated UCI Version is even more popular in some extension than its original Fisher Version (SASHELP.iris also seems to be copied from UCI Version). Story goes on. In 1998, James Bezdek and other scholars just found the three discrepancies between Iris Fisher Version and UCI Version (and in some published papers using the same version of data). You can read it in *[Will the Real Iris Data Please Stand Up?][9]* 

Bezdek then proposed to use the original Fisher Version of Iris, and UCI Machine Learning Repository also [documented these three errors][10] and added new dataset called [bezdekIris.data][11] (Bezdek Version) which is exactly Fisher Version (iris.data kept and I think it is because now the so called error version is also valuable).

Return to error 4 and I can’t figure out why and I might as well call it Iris SAS Version. Note that the unit in SAS Version is millimeter (mm), while others version all use centimeter (cm). 

The interesting part is that I also check the [Iris data in SAS 9.1.3 IML][4] mentioned before and not surprising, it is exactly the Fisher Version (you can also find a right one in a demo from [SAS 9.2 IML Studio 3.2][12]).

The following codes generate several Iris versions:

> iris_uci: UCI Version with both CM and MM as unit
> 
> bezdekiris_uci: Bezdek Version or Fisher Version with both CM and MM as unit
> 
> iris_mm: UCI Version with MM as unit and attributes alike SASHELP.iris, SAS Version
> 
> bezdekiris_mm: Bezdek Version or Fisher Version with MM as unit and attributes alike SASHELP.iris, SAS Version

  
> filename iris URL "<http://archive.ics.uci.edu/ml/machine-learning-databases/iris/";>
> 
> %macro getIris(input);   
> data &input._uci;   
>     length _Species $15.;   
>     length  Species $10.;   
>     infile iris(&input..data) dlm=’,';   
>     input \_SepalLength \_SepalWidth \_PetalLength \_PetalWidth _Species $; 
> 
>     Species=propcase(scan(_Species,2)); 
> 
>     array iris {*}  \_SepalLength \_SepalWidth \_PetalLength \_PetalWidth;   
>     array iris_mm{4} SepalLength  SepalWidth  PetalLength  PetalWidth; 
> 
>     do i=1 to dim(iris);   
>         iris_mm{i}=iris{i}*10;   
>     end; 
> 
>     drop i; 
> 
>     label   _sepallength=’Sepal Length (cm)’   
>             _sepalwidth =’Sepal Width (cm)’   
>             _petallength=’Petal Length (cm)’   
>             _petalwidth =’Petal Width (cm)’   
>             _Species =’Iris Species’; 
> 
>     label   sepallength=’Sepal Length (mm)’   
>             sepalwidth =’Sepal Width (mm)’   
>             petallength=’Petal Length (mm)’   
>             petalwidth =’Petal Width (mm)’   
>             Species =’Iris Species’;   
> run; 
> 
> data &input._mm (label="Fisher’s Iris Data (1936)");   
>     set &input._uci;   
>     drop _:;   
> run; 
> 
> %mend getIris; 
> 
> %getIris(iris)   
> %getIris(bezdekIris)

 []: http://dl.dropbox.com/u/69732603/iris.gif
 [2]: http://www.jiangtanghu.com/blog/2011/08/31/who-is-alfred/
 [3]: http://en.wikipedia.org/wiki/Iris_flower_data_set
 [4]: http://support.sas.com/onlinedoc/913/getDoc/en/imlug.hlp/graphstart_sect13.htm
 [5]: http://archive.ics.uci.edu/ml/
 [6]: http://rcs.chph.ras.ru/Tutorials/classification/Fisher.pdf
 [7]: http://archive.ics.uci.edu/ml/datasets/Iris
 [8]: http://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.data
 [9]: http://pages.bangor.ac.uk/~mas00a/papers/jbjkrklknptfs99.pdf
 [10]: http://archive.ics.uci.edu/ml/machine-learning-databases/iris/iris.names
 [11]: http://archive.ics.uci.edu/ml/machine-learning-databases/iris/bezdekIris.data
 [12]: http://support.sas.com/documentation/cdl/en/imlsug/62558/HTML/default/viewer.htm#ugappdatasets_sect11.htm