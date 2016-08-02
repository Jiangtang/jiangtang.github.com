---
id: 216
title: 'Too Big to Be Accurate(1): Which is the Most Powerful Calculator in the World?'
date: 2011-01-22T17:05:17+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2011/01/22/big-numbers/
permalink: /2011/01/22/big-numbers/
categories:
  - misc
  - SAS
tags:
  - Approximation
  - C++
  - Excel
  - factorial
  - Google Calculator
  - Python
  - R
  - recursion
  - SAS
  - Windows Calculator
  - WolframAlpha
---
Calculate the factorial of 171 (171!)? Just TRY! It is equal to 171\*170\*169\*….2\*1.

### 1. Google calculator

As Google fanatics, I first try to search the answer via Google:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="Google171" border="0" alt="Google171" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/Google171_thumb.png" width="336" height="116" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/Google171.png) 

Whoops, nothing interested returned! Type “170!” and get the output:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="Google170" border="0" alt="Google170" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/Google170_thumb.png" width="244" height="110" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/Google170.png) Why kinda things happened in this calculator? 171! is just equal to 171*170!.

### 2. Excel

Switch to Excel spreadsheet. Function fact(*) used:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="Excel170" border="0" alt="Excel170" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/Excel170_thumb.png" width="228" height="66" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/Excel170.png) [<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="Excel171" border="0" alt="Excel171" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/Excel171_thumb.png" width="244" height="64" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/Excel171.png) Oo, interesting. The same. 

### 3. SAS

Google and Excel may be the niche players in calculators’ family. Why not try to use some programming languages?

<!--more-->

As a SAS programmer, my handy tool is SAS of course.

First, I use **SAS data step** with its build-in function fact(*):

> <font face="Courier New">data _null_; <br />&#160;&#160;&#160; x=fact(170); <br />&#160;&#160;&#160; y=fact(171); <br />&#160;&#160;&#160; put x= y=; <br />run;</font>

and I get

> NOTE: Invalid argument to function FACT at line 49 column 7.   
> <font color="#ff0000">x=7.257416E306 y=.</font>   
> <font color="#ff0000">x=7.257416E306 y=. _ERROR_=1 _N_=1</font>   
> NOTE: Mathematical operations could not be performed at the following places. The results of the operations have been set to missing values.

Expected or unexpected? I don’t know how this fact(*) function is defined, and&#160; try to define a function to calculate the factorials by myself. In SAS 9.2, you can use **PROC FCMP**(also available at 9.1.3 as a experimental procedure):

> <font face="Courier New">proc fcmp outlib = work.funcs.math ; <br />&#160;&#160;&#160; function factorial(k) ; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; if k = 0 then return(1) ; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; z = k ; *preserve k ; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; x = factorial(k-1) ; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; k = z ; *recover k ; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; k = k * x ; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; return(k) ; <br />&#160;&#160;&#160; endsub ; <br />quit ; </font>
> 
> <font face="Courier New">options cmplib=work.funcs ; </font>

Use this self-defined function to get 170!

> <font face="Courier New">proc fcmp ; <br />&#160;&#160;&#160; x = factorial (170) ; <br />&#160;&#160;&#160; put x = ; <br />run ; </font>

The FCMP procedure returns

> x=7.257416E306

Try to calculate 171! ?

> <font face="Courier New">proc fcmp ; <br />&#160;&#160;&#160; y = factorial (171) ; <br />&#160;&#160;&#160; put y = ; <br />run ;</font>

Just get the overflow error. The interaction stops at 170!:

> ERROR: An overflow occurred during execution in function &#8216;factorial&#8217; in statement number 7 at&#160;&#160; line 10 column 1.   
> &#160;&#160;&#160;&#160;&#160;&#160; The statement was:   
> &#160;&#160;&#160; 1&#160;&#160;&#160;&#160;&#160; (10:1)&#160;&#160;&#160; k = (k=171) * (<font color="#ff0000">x=7.257416E306</font>)

The above function definitions use recursion. Recursion may have some limitation on efficiency. We could try the loop without recursion. **SAS/IML** doesn’t support recursion. Let SAS/IML to the court:

> <font face="Courier New">proc iml; <br />&#160;&#160;&#160; start factorial (n); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; fact=1; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; do i=1 to n; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; fact=fact*i; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; end; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; return (fact); <br />&#160;&#160;&#160; finish factorial;</font>
> 
> <font face="Courier New">&#160;&#160;&#160; x= factorial (170); <br />&#160;&#160;&#160; print x;</font>
> 
> <font face="Courier New">&#160;&#160;&#160; y= factorial (171); <br />&#160;&#160;&#160; print y; <br />quit;</font>

Again, I get 170!

> &#160;&#160;&#160; x   
> 7.257E306

and a overflow error for 171!

> &#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; y= factorial (171);   
> ERROR: Overflow error in *.

Turing, Von Neumann and Tony, what happened?

### 4. R

When SAS failed, lots of voices pop up: use R! OK, Rction!

> <font color="#ff0000">> x=factorial(170);x</font>   
> [1] 7.257416e+306   
> <font color="#ff0000">> y=factorial(171);y</font>   
> Warning message:   
> In factorial(171) : value out of range in &#8216;gammafn&#8217;   
> [1] Inf

### 5. C++

I don’t want to lose my patience. Think C++(use both recursive and non-recursive methods):

> <font face="Courier New">#include <iostream> <br />using namespace std; </font>
> 
> <font face="Courier New">double factRecursive(double num); <br />double factNonRecursive(double num); </font>
> 
> <font face="Courier New">int main() <br />{ <br />&#160;&#160;&#160; cout<<endl;&#160;&#160;&#160; <br />&#160;&#160;&#160; cout<<"Recursive: the factorial of 170 is "<<factRecursive(170)<<endl; <br />&#160;&#160;&#160; cout<<"Recursive: the factorial of 171 is "<<factRecursive(171)<<endl; <br />&#160;&#160;&#160; cout<<endl;&#160;&#160; </font>
> 
> <font face="Courier New">&#160;&#160;&#160; cout<<"NonRecursive: the factorial of 170 is "<<factNonRecursive(170)<<endl; <br />&#160;&#160;&#160; cout<<"NonRecursive: the factorial of 171 is "<<factNonRecursive(171)<<endl; <br />&#160;&#160;&#160; cout<<endl;&#160;&#160;&#160; </font>
> 
> <font face="Courier New">return 0; <br />} </font>
> 
> <font face="Courier New">double factRecursive (double num) <br />{ <br />&#160;&#160;&#160; if (num==0) <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; return 1; <br />&#160;&#160;&#160; else <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; return num*factRecursive(num-1); <br />} </font>
> 
> <font face="Courier New">double factNonRecursive (double num) <br />{ <br />&#160;&#160;&#160; double fact=1; <br />&#160;&#160;&#160; for (double i=2;i<=num;i++) fact *=i; <br />&#160;&#160;&#160; return fact; <br />}</font>

Unfortunately, same story once more:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="Cpp" border="0" alt="Cpp" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/Cpp_thumb.png" width="449" height="121" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/Cpp.png)

Well. The story&#8217;s played out like this. It may be not the limitable of the language but the machine. I check which is the largest numbers my computer supports:

> <font face="Courier New">#include <iostream> <br />#include <cfloat> </font>
> 
> <font face="Courier New">using namespace std; </font>
> 
> <font face="Courier New">int main() <br />{ <br />&#160; cout<<"maxinum double value of machine: "<<DBL_MAX<<endl; <br />&#160; return 0; </font><font face="Courier New">}</font>

> <pre>maxinum double value of machine: <font color="#ff0000">1.79769e+308</font></pre>

Now everything’s in the open. The factorial of 170 is about 7.257416e+306. 171! is too big to be supported by my PC. 

(Note: I put these codes in <http://codepad.org>, a online complier. if you don’t have any C++ complier in your machine, you can see the codes and outputs in:<http://codepad.org/xnneavsw>&#160; and <http://codepad.org/3FeEC9t2>)

### 6. <a href="http://www.wolframalpha.com/" target="_blank">WolframAlpha</a>

Struggled for hours, I turn to <a href="http://www.wolframalpha.com" target="_blank">WolframAlpha</a> computing platform. It returns <a href="http://www.wolframalpha.com/input/?i=171!" target="_blank">the factorial of 171</a> AT LAST:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="WA171" border="0" alt="WA171" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/WA171_thumb.gif" width="454" height="128" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/WA171.gif)&#160;[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="WA171_s" border="0" alt="WA171_s" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/WA171_s_thumb.gif" width="477" height="52" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/WA171_s.gif)&#160; AT LAST we know the factorial of 171 has 310 digits. 

### 7. Windows Calculator

I try to use Windows build-in calculator. Amazing, it is powerful:

[<img style="border-right-width: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; margin-left: auto; border-left-width: 0px; margin-right: auto" title="winCalc" border="0" alt="winCalc" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/winCalc_thumb.png" width="323" height="250" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2011/01/winCalc.png)

### 8. Python

Return to programming language.&#160; First, I defined a function(recursive version) in Python and then use its MATH library:

> <font face="Courier New">>>> def factorial(n):<br /> <br />&#160;&#160;&#160; if n==0: </p> 
> 
> <p>
>   &#160;&#160;&#160;&#160;&#160;&#160;&#160; return 1
> </p>
> 
> <p>
>   &#160;&#160;&#160; else:
> </p>
> 
> <p>
>   &#160;&#160;&#160;&#160;&#160;&#160;&#160; return n*factorial(n-1) </font>
> </p>
> 
> <p>
>   <font face="Courier New"><font color="#ff0000">>>> factorial(170)</font> </p> 
>   
>   <p>
>     7257415615307998967396728211129263114716991681296451376
>   </p>
>   
>   <p>
>     5435777989005618434017061578523507492426174595114909912
>   </p>
>   
>   <p>
>     3783852077666602256544275302532890077320751090240043028
>   </p>
>   
>   <p>
>     0058295603966612599658257104398558294257568966313439612
>   </p>
>   
>   <p>
>     2625710949468067112055688804571933402126614528000000000
>   </p>
>   
>   <p>
>     00000000000000000000000000000000L
>   </p>
>   
>   <p>
>     <font color="#ff0000">>>> factorial(171)</font>
>   </p>
>   
>   <p>
>     1241018070217667823424840524103103992616605577501693185
>   </p>
>   
>   <p>
>     3889518036119960752216917529927519781204875855764649595
>   </p>
>   
>   <p>
>     0167038705280988985869071076733124203221848436431047357
>   </p>
>   
>   <p>
>     7889968548278290754541561964852153468318044293239598173
>   </p>
>   
>   <p>
>     6968996572359039476161522785581800611763651084288000000
>   </p>
>   
>   <p>
>     00000000000000000000000000000000000L</font>
>   </p></blockquote> 
>   
>   <blockquote>
>     <p>
>       >>> import math<br /> <br /><font color="#ff0000">>>> math.factorial(171)</font>
>     </p>
>     
>     <p>
>       1241018070217667823424840524103103992616605577501693185
>     </p>
>     
>     <p>
>       3889518036119960752216917529927519781204875855764649595
>     </p>
>     
>     <p>
>       0167038705280988985869071076733124203221848436431047357
>     </p>
>     
>     <p>
>       7889968548278290754541561964852153468318044293239598173
>     </p>
>     
>     <p>
>       6968996572359039476161522785581800611763651084288000000
>     </p>
>     
>     <p>
>       00000000000000000000000000000000000L
>     </p>
>   </blockquote>
>   
>   <p>
>     Amazing, Python beats up C++!
>   </p>
>   
>   <p>
>     <em>(to be continued :</em>
>   </p>
>   
>   <p>
>     <em>Too Big to Be Accurate(2): <font color="#ff0000">Approximation</font> </em>
>   </p>
>   
>   <p>
>     <em>)</em>
>   </p>