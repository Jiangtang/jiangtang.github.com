---
id: 169
title: 'SAS Data Step&rsquo;s Built-in Loop: An illustrated Example'
date: 2011-01-03T17:29:40+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/01/03/sas-data-steps-built-in-loop-an-illustrated-example/
permalink: /2011/01/03/sas-data-steps-built-in-loop-an-illustrated-example/
categories:
  - SAS
tags:
  - C++
  - implicit built-in loop
  - Loop
  - SAS
---
Some newbie SAS programmers take SAS as their first programming language even learned. Sometimes they are confused by the concept of “data step’s built-in loop” even after reading the well-written _The Little SAS Book: A Primer_:

> DATA steps also have an underlying structure, an implicit, built-in loop. You don’t tell SAS to execute this loop: SAS does it automatically. Memorize this:
> 
> **DATA steps execute line by line and observation by observation.**

Programmers could memorize the statement above and apply it well in their programming practices, but still find it hard to get the vivid idea about the so called **implicit** built-in loop. –This post would make it easy.

The following will show an **explicit** loop example in C++. Note that you do not need to know any about C++ to get the idea. Suppose that a data file _data.dat_ in D driver holds three numbers

> 1
  
> 2
  
> 3

The question is how to (read and) print out these numbers and their sums.  Following is the C++ approach (**just read the bold session**):

> <span style="font-family: 'Courier New';">#include <iostream><br /> #include <fstream><br /> using namespace std;<br /> int main()<br /> {<br /> int x;<br /> int sum=0;<br /> ifstream inFile;<br /> inFile.open(&#8220;d:data.dat&#8221;);<br /> inFile >> x; </span>
> 
> <span style="font-family: 'Courier New';"><strong> while (<span style="color: #ff0000;">!inFile.eof( )</span>)<br /> {<br /> cout<<x<<endl;<br /> sum = sum + x;<br /> inFile >> x;<br /> }</strong> </span>
> 
>  <span style="font-family: 'Courier New';">inFile.close( );<br /> cout << &#8220;Sum = &#8221; << sum << endl;<br /> return 0;<br /> }</span>

There is an **explicit** loop in these C++ codes: while (<span style="color: #ff0000;">!inFile.eof( )</span>) .  While it is not at the end of infile, the codes above will keep print out the numbers and do the accumulation. The final output is

> 1
  
> 2
  
> 3
  
> sum=6

The following SAS codes produce the exactly same output:

> <span style="font-family: 'Courier New';">data _null_;<br /> infile &#8220;d:data.dat&#8221; end=eof;<br /> input x;<br /> sum+x;<br /> put x;<br /> if eof then put sum=;<br /> run;</span>

Note that SAS codes do not need an **explicit** loop to reach to the end of file. There is a so called **implicit** built-in loop.<the end>