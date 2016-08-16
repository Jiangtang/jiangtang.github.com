---
id: 62
title: Options Pricing Using SAS
date: 2009-01-06T16:20:00+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/2009/01/06/options-pricing-using-sas-2/
permalink: /2009/01/06/options-pricing-using-sas-2/
blogger_blog:
  - jiangtanghu.blogspot.com
  - jiangtanghu.blogspot.com
blogger_author:
  - John(Jiangtang) Huhttp://www.blogger.com/profile/04383471478195804254JiangtangHu@gmail.com
  - John(Jiangtang) Huhttp://www.blogger.com/profile/04383471478195804254JiangtangHu@gmail.com
blogger_permalink:
  - /2009/01/options-pricing-using-sas.html
  - /2009/01/options-pricing-using-sas.html
categories:
  - SAS
tags:
  - Black
  - Black-Scholes
  - Call
  - Currency Option
  - Exchange Option
  - Financial Engineering
  - Financial Functions
  - Futures Option
  - Garman-Kohlhagen
  - Margrabe
  - Options
  - Put
  - SAS
  - SAS9.2
  - Stock Option
---
There are some new financial functions in SAS9.2 Base, including 8 options pricing functions(formerly in SAS Risk Dimension). These functions can compute the price of both call and put options on different underlying assets (stock, futures, currency, and exchange asset), using the following models respectively:

>   * <a href="http://en.wikipedia.org/wiki/Black-Scholes" target="_blank"><span style="color: #669966;">Black-Scholes model</span></a>，the traditional stock options pricing model, _see_ <a href="http://riem.swufe.edu.cn/new/techupload/course/200742423245359181.pdf" target="_blank"><span style="color: #669966;">Fischer Black and Myron Scholes (1973)</span></a> ;
> 
>   * <a href="http://en.wikipedia.org/wiki/Black_model" target="_blank"><span style="color: #669966;">Black model</span></a>，extension of Black-Scholes model on futures option (also called Black-76 model)，_see_ <a href="http://math.ucalgary.ca/%7Eware/jc/black76_slides.pdf" target="_blank"><span style="color: #669966;">Fischer Black(1976)</span></a>;
> 
>   * <a href="http://www.riskglossary.com/link/garman_kohlhagen_1983.htm" target="_blank"><span style="color: #669966;">Garman-Kohlhagen model</span></a>，pricing model on foreign currency options，_see_ <a href="http://ideas.repec.org/a/eee/jimfin/v2y1983i3p231-237.html" target="_blank"><span style="color: #669966;">Mark Garman and Steven Kohlhagen(1983)</span></a> ;
> 
>   * <a href="http://www.sitmo.com/eq/671" target="_blank"><span style="color: #669966;">Margrabe model</span></a>，on exchange options，_see_ <a href="http://www.er.ethz.ch/teaching/Margrabe_Option.pdf" target="_blank"><span style="color: #669966;">William Margrabe(1978)</span></a>.

<table border="0" cellspacing="0" cellpadding="2" width="473">
  <tr>
    <td width="137" valign="top">
      Model
    </td>
    
    <td width="103" valign="top">
      Underlying
    </td>
    
    <td width="119" valign="top">
      Call
    </td>
    
    <td width="112" valign="top">
      Put
    </td>
  </tr>
  
  <tr>
    <td width="134" valign="top">
      Black model
    </td>
    
    <td width="104" valign="top">
      Futures
    </td>
    
    <td width="120" valign="top">
      BLACK<span style="color: #ff0000;">CL</span>PRC
    </td>
    
    <td width="112" valign="top">
      BLACK<span style="color: #ff0000;">PT</span>PRC
    </td>
  </tr>
  
  <tr>
    <td width="133" valign="top">
      Black-Scholes model
    </td>
    
    <td width="105" valign="top">
      Stock
    </td>
    
    <td width="121" valign="top">
      BLKSH<span style="color: #ff0000;">CL</span>PRC
    </td>
    
    <td width="112" valign="top">
      BLKSH<span style="color: #ff0000;">PT</span>PRC
    </td>
  </tr>
  
  <tr>
    <td width="132" valign="top">
      Garman-Kohlhagen model
    </td>
    
    <td width="105" valign="top">
      Currency
    </td>
    
    <td width="122" valign="top">
      GARKH<span style="color: #ff0000;">CL</span>PRC
    </td>
    
    <td width="112" valign="top">
      GARKH<span style="color: #ff0000;">PT</span>PRC
    </td>
  </tr>
  
  <tr>
    <td width="133" valign="top">
      Margrabe model
    </td>
    
    <td width="105" valign="top">
      Exchange
    </td>
    
    <td width="122" valign="top">
      MARGR<span style="color: #ff0000;">CL</span>PRC
    </td>
    
    <td width="112" valign="top">
      MARGR<span style="color: #ff0000;">PT</span>PRC
    </td>
  </tr>
</table>

  * BLACKCLPRC: calculates the call price for European options on futures, based on the Black model.

  * BLACKPTPRC: calculates the put price for European options on futures, based on the Black model.

  * BLKSHCLPRT: calculates the call price for European options, based on the Black-Scholes model.

  * BLKSHPTPRT: calculates the put price for European options, based on the Black-Scholes model.

  * GARKHCLPRC: calculates the call price for European options on currencies, based on the Garman-Kohlhagen model.

  * GARKHPTPRC: calculates the put price for European options on currencies, based on the Garman-Kohlhagen model.

  * MARGRCLPRC: calculates the call price for European options on exchange assets, based on the Margrabe model.

  * MARGRPTPRC: calculates the put price for European options on exchange assets, based on the Margrabe model.

For more，see SAS9.2 online help，_Functions and CALL Routines by Category: Financial_：
  
[<span style="color: #669966;">http://support.sas.com/documentation/cdl/en/lrdict/59540/HTML/default/a000245860.htm</span>](http://support.sas.com/documentation/cdl/en/lrdict/59540/HTML/default/a000245860.htm)

Note: A good web site for options pricing with different models, [<span style="color: #669966;">http://www.montegodata.co.uk/</span>](http://www.montegodata.co.uk/ "http://www.montegodata.co.uk/")

 <span style="color: #669966;"></span>

<div id="scid:0767317B-992E-4b12-91E0-4F059A8CECA8:a25c1b69-c356-4773-9162-c96f6558b8e8" class="wlWriterEditableSmartContent" style="margin: 0px; padding: 0px; display: inline;">
  del.icio.us Tags: <a rel="tag" href="http://del.icio.us/popular/SAS"><span style="color: #669966;">SAS</span></a>,<a rel="tag" href="http://del.icio.us/popular/Base"><span style="color: #669966;">Base</span></a>,<a rel="tag" href="http://del.icio.us/popular/ETS"><span style="color: #669966;">ETS</span></a>,<a rel="tag" href="http://del.icio.us/popular/SAS9.2"><span style="color: #669966;">SAS9.2</span></a>,<a rel="tag" href="http://del.icio.us/popular/Financial%20Functions"><span style="color: #669966;">Financial Functions</span></a>,<a rel="tag" href="http://del.icio.us/popular/Options"><span style="color: #669966;">Options</span></a>,<a rel="tag" href="http://del.icio.us/popular/Call"><span style="color: #669966;">Call</span></a>,<a rel="tag" href="http://del.icio.us/popular/Put"><span style="color: #669966;">Put</span></a>,<a rel="tag" href="http://del.icio.us/popular/Pricing"><span style="color: #669966;">Pricing</span></a>,<a rel="tag" href="http://del.icio.us/popular/Black-Scholes%20model"><span style="color: #669966;">Black-Scholes model</span></a>,<a rel="tag" href="http://del.icio.us/popular/Black%20model"><span style="color: #669966;">Black model</span></a>,<a rel="tag" href="http://del.icio.us/popular/Black-76"><span style="color: #669966;">Black-76</span></a>,<a rel="tag" href="http://del.icio.us/popular/Garman-Kohlhagen%20model"><span style="color: #669966;">Garman-Kohlhagen model</span></a>,<a rel="tag" href="http://del.icio.us/popular/Margrabe%20model"><span style="color: #669966;">Margrabe model</span></a>,<a rel="tag" href="http://del.icio.us/popular/Futures%20Option"><span style="color: #669966;">Futures Option</span></a>,<a rel="tag" href="http://del.icio.us/popular/Stock%20Option"><span style="color: #669966;">Stock Option</span></a>,<a rel="tag" href="http://del.icio.us/popular/Currency%20Option"><span style="color: #669966;">Currency Option</span></a>,<a rel="tag" href="http://del.icio.us/popular/Exchange%20Option"><span style="color: #669966;">Exchange Option</span></a>,<a rel="tag" href="http://del.icio.us/popular/Financial%20Engineering"><span style="color: #669966;">Financial Engineering</span></a>
</div>

 <span style="font-family: Arial; font-size: 85%;"></span>