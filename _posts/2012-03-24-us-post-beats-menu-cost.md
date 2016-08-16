---
id: 572
title: US Post Beats Menu Cost
date: 2012-03-24T01:29:47+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=572
permalink: /2012/03/24/us-post-beats-menu-cost/
categories:
  - misc
  - SAS
  - statistics
tags:
  - CPI
  - economics
  - Inflation
  - mail stamp
  - menu cost
  - SAS
---
<font size="1"></font>

<table border="0" cellspacing="0" cellpadding="2" width="400">
  <tr>
    <td valign="top" width="200">
      <p>
        <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/stamp_5c.jpg"><img style="background-image: none; border-right-width: 0px; margin: 3px 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="stamp_5c" border="0" alt="stamp_5c" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/stamp_5c_thumb.jpg" width="196" height="235" /></a>
      </p>
    </td>
    
    <td valign="top" width="200">
      <p>
        <a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/stamp2011.jpg"><img style="background-image: none; border-right-width: 0px; margin: 3px 0px 5px; padding-left: 0px; padding-right: 0px; display: inline; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="stamp2011" border="0" alt="stamp2011" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/stamp2011_thumb.jpg" width="201" height="236" /></a>
      </p>
    </td>
  </tr>
</table>

<font size="1">One of the interesting observations in my first few months in US: there is no price printed in the new mail stamps!</font>

<font size="1">It is interesting because as a former student of economics, I think US Post system did a nice attempt to beat the so called “<a href="http://en.wikipedia.org/wiki/Menu_cost" target="_blank">menu cost</a>” which should honor to Harvard economist <a href="http://en.wikipedia.org/wiki/N._Gregory_Mankiw" target="_blank">Mankiw</a>. Literally the menu cost is the cost of a restaurant to print new menus due to price adjustment. In this story, it is the cost of US Post to print new stamps with adjusted price.</font>

[<img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="US_CPI" border="0" alt="US_CPI" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/US_CPI_thumb.png" width="459" height="360" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/US_CPI.png)

<font size="1">Why US Post need to print new stamps with new price? It is because of the inflation! I took a quick search, the first class postage rate was 5 cents in 1963 and never changed until 1968. But during this 5 years, the CPI (<a href="http://en.wikipedia.org/wiki/Consumer_price_index" target="_blank">consumer price index</a>, one of the robust measures of inflation; data see <a href="http://www.johnstonsarchive.net/other/postage.html" target="_blank">here</a>, codes see below) increased from 30.6 to 33.4, which means, the actual price (see <font color="#ff0000">red</font> line below) of a postage in 1967 was even less than in 1963! </font>

[<img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="US_Postage_Rates" border="0" alt="US_Postage_Rates" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/US_Postage_Rates_thumb.png" width="484" height="384" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/03/US_Postage_Rates.png)

<font size="1">Why US Post didn’t adjust the postage rate accordingly in these years? In a free market, prices are supposed to be adjusted immediately upon market demands and supplies. <a href="http://en.wikipedia.org/wiki/New_Keynesian_economics" target="_blank">A school of economics</a> argues that even in free markets, the prices can be sticky. One of causes of such price stickiness is the menu cost. In this case, US Post knew that the actual cost of posting a mail was up, but it still didn’t will to print new stamps with new price due to printing cost itself (suppose there were lots of stocks) and even the cost to inform people(and such small costs).</font>

<font size="1">Now US Post doesn’t want to lose money by supplying mail services with a price under market value while also want to avoid so called menu cost, then a stamp without price printed seems good enough to solve such dilemma!</font>

<font size="1">/*&#8212;&#8212;&#8212;&#8211;codes for graphics go here and it’s nice to post the first SGPLOT in this blog while watching NCAA game of NCSU vs Kansas&#8212;&#8212;&#8212;&#8212;&#8211;*/</font>

> <font face="Courier New">data rate; <br />&#160;&#160;&#160; input Year Nominal Real CPI; <br />datalines; <br />1866&#160;&#160;&#160; 3&#160;&#160;&#160; 44.0&#160;&#160;&#160; 15.4 <br />1867&#160;&#160;&#160; 3&#160;&#160;&#160; 47.4&#160;&#160;&#160; 14.3 <br />1868&#160;&#160;&#160; 3&#160;&#160;&#160; 49.1&#160;&#160;&#160; 13.8 <br /><em>(data see </em><a href="http://www.johnstonsarchive.net/other/postage.html" target="_blank"><em>here</em></a><em>)</em> <br />;</font>
> 
> <font face="Courier New">proc means data=rate; <br />&#160;&#160;&#160; var Nominal Real CPI; <br />run;</font>
> 
> <font face="Courier New">proc sgplot data=rate; <br />&#160;&#160;&#160; title "History of United States CPI"; <br />&#160;&#160;&#160; series x=year y=cpi; <br />&#160;&#160;&#160; xaxis values= (1870 to 2010 by 10); <br />&#160;&#160;&#160; refline 100 / transparency = 0.5; <br />run;</font>
> 
> <font face="Courier New">proc sgplot data=rate; <br />&#160;&#160;&#160; title &#8216;History of United States Postage Rates&#8217;; <br />&#160;&#160;&#160; series x=Year y=Nominal; <br />&#160;&#160;&#160; series x=Year y=Real; <br />&#160;&#160;&#160; xaxis values= (1870 to 2010 by 10); <br />&#160;&#160;&#160; yaxis label=&#8217;Rates&#8217;; <br />&#160;&#160;&#160; refline 10 44 / transparency = 0.5&#160; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; label = (&#8216;Nominal (Mean)&#8217; &#8216;Real (Mean)&#8217;); <br />run;</font>

<font size="1">&#160;</font>