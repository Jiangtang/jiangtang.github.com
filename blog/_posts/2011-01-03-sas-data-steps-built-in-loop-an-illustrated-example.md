---
author: Jiangtang Hu
title: 'SAS Data Step&rsquo;s Built-in Loop: An illustrated Example'
excerpt:
layout: post
category:
  - SAS
tags:
  - C++
  - implicit built-in loop
  - Loop
  - SAS
post_format: [ ]
---
Some newbie SAS programmers take SAS as their first programming language even learned. Sometimes they are confused by the concept of “data step’s built-in loop” even after reading the well-written *The Little SAS Book: A Primer*:

> DATA steps also have an underlying structure, an implicit, built-in loop. You don’t tell SAS to execute this loop: SAS does it automatically. Memorize this:
> 
> **DATA steps execute line by line and observation by observation.**

Programmers could memorize the statement above and apply it well in their programming practices, but still find it hard to get the vivid idea about the so called **implicit** built-in loop. –This post would make it easy.

The following will show an **explicit** loop example in C++. Note that you do not need to know any about C++ to get the idea. Suppose that a data file *data.dat* in D driver holds three numbers

> 1  
> 2  
> 3

The question is how to (read and) print out these numbers and their sums.  Following is the C++ approach (**just read the bold session**):

> #include <iostream>  
> #include <fstream>  
> using namespace std;  
> int main()  
> {  
> int x;  
> int sum=0;  
> ifstream inFile;  
> inFile.open(“d:data.dat”);  
> inFile >> x; 
> 
> ** while (!inFile.eof( ))  
> {  
> cout<<x<<endl;  
> sum = sum + x;  
> inFile >> x;  
> }** 
> 
>  inFile.close( );  
> cout << “Sum = ” << sum << endl;  
> return 0;  
> }

There is an **explicit** loop in these C++ codes: while (!inFile.eof( )) .  While it is not at the end of infile, the codes above will keep print out the numbers and do the accumulation. The final output is

> 1  
> 2  
> 3  
> sum=6

The following SAS codes produce the exactly same output:

> data \_null\_;  
> infile “d:data.dat” end=eof;  
> input x;  
> sum+x;  
> put x;  
> if eof then put sum=;  
> run;

Note that SAS codes do not need an **explicit** loop to reach to the end of file. There is a so called **implicit** built-in loop.<the end>