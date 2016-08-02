---
id: 1389
title: 'SAS Combinatorial Functions: Snippets'
date: 2015-06-25T12:55:38+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1389
permalink: /2015/06/25/sas-combinatorial-functions-snippets/
categories:
  - SAS
tags:
  - combination
  - IML
  - SAS
---
### 1. Permutation and Combination

> <span style="font-family: 'Courier New'; font-size: xx-small;">data _null_;<br /> n = 5;<br /> r = 2;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">   *the factorial of a number;<br /> fact=fact(n);</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">   *for positive integers, fact(n) = gamma(n+1);<br /> gamm=gamma(n + 1);</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">   *C(n,r): number of combinations of n objects selected r ;<br /> *n! / [r!(n-r)!];<br /> comb1 = comb(n,r);<br /> comb2 = fact(n) / (fact(r) * fact(n-r));<br /> comb3 = gamma(n+1) / (gamma(r+1) * gamma(n-r+1));<br /> comb4 = exp(lcomb(n,r));<br /> comb5 = exp(lgamma(n+1)-lgamma(r+1)-lgamma(n-r+1));</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">   *A(n,r): number of permutation (ordered arrangements);<br /> *n! / (n-r)!;<br /> perm1 = perm(n,r);<br /> perm2 = fact(n) /  fact(n-r);<br /> perm3 = gamma(n+1) /  gamma(n-r+1);<br /> perm4 = exp(lperm(n,r));<br /> perm5 = exp(lgamma(n+1)-lgamma(n-r+1));</span>
> 
> <span style="font-size: xx-small;"><span style="font-family: 'Courier New';">   put (_all_) (= / );<br /> run;</span><br /> </span>

<span style="font-size: xx-small;">Note functions <em>fact()</em> and <em>gamm()</em> can quickly reach out their limitations(<em>try n=<span style="color: #ff0000;">171 </span></em>and check the overflow notes in Log window).</span>

<h3 align="left">
  2. Generate Unique Pairs
</h3>

<span style="font-size: xx-small;">Question see </span>[<span style="font-size: xx-small;">here</span>](http://stackoverflow.com/questions/19875633/how-to-pick-unique-pairs-from-a-single-list)<span style="font-size: xx-small;">.</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">data _null_;<br /> array x[5] $1 (&#8220;A&#8221; &#8220;C&#8221; &#8220;D&#8221; &#8220;B&#8221; &#8220;E&#8221;);<br /> n = dim(x);<br /> r = 2;<br /> ncomb = comb(n, r);<br /> do j = 1 to ncomb+1;<br /> rc = <span style="color: #ff0000;">allcomb</span>(j, r, of x[*]);<br /> if rc < 0 then leave;<br /> put j 5. +3 x1 “- ” x2 +3;<br /> end;<br /> run;</span>

<span style="font-size: xx-small;">The output in Log:</span>

> <span style="font-size: xx-small;">1   A &#8211; C<br /> 2   A &#8211; E<br /> 3   A &#8211; B<br /> 4   A &#8211; D<br /> 5   C &#8211; D<br /> 6   C &#8211; E<br /> 7   C &#8211; B<br /> 8   D &#8211; B<br /> 9   D &#8211; E<br /> 10   B &#8211; E</span>

<span style="font-size: xx-small;">Or if you like alphabetical sorted pairs:</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">data _null_;<br /> array x[5] $1 (&#8220;A&#8221; &#8220;C&#8221; &#8220;D&#8221; &#8220;B&#8221; &#8220;E&#8221;);<br /> n = dim(x);<br /> r = 2;<br /> ncomb = comb(n, r);<br /> do j = 1 to ncomb+1;<br /> rc = <span style="color: #ff0000;">lexcomb</span>(j, r, of x[*]);<br /> if rc < 0 then leave;<br /> put j 5. +3 x1 “- ” x2 +3;<br /> end;<br /> run;</span>

<span style="font-size: xx-small;">The output:</span>

> <span style="font-size: xx-small;">1   A &#8211; B<br /> 2   A &#8211; C<br /> 3   A &#8211; D<br /> 4   A &#8211; E<br /> 5   B &#8211; C<br /> 6   B &#8211; D<br /> 7   B &#8211; E<br /> 8   C &#8211; D<br /> 9   C &#8211; E<br /> 10   D &#8211; E</span>

<span style="font-size: xx-small;">I checked </span>[<span style="font-size: xx-small;">Rick Wicklin’s blog</span>](http://blogs.sas.com/content/iml/) <span style="font-size: xx-small;">and found  </span>[<span style="font-size: xx-small;">PROC IML</span>](http://blogs.sas.com/content/iml/2013/09/30/generate-combinations-in-sas.html) <span style="font-size: xx-small;">offers a much more intuitive approach to this problem:</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">proc iml;<br /> n = 5;<br /> r = 2;<br /> idx = <span style="color: #ff0000;">allcomb</span>(n, r);<br /> print idx;<br /> quit;</span>

<span style="font-size: xx-small;">The output:</span>

> <span style="font-size: xx-small;">1 2<br /> 2 3<br /> 1 3<br /> 3 4<br /> 2 4<br /> 1 4<br /> 4 5<br /> 3 5<br /> 2 5<br /> 1 5 </span>

<span style="font-size: xx-small;">or make the output more readable:</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">proc iml;<br /> n = 5;<br /> r = 2;<br /> idx = allcomb(n, r);<br /> print idx;</span>
> 
> <span style="font-family: 'Courier New'; font-size: xx-small;">    Items = {&#8220;A&#8221; &#8220;C&#8221; &#8220;D&#8221; &#8220;B&#8221; &#8220;E&#8221;};<br /> S = Items[ ,idx];<br /> S = shape(S, 0, r);<br /> print S[r=(char(1:nrow(S)))];<br /> quit;</span>

<span style="font-size: xx-small;">the output:</span>

> <span style="font-size: xx-small;">1  A C<br /> 2  C D<br /> 3  A D<br /> 4  D B<br /> 5  C B<br /> 6  A B<br /> 7  B E<br /> 8  D E<br /> 9  C E<br /> 10 A E </span>

### 3. Generate Unique Pairs: A Macro

<span style="font-size: xx-small;">Years ago when the build-in functions above might not be available in SAS, a </span>[<span style="font-size: xx-small;">macro %combo</span>](http://www.urz.uni-heidelberg.de/statistik/sas/doc/ts498-combperm.txt) <span style="font-size: xx-small;">did the same job:</span>

> <span style="font-family: 'Courier New'; font-size: xx-small;">%combo(2,a,c,d,b,e)</span>

<span style="font-size: xx-small;">The output:</span>

> <span style="font-size: xx-small;">1  a c<br /> 2  a d<br /> 3  a b<br /> 4  a e<br /> 5  c d<br /> 6  c b<br /> 7  c e<br /> 8  d b<br /> 9  d e<br /> 10 b e<br /> </span>

<span style="font-size: xx-small;">It’s fun to check out the macro how to implement it by arrays.</span>