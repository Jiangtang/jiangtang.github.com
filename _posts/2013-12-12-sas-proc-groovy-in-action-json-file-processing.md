---
id: 1284
title: 'SAS Proc Groovy in Action: JSON File Processing'
date: 2013-12-12T13:30:49+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1284
permalink: /2013/12/12/sas-proc-groovy-in-action-json-file-processing/
categories:
  - SAS
  - XML
tags:
  - JSON
  - SAS
  - XML
---
<font size="1">Last year I took a bite of </font>[<font size="1">the newly SAS Proc Groovy to read JSON data</font>](http://www.jiangtanghu.com/blog/2012/10/28/hello-groovy-in-sas-9-3/) <font size="1">since there was no direct “proc import” or “infile” or “libname” way to play with JSON. Here is an nice example from SAS official blog, by Falko Schulz where Proc Groovy is used to parse Twitter JSON file:</font>

> _[<font size="1">How to import Twitter tweets in SAS DATA Step using OAuth 2 authentication style</font>](http://blogs.sas.com/content/sascom/2013/12/12/how-to-import-twitter-tweets-in-sas-data-step-using-oauth-2-authentication-style/)_

<font size="1">PS: Since SAS 9.4, you can output a JSON file by </font>[<font size="1">Proc JSON</font>](http://support.sas.com/documentation/cdl/en/proc/64787/HTML/default/viewer.htm#n0nejfk9q0pzmnn181l92qk3ah2e.htm)<font size="1">, but still no XML-libname-engine like JSON parser available.</font>