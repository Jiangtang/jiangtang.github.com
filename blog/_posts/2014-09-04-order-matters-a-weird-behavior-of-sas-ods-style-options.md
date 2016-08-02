---
id: 1353
title: 'Order Matters: A Weird Behavior of SAS ODS Style Options'
date: 2014-09-04T14:24:16+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1353
permalink: /2014/09/04/order-matters-a-weird-behavior-of-sas-ods-style-options/
categories:
  - SAS
tags:
  - ODS
  - SAS
---
The codes to push a dataset to Excel (_technically XML_):

> <font face="Courier New">ods tagsets.excelxp file="test.xls"; <br />&#160; <br />*#1; <br />ods tagsets.excelxp options( sheet_name=&#8217;test 1&#8242;); <br />proc print data=sashelp.class noobs; <br />&#160;&#160;&#160; var height / <font color="#ff0000">style={tagattr=&#8217;format:text&#8217;}</font> style(column)={cellwidth=.5 in}; <br />run;</font>
> 
> <font face="Courier New">*#2;&#160; <br />ods tagsets.excelxp options( sheet_name=&#8217;test 2&#8242;); <br />proc print data=sashelp.class noobs; <br />&#160;&#160;&#160; var height / style(column)={cellwidth=.5 in} <font color="#ff0000">style={tagattr=&#8217;format:text&#8217;}</font> ; <br />run; <br />&#160; <br />ods tagsets.excelxp close;</font>

The output of #1:[<img title="SAS_ODS_options1" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; border-left: 0px; display: block; padding-right: 0px" border="0" alt="SAS_ODS_options1" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2014/09/SAS_ODS_options1_thumb.png" width="295" height="575" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2014/09/SAS_ODS_options1.png)

#2:[<img title="SAS_ODS_options2" style="border-top: 0px; border-right: 0px; background-image: none; border-bottom: 0px; float: none; padding-top: 0px; padding-left: 0px; margin: 3px auto 5px; border-left: 0px; display: block; padding-right: 0px" border="0" alt="SAS_ODS_options2" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2014/09/SAS_ODS_options2_thumb.png" width="318" height="567" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2014/09/SAS_ODS_options2.png)

The difference among the two pieces of code, #1 and #2 is trivial, as far as observed: only the position of the ODS style options was swapped. The weird thing is that they produced different outputs with different column width and cell format.

The answer: I don’t know. I threw this question to SAS-L and SAS tech and we might come back to this question days later.