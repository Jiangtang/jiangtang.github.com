---
id: 423
title: Hello Python
date: 2011-10-31T20:29:43+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/10/31/hello-python/
permalink: /2011/10/31/hello-python/
categories:
  - misc
tags:
  - Python
---
Inspired by <a href="http://www.jiangtanghu.com/blog/2011/08/15/sas-bloggers-in-action-2-jian-dai-and-his-sas-academy/" target="_blank">Jian’s polyglot programming practice</a>, I also begin to brush up Python and C++ which I learned during graduate school. Following is a Python response to one of <a href="http://tech.groups.yahoo.com/group/sas_academy/" target="_blank">Jian Dai</a>’s former programming challenges for <a href="http://blog.clinovo.com/megha-becomes-the-third-time-winner-june-programming-challenge-now-is-finished/" target="_blank">lines count of source codes</a>:
  
[cce lang=&#8221;python&#8221;]
  
import os

#count number of lines of
  
#single file
  
def lineCount(fileName):
	  
countSingle=0
	  
for line in open(fileName):
		  
countSingle += 1
	  
return countSingle

#count number of lines of
  
#directory and subdirectories
  
def dirCount(dir,extension):
	  
countTotal=0
	  
for r,d,f in os.walk(dir):
		  
for files in f:
			  
if files.endswith(extension):
				  
fileName=os.path.join(r,files)
				  
countSingle=lineCount(fileName)
				  
countTotal += countSingle
	  
return countTotal

a=dirCount(&#8220;C:/Program Files/CDISC Express/&#8221;,&#8221;.sas&#8221;)

print a
  
[/cc]

I use <a href="http://www.jiangtanghu.com/docs/en/readME_IDE.txt" target="_blank">python-2.7.2</a>, the final Python 2.x release most because of the various modules support for learning purpose. The book helps me to get the quick review of Python is _<a href="http://greenteapress.com/thinkpython/thinkpython.html" target="_blank">Think Python: How to Think Like a Computer Scientist</a>_ by Allen Downey.

Also, I begin to use <a href="http://kpumuk.info/projects/wordpress-plugins/codecolorer/" target="_blank">CodeColorer</a> for this blog to insert codes.