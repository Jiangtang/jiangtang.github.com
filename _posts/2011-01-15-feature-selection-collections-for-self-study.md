---
id: 199
title: 'Feature Selection: Collections for Self Study'
date: 2011-01-15T10:58:44+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/01/15/feature-selection-collections-for-self-study/
permalink: /2011/01/15/feature-selection-collections-for-self-study/
categories:
  - data mining
tags:
  - data mining
  - feature selection
  - fselector
  - R
---
Recently I start to learn the algorithms and applications of <a href="http://en.wikipedia.org/wiki/Feature_selection" target="_blank">feature selection</a>. The term  “Feature”, wildly used in machine learning and data mining literatures,  simply means “Variable”. In some practices, for example, a neural network model uses a decision tree as input; the tree performs the function of variables selection.

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
  
> _<span style="color: #ff0000;">see</span>_ <a href="http://featureselection.asu.edu/software.php" target="_blank">http://featureselection.asu.edu/software.php</a>

A R package, <a href="http://cran.r-project.org/web/packages/FSelector/index.html" target="_blank">FSelector</a>, is also useful for step-by-step studying. This package covers:

> **Filters:
  
>** *cfs
  
> *chi-squared
  
> *consistency
  
> *correlation
  
> &#8211;linear.correlation
  
> &#8211;rank.correlation
  
> *entropy.based
  
> &#8211;information.gain
  
> &#8211;gain.ratio
  
> &#8211;symmetrical.uncertainty
  
> *OneR
  
> *random.forest.importance
  
> *relif-F
> 
> **Wrappers:**
  
> *best.first.search
  
> *exhaustive.search
  
> *greedy.search
  
> &#8211;backward.search
  
> &#8211;forward.search
  
> *hill.climbing.search