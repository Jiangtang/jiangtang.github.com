---
id: 1277
title: 3 Ways to Convert SAS Datasets to Plain Codes
date: 2013-11-04T21:19:49+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1277
permalink: /2013/11/04/3-ways-to-convert-sas-datasets-to-plain-codes/
categories:
  - SAS
tags:
  - ODS
  - ODS Markup
  - SAS
  - SAS Enterprise Guide
---
##### 1. If you have SAS Enterprise Guide installed

Try one of Chris Hemedinger’s EG plug-ins, “_[Data Set to DATA Step](http://support.sas.com/documentation/onlinedoc/guide/customtasks/book/)_”. Chris also wrote a post for it, _[Turn your data set into a DATA step program](http://blogs.sas.com/content/sasdummy/2013/01/21/turn-your-data-set-into-a-data-step-program/)_.

##### 2. If you need to embed the dataset to SQL Clauses

Use one of Eric Gebhart’s ODS tagsets, “[SQL Tagset](http://support.sas.com/rnd/base/ods/odsmarkup/sql.html)”. 

##### 3. If you want to make your hands dirty…

You can also take a bite of some SAS base codes by Rick Langston. Check out his 2011 paper, _[Recreating SAS Data Sets via SAS Code Generation](http://support.sas.com/resources/papers/proceedings11/064-2011.pdf)_.