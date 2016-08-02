---
id: 700
title: Frequentist or Baysian in A Binomial Test
date: 2012-09-21T01:20:10+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=700
permalink: /2012/09/21/frequentist-or-baysian/
categories:
  - Logic
  - SAS
  - statistics
tags:
  - Bayesian
  - frequentist inference
  - Hypothesis Testing
  - P-value
  - PROC FREQ
  - Proc TTEST
  - SAS
  - statistics
---
<font size="1">A latest updated post on </font><a href="http://www.freakonomics.com" target="_blank"><em><font size="1">Freakonomics</font></em></a><font size="1">, <em><a href="http://www.freakonomics.com/2012/09/20/beware-the-weasel-word-statistical-in-statistical-significance/" target="_blank">Beware the Weasel Word “Statistical” in Statistical Significance!</a></em>,&#160; seemed to attempt to challenge frequentist statistics by Bayesian. I have no research on Bayesian and won’t jump to the debates. I’d rather to use this case to apply the </font><a href="http://www.jiangtanghu.com/blog/2012/09/16/hypothesis-testing/" target="_blank"><font size="1">Dragon’s Teeth and Fleas logic of hypothesis testing</font></a> (at least I think frequentist is pretty intuitive)<font size="1">. </font>

<font size="1">A story goes with this post, that Bob won 20 times out of total 30 rounds with Alice in a children card game, “War”. War itself is a totally random game, so everyone is supposed to have 50% chance to win in a fair game. Since Bob won 20 out of 30, the question raised: is he cheating?</font>

<font size="1">To answer this question, just follow the </font><a href="http://www.jiangtanghu.com/blog/2012/09/16/hypothesis-testing/" target="_blank"><font size="1">Dragon’s Teeth and Fleas logic of hypothesis testing</font></a><font size="1">:</font>

  * <font size="1">First, assume they are dragon’s teeth; in this case, we assume it is a fair game that everyone has probability of 0.5 to win. </font>
  * <font size="1">Under this assumption, we know the the number of winning follows </font><a href="http://en.wikipedia.org/wiki/Binomial_distribution" target="_blank"><font size="1">binomial distribution</font></a> <font size="1">with probability of 0.5. Now we should check Bob’s 20 winning in 30 in this distribution: is this output extreme, or is it a flea? </font>
  * <font size="1">We then get the p-Value calculated by P(X>=20) which means the chance of winning 20 times and more in 30 games (as extreme or even more extreme ), is 0.0494. Here we only think about winning, so it is a one-sided test. Since this p-Value is less than the default </font>[<font size="1">significance level</font>](http://en.wikipedia.org/wiki/Statistical_significance) <font size="1">of 0.05 (IT IS A FLEA!), we reject the null and think this is more likely not a fair game (Bob is cheating in this statistical point of view). </font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="Bob" border="0" alt="Bob" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/Bob_thumb.png" width="503" height="257" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/Bob.png)

<font size="1">That’s all the story. Then </font><a href="http://www.freakonomics.com/2012/09/20/beware-the-weasel-word-statistical-in-statistical-significance/" target="_blank"><font size="1">this post</font></a> <font size="1">goes, “Although the procedure is mathematically well defined, it is nonsense”. The following is the first reason listed in the post:</font>

> <font size="1">To calculate the probability of Bob’s winning at least 20 games, you use not only the data that you saw (that Bob won 20 games out of 30) but also the imaginary data of Bob winning 21 out of 30 games, or 22 out of 30 games, all the way up to Bob winning all 30 games. The idea of imaginary data is oxymoronic.</font>

<font size="1">In my opinion, the so called “imaginary data” are just the data filling out the binomial distribution (under the assumption of true null hypothesis) we got before and they are not oxymoronic at all (<em>sorry I use “data” as plural</em>).&#160; </font>

<font size="1">What do you think? I can’t go far away from here due to my limit knowledge of Bayesian.</font>

<font size="1">&#8212;&#8212;&#8212;&#8212;-appendix: SAS Codes and Outputs&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;</font>

> <font size="1" face="Courier New">data a; <br />&#160;&#160;&#160; input output count; <br />datalines; <br />0 20 <br />1 10 <br />;</font>
> 
> <font size="1" face="Courier New">proc freq data=a; <br />&#160;&#160;&#160; tables output /binomialc (p=0.5) alpha=0.05; <br />&#160;&#160;&#160; exact binomial; <br />&#160;&#160;&#160; weight count; <br />run;</font>

[<img style="background-image: none; border-bottom: 0px; border-left: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top: 0px; border-right: 0px; padding-top: 0px" title="Bob_SAS" border="0" alt="Bob_SAS" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/Bob_SAS_thumb.png" width="325" height="314" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/Bob_SAS.png)