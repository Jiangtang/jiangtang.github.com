---
author: Jiangtang Hu
title: Hello Python
excerpt:
layout: post
category:
  - misc
tags:
  - Python
post_format: [ ]
---
Inspired by [Jian’s polyglot programming practice][1], I also begin to brush up Python and C++ which I learned during graduate school. Following is a Python response to one of [Jian Dai][2]’s former programming challenges for [lines count of source codes][3]:  
[cce lang="python"]  
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

a=dirCount(“C:/Program Files/CDISC Express/”,”.sas”)

print a  
[/cc]

I use [python-2.7.2][4], the final Python 2.x release most because of the various modules support for learning purpose. The book helps me to get the quick review of Python is *[Think Python: How to Think Like a Computer Scientist][5]* by Allen Downey.

Also, I begin to use [CodeColorer][6] for this blog to insert codes.

 [1]: http://www.jiangtanghu.com/blog/2011/08/15/sas-bloggers-in-action-2-jian-dai-and-his-sas-academy/
 [2]: http://tech.groups.yahoo.com/group/sas_academy/
 [3]: http://blog.clinovo.com/megha-becomes-the-third-time-winner-june-programming-challenge-now-is-finished/
 [4]: http://www.jiangtanghu.com/docs/en/readME_IDE.txt
 [5]: http://greenteapress.com/thinkpython/thinkpython.html
 [6]: http://kpumuk.info/projects/wordpress-plugins/codecolorer/