---
id: 179
title: Decision Trees in SAS Enterprise Miner and SPSS Clementine
date: 2011-01-04T20:44:50+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/01/04/decision-trees-in-sas-enterprise-miner-and-spss-clementine/
permalink: /2011/01/04/decision-trees-in-sas-enterprise-miner-and-spss-clementine/
categories:
  - data mining
  - Industry Review
  - SAS
tags:
  - C5.0
  - CART
  - CHAID
  - data mining
  - decision tree
  - IBM
  - QUEST
  - SAS
  - SPSS
  - SPSS Clementine
---
Decision trees are included in SAS Enterprise Miner(EM). The counterpart is SPSS Clementine, which should be called IBM SPSS Modeler for precision after IBM’s acquisition of SPSS.

Recently I read a paper on the comparisons of SAS EM, SPSS Clementine and IBM Intelligent Miner on their decision tree and cluster technology:

> _<a href="http://www.gimi.us/CLUTE_INSTITUTE/ORLANDO_2010/Article%2520452.pdf" target="_blank">Decision Tree Induction & Clustering Techniques in SAS Enterprise Miner, SPSS Clementine, and IBM Intelligent Miner – A Comparative Analysis</a>_ by Abdullah M. Al Ghoson, Virginia Commonwealth University 

The output is not that surprising. SAS EM plays better in performance, functionality and auxiliary task support but worse in usability.

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="SAS_VS_SPSS" border="0" alt="SAS_VS_SPSS" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/SAS_VS_SPSS_thumb.png" width="503" height="476" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/SAS_VS_SPSS.png) 

Here are few comments on decision trees implementations in SAS EM and SPSS Clementine based on my own experiences. Some advises for beginners are also supplied.

There are four nodes in SPSS Clementine to supports four trees algorithms respectively: <font color="#ff0000">C5.0</font>, Classification And Regression Trees (<font color="#ff0000">CART</font>),&#160; Quick, Unbiased, Efficient Statistical Tree(<font color="#ff0000">QUEST</font>) and Chi-squared Automatic Interaction Detector(<font color="#ff0000">CHAID</font>),&#160; which are most famous and popular in decision trees family.

[<img style="border-bottom: 0px; border-left: 0px; display: block; float: none; margin-left: auto; border-top: 0px; margin-right: auto; border-right: 0px" title="SPSS_4_trees" border="0" alt="SPSS_4_trees" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/SPSS_4_trees_thumb.png" width="412" height="105" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/SPSS_4_trees.png) Note that CART(R) is a registered trademark of California Statistical Software, Inc., and is licensed exclusively to Salford Systems, San Diego, California. So SPSS Clementine uses C&R Tree as name.

In SAS EM, there is only one decision tree node:

[<img style="border-bottom: 0px; border-left: 0px; display: block; float: none; margin-left: auto; border-top: 0px; margin-right: auto; border-right: 0px" title="SAS_tree" border="0" alt="SAS_tree" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/SAS_tree_thumb.png" width="155" height="74" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/SAS_tree.png) The algorithms behind this node is called SAS tree algorithms, which incorporate and extend the four mentioned before. Just change the settings in decision tree node, you can get the trees you want. 

Obviously, SAS tree algorithms is superior than the separated ones in SPSS Clementine for expansibility and flexibility. But at the other hand, the complexities increase. For a newbie user of SAS EM, he/she may wonder which trees he/she is training. A SPSS Clementine users just picks up a node and says: OK, I am now training a CART or CHAID.—he/she would communicate with others more smoothly.

Regardless of the industry application, I think this is the educational benefit of SPSS Clementine. Since almost every data mining book introduces decision trees by separated algorithms(such as ID3/C4.5/C5.0, CART, QUEST, CHAID, . . .), the beginners using SPSS Clementine as instructional tool may get the clear ideas about the algorithms one by one. Once he/she get the full understanding of the differences among tree algorithms, he/she would train trees in SAS EM more comfortable.

What’s more, SPSS Clementine supplies rich supporting documentations for beginners and self learners , such as Tutorial, User Guide, Algorithms Guide, Node Reference. The official documentations of SAS EM 5.x and 6.x are relatively poor. Yes there is a good SAS Help and Documentation for SAS EM 4.3 including _Getting Started with Enterprise Miner_. EM4.3 is a traditional AF application but EM5.x and above are Java client incorporated in SAS analysis platform(they are totally different!). For EM5.x and above, only installation guides and a plain reference are available.

SAS Institute may have its own marketing strategies. No rich references available, the Institute DOES offer <a href="https://support.sas.com/edu/prodcourses.html?code=MINER&ctry=US" target="_blank">rich training programs</a> in data mining and Enterprise Miner application. Wooo, the big-budget purchasers of SAS EM can also afford the trainings.