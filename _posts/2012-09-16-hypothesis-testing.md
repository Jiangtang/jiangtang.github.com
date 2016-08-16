---
id: 693
title: 'Statistical Notes (4): Dragon&rsquo;s Teeth and Fleas: Hypothesis Testing in Plain English'
date: 2012-09-16T14:12:07+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=693
permalink: /2012/09/16/hypothesis-testing/
categories:
  - Logic
  - SAS
  - statistics
tags:
  - Hypothesis Testing
  - P-value
  - Proc TTEST
  - SAS
  - statistics
---
> <a href="http://mathbabe.org/2012/07/31/statisticians-arent-the-problem-for-data-science-the-real-problem-is-too-many-posers/" target="_blank"><font size="1">Statisticians aren’t the problem for data science. The real problem is too many posers</font></a> <font size="1">&#8212; Cathy O’Neil</font>
> 
> <a href="http://mathbabe.org/2012/07/31/statisticians-arent-the-problem-for-data-science-the-real-problem-is-too-many-posers/" target="_blank"><font size="1">you actually do need to understand how to invert a matrix at some point in your life if you want to be a data scientist.</font></a> <font size="1">&#8212; Cathy O’Neil</font>

<a href="http://deepbluenine.deviantart.com/art/Red-Dragon-170245865" target="_blank"><font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="Red_Dragon_by_DeepBlueNine" border="0" alt="Red_Dragon_by_DeepBlueNine" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/Red_Dragon_by_DeepBlueNine.jpg" width="404" height="312" /></font></a>

<font size="1">I was asked in several different occasions to explain <a href="http://en.wikipedia.org/wiki/Statistical_hypothesis_testing" target="_blank">hypothesis testing</a> to non-technical people in plain English. Now I think I got a pretty neat one while honors belong to three great Germans, </font><a href="http://en.wikipedia.org/wiki/Friedrich_Engels" target="_blank"><font size="1">Friedrich Engels</font></a><font size="1">, </font><a href="http://en.wikipedia.org/wiki/Karl_Marx" target="_blank"><font size="1">Karl Marx</font></a><font size="1">, and </font><a href="http://en.wikipedia.org/wiki/Heinrich_Heine" target="_blank"><font size="1">Heinrich Heine</font></a><font size="1">. Engels wrote that Marx once quoted a saying from Heine that “I have sown <strong>dragon’s teeth</strong> and harvested <strong>fleas</strong>” (<em>but I didn’t find the original source</em>):</font>

<font color="#ff0000" size="1">In terms of hypothesis testing, say, if you plant <a href="http://en.wikipedia.org/wiki/Dragon's_teeth_(mythology)" target="_blank">dragon’s teeth</a>, you are not supposed to harvest the fleas; but if you do get the fleas, then most likely they are not dragon’s teeth at all!</font>

<font size="1">To make up the story as simple as possible while keep most of the key messages, here take a one-sample <a href="http://en.wikipedia.org/wiki/Student's_t-test" target="_blank">T-test</a> example from </font><a href="http://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/viewer.htm#statug_ttest_examples02.htm" target="_blank"><em><font size="1">SAS TTEST Procedure User Guide</font></em></a><font size="1"><em>,</em> where the investigated data is the Degree of Reading Power (DRP, a measurement of children’s reading skill) from 44 third-grade children. The goal is to test if the mean score of DRP is equal to 30:</font>

> <font size="1" face="Courier New"><a href="http://en.wikipedia.org/wiki/Null_hypothesis" target="_blank">Null&#160;&#160;&#160;&#160;&#160;&#160;&#160; Hypothesis</a> (H0): μ = 30</font>
> 
> <font size="1" face="Courier New"><a href="http://en.wikipedia.org/wiki/Alternative_hypothesis" target="_blank">Alternative Hypothesis</a> (H1): μ ≠ 30</font>

<font size="1"></font>

<font size="1"></font>

<font size="1">For the following discussion, three statistical measures needed (number of cases, mean and standard error):</font>

> <font size="1" face="Courier New">proc means data=read maxdec=4 n mean stderr; <br />&#160;&#160;&#160; var score; <br />&#160;&#160;&#160; freq count; <br />run;</font>

<font size="1">and the output:</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="read" border="0" alt="read" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/read_thumb.png" width="244" height="110" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/read.png)

<font size="1">Here we go:</font>

<font size="1">1. Suppose H0 is true that the mean score is equal to 30 (population mean μ = 30, we assume they are dragon’s teeth!).</font>

<font size="1">2.&#160; We know the sample mean is the best estimate of the population mean, here it is 34.8636.</font>

<font size="1">3. This sample mean is derived from a sample (namely, the 44 children). We’d like to know if this sample (with mean of 34.8636) really come from the population (with mean of 30).</font>

<font size="1">4. To get to know this, we can repeat this survey (or trial, experiment), for example, take another 99 samples (also with 44 children in each sample) and calculate their sample means (we then have 100 different means from the whole 100 samples).</font>

<font size="1">5.&#160; We may know these means (got from such mechanism), with some necessary mathematical transformation,&#160; follow a </font><a href="http://en.wikipedia.org/wiki/Student's_t-distribution" target="_blank"><font size="1">t-distribution</font></a> <font size="1">with degree of freedom of 43 (df = 44 &#8211; 1):</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="test" border="0" alt="test" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/test_thumb.png" width="309" height="60" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/test.png)

<font size="1">The denominator as a whole is the standard error.</font>

<font size="1">6. Now we can check our interested sample (with mean of 34.8636) in this t-distribution. There is a corresponding t-value of this sample in the distribution, (34.8636 &#8211; 30) / 1.6930 =&#160; 2.8728:</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="T_2side" border="0" alt="T_2side" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/T_2side_thumb.png" width="392" height="427" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/T_2side.png)

<font size="1">7. In this distribution, there are only 0.63% (0.0063) of t-values either above 2.8728 or below -2.8728 (symmetry of t-distribution). What does this mean?&#160; Obviously, our interested sample (with mean of 34.8636 and t-value of 2.8728) is not in the mainstream of the whole distribution. We can even think it is&#160; very “extreme”&#160; because, there are only 0.63% of elements in the whole that are more (or at least as equal) extreme than it.</font>

<font size="1">8. We call this number, 0.63% (0.0063) the </font><a href="http://en.wikipedia.org/wiki/P-value" target="_blank"><font size="1">P-value</font></a><font size="1">. According to </font><a href="http://en.wikipedia.org/wiki/P-value" target="_blank"><font size="1">wikipedia</font></a><font size="1">:</font>

> <font size="1">the p-value is the <strong>probability</strong> of obtaining a test statistic at least as <strong>extreme</strong> as the one that was actually observed, <strong>assuming that the null hypothesis is true</strong>.</font>

<font size="1">Here the test statistic that was actually observed is 2.8728, the t-value from our interested sample. And we got from this t-distribution that P{|t|>2.8728} = 0.0063. </font>

<font size="1">9. A question is, how extreme is extreme? We can’t define “extreme” exactly, but <em>probably,</em> we can. The threshold is the </font><a href="http://en.wikipedia.org/wiki/Statistical_significance" target="_blank"><font size="1">significance level</font></a> <font size="1">α (usually 0.05). As a rule of thumb, if p-value is less than the predefine </font><a href="http://en.wikipedia.org/wiki/Statistical_significance" target="_blank"><font size="1">significance level</font></a> <font size="1">α, then&#160; we think the event associated&#160; with this p-value is pretty extreme. </font>

<font size="1">10. Retell our story: first we assume the population mean is 30 just as the null hypothesis claims (<em><font color="#ff0000"><strong>assume they are dragon’s teeth</strong></font></em>), and under this assumption,&#160; we built a t-distribution; we then got that our interested sample is an extreme case (<em><strong><font color="#ff0000">it is a flea!</font></strong></em>). It is so extreme (much less than 0.05) that we can even think about that our assumption (the null hypothesis) is far away from true (<em><strong><font color="#ff0000">most likely they are not dragon’s teeth at all!</font></strong></em>). We reject the null hypothesis and take the alternative that the mean score is different from 30.</font>

<font size="1">11. Formally, it just follows a simple logic (taken from </font><a href="http://www.amazon.com/Statistical-Methods-Clinical-Research-Examples/dp/160764228X/ref=la_B001K8B726_1_1?ie=UTF8&qid=1347463509&sr=1-1" target="_blank"><font size="1">Glenn Walker and Jack Shostak</font></a><font size="1">, P.18): </font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="logic" border="0" alt="logic" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/logic_thumb.png" width="391" height="247" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/logic.png)

<font size="1">In our story, P is the null hypothesis, while Q is the extreme case: if H0 is true, most likely such extreme case should not happen; now we observe the extreme case (a t-value of 2.8728 in a </font><a href="http://en.wikipedia.org/wiki/Student's_t-distribution" target="_blank"><font size="1">t-distribution</font></a> <font size="1">with degree of freedom of 43), then it is reasonable to question the null hypothesis itself.</font>

<font size="1">12. To end this analysis, we can take a look at the output of </font><a href="http://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/viewer.htm#statug_ttest_examples02.htm" target="_blank"><font size="1">SAS PROC TTEST</font></a><font size="1">: </font>

<font size="1"></font>

> <font size="1" face="Courier New">proc ttest data=read h0=30; <br />&#160;&#160; var score; <br />&#160;&#160; freq count; <br />run;</font>

<font size="1">The same result (P-value 0.0063 < 0.05, reject H0):</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="TTEST_read" border="0" alt="TTEST_read" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/TTEST_read_thumb.png" width="487" height="268" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/TTEST_read.png)

# <font style="font-weight: bold">SAS Notes</font>

<font size="1">12. In this </font><a href="http://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/viewer.htm#statug_ttest_examples02.htm" target="_blank"><font size="1">example</font></a><font size="1">, input data take a form of cell count data, not as raw as the case-record data, so in both PROC MEANS and PROC TTEST, a “FREQ” statement added.</font>

<font size="1">13. You can compute this P-value in step-6 with SAS using </font><a href="http://support.sas.com/documentation/cdl/en/lefunctionsref/63354/HTML/default/viewer.htm#n0xy5mce5jgfh3n1wvy919jgm1iv.htm" target="_blank"><font size="1">ProbT</font></a> <font size="1">function:</font>

> <font size="1" face="Courier New">data; <br />&#160;&#160;&#160; t&#160;&#160;&#160; = 2.8727938571; <br />&#160;&#160;&#160; df&#160;&#160; = 43; <br />&#160;&#160;&#160; tail = 2; <br />&#160;&#160;&#160; P&#160;&#160;&#160; = tail*(1-probt(t,df)); <br />&#160;&#160;&#160; put P = ; <br />run;</font>

<font size="1">According to the symmetry of t-distribution, you should multiple 2 to get the two-sided probability:</font>

<font size="1"></font>

<table border="0" cellspacing="0" cellpadding="2" width="400">
  <tr>
    <td valign="top" width="400">
      <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/Left.png"><font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="Left" border="0" alt="Left" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/Left_thumb.png" width="450" height="216" /></font></a>
    </td>
  </tr>
  
  <tr>
    <td valign="top" width="400">
      <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/Right.png"><font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="Right" border="0" alt="Right" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/Right_thumb.png" width="448" height="219" /></font></a>
    </td>
  </tr>
</table>

<font size="1">14. Long long ago, a so called “</font><a href="https://onlinecourses.science.psu.edu/stat501/node/7" target="_blank"><font size="1">critical value</font></a><font size="1">” is calculated to support the decision. That’s the calculation method using </font><a href="http://support.sas.com/documentation/cdl/en/lefunctionsref/63354/HTML/default/viewer.htm#n0yhwu36w3pj41n16j69b3hmzqvc.htm" target="_blank"><font size="1">TINV</font></a> <font size="1">function:</font>

> <font size="1" face="Courier New">data; <br />&#160;&#160;&#160; alpha = 0.05; <br />&#160;&#160;&#160; tail&#160; = 2; <br />&#160;&#160;&#160; df&#160;&#160;&#160; = 43;</font>
> 
> <font size="1" face="Courier New">&#160;&#160;&#160; tCritic = tinv(1-alpha<font color="#ff0000">/</font>tail,df); <br />&#160;&#160;&#160; put tCritic=; <br />run;</font>

<font size="1">We get this critical value of 2.0166921992:</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="critical" border="0" alt="critical" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/critical_thumb.png" width="395" height="417" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/09/critical.png)

<font size="1">These two shaded zones are called “rejection zones”. The rule is, if the t-value we observed lies within the rejection zones, we should then reject the null hypothesis and take the alternative. In step-6, the t-value we calculated is 2.8728, which is bigger than this critical value, so we should reject H0.</font>

<font size="1">Critical value approach is equivalent with the p-value approach we discussed before, but slightly old fashioned. P-value is pretty intuitive and can be also easily calculated by computer. In days when computing power was not wildly available, people just took the t-distribution table to look up the critical values. </font>

<font size="1">Most statistical packages including SAS software don’t report the critical value (but still alive in statistics text books).</font>

# <font style="font-weight: bold">Reference</font>

_<a href="http://support.sas.com/documentation/cdl/en/statug/65328/HTML/default/viewer.htm#statug_ttest_examples02.htm" target="_blank"><font size="1">SAS PROC TTEST USER GUIDE</font></a>_

[_<font size="1">Common Statistical Methods for Clinical Research with SAS Examples</font>_](http://www.amazon.com/Statistical-Methods-Clinical-Research-Examples/dp/160764228X/ref=la_B001K8B726_1_1?ie=UTF8&qid=1347463509&sr=1-1) <font size="1">by Glenn Walker and Jack Shostak</font>

_<a href="http://cos.name/2010/11/hypotheses-testing/" target="_blank"><font size="1">Hypothesis Testing: A Primer</font></a>_ <font size="1">(in Chinese)</font>

<a href="http://onlinestatbook.com/analysis_lab/t_dist.html" target="_blank"><font size="1">Two sides T-distribution calculator</font></a>

<a href="http://www.stat.tamu.edu/~west/applets/tdemo.html" target="_blank"><font size="1">Single side t-distribution calculator</font></a>

<a href="http://www.codecogs.com/latex/eqneditor.php" target="_blank"><font size="1">Online Latex Equation Editor</font></a>