---
author: Jiangtang Hu
title: 'Feature Selection: Collections for Self Study'
excerpt:
layout: post
category:
  - data mining
tags:
  - data mining
  - feature selection
  - fselector
  - R
post_format: [ ]
---
Recently I start to learn the algorithms and applications of [feature selection][1]. The term  “Feature”, wildly used in machine learning and data mining literatures,  simply means “Variable”. In some practices, for example, a neural network model uses a decision tree as input; the tree performs the function of variables selection.

The Arizona State University is maintaining a repository of feature selection, including original documentations, Matlab packages and user guide for the following popular algorithms so far:

> BLogReg  
> CFS  
> Chi Square  
> FCBF  
> Fisher Score  
> Gini Index  
> Information Gain  
> Kruskal-Wallis  
> mRMR  
> Relief-F  
> SBMLR  
> T-test  
> SPEC  
> *see* <http://featureselection.asu.edu/software.php>

A R package, [FSelector][2], is also useful for step-by-step studying. This package covers:

> **Filters:  
> ***cfs  
> *chi-squared  
> *consistency  
> *correlation  
> –linear.correlation  
> –rank.correlation  
> *entropy.based  
> –information.gain  
> –gain.ratio  
> –symmetrical.uncertainty  
> *OneR  
> *random.forest.importance  
> *relif-F
> 
> **Wrappers:**  
> *best.first.search  
> *exhaustive.search  
> *greedy.search  
> –backward.search  
> –forward.search  
> *hill.climbing.search

 [1]: http://en.wikipedia.org/wiki/Feature_selection
 [2]: http://cran.r-project.org/web/packages/FSelector/index.html