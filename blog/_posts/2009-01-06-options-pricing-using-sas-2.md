---
author: Jiangtang Hu
title: Options Pricing Using SAS
excerpt:
layout: post
category:
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
post_format: [ ]
---
There are some new financial functions in SAS9.2 Base, including 8 options pricing functions(formerly in SAS Risk Dimension). These functions can compute the price of both call and put options on different underlying assets (stock, futures, currency, and exchange asset), using the following models respectively:

> *   [Black-Scholes model][1]，the traditional stock options pricing model, *see* [Fischer Black and Myron Scholes (1973)][2] ;
> 
> 
> <!-- -->
> 
> *   [Black model][3]，extension of Black-Scholes model on futures option (also called Black-76 model)，*see *[Fischer Black(1976)][4];
> 
> 
> <!-- -->
> 
> *   [Garman-Kohlhagen model][5]，pricing model on foreign currency options，*see *[Mark Garman and Steven Kohlhagen(1983)][6] ;
> 
> 
> <!-- -->
> 
> *   [Margrabe model][7]，on exchange options，*see *[William Margrabe(1978)][8].

| Model                  | Underlying | Call       | Put        |
||
| Black model            | Futures    | BLACKCLPRC | BLACKPTPRC |
| Black-Scholes model    | Stock      | BLKSHCLPRC | BLKSHPTPRC |
| Garman-Kohlhagen model | Currency   | GARKHCLPRC | GARKHPTPRC |
| Margrabe model         | Exchange   | MARGRCLPRC | MARGRPTPRC |

*   BLACKCLPRC: calculates the call price for European options on futures, based on the Black model.


<!-- -->

*   BLACKPTPRC: calculates the put price for European options on futures, based on the Black model.


<!-- -->

*   BLKSHCLPRT: calculates the call price for European options, based on the Black-Scholes model.


<!-- -->

*   BLKSHPTPRT: calculates the put price for European options, based on the Black-Scholes model.


<!-- -->

*   GARKHCLPRC: calculates the call price for European options on currencies, based on the Garman-Kohlhagen model.


<!-- -->

*   GARKHPTPRC: calculates the put price for European options on currencies, based on the Garman-Kohlhagen model.


<!-- -->

*   MARGRCLPRC: calculates the call price for European options on exchange assets, based on the Margrabe model.


<!-- -->

*   MARGRPTPRC: calculates the put price for European options on exchange assets, based on the Margrabe model.

For more，see SAS9.2 online help，*Functions and CALL Routines by Category: Financial*：  
<http://support.sas.com/documentation/cdl/en/lrdict/59540/HTML/default/a000245860.htm>

Note: A good web site for options pricing with different models, [http://www.montegodata.co.uk/][9]

 

del.icio.us Tags: [SAS][10],[Base][11],[ETS][12],[SAS9.2][13],[Financial Functions][14],[Options][15],[Call][16],[Put][17],[Pricing][18],[Black-Scholes model][19],[Black model][20],[Black-76][21],[Garman-Kohlhagen model][22],[Margrabe model][23],[Futures Option][24],[Stock Option][25],[Currency Option][26],[Exchange Option][27],[Financial Engineering][28]

 [1]: http://en.wikipedia.org/wiki/Black-Scholes
 [2]: http://riem.swufe.edu.cn/new/techupload/course/200742423245359181.pdf
 [3]: http://en.wikipedia.org/wiki/Black_model
 [4]: http://math.ucalgary.ca/%7Eware/jc/black76_slides.pdf
 [5]: http://www.riskglossary.com/link/garman_kohlhagen_1983.htm
 [6]: http://ideas.repec.org/a/eee/jimfin/v2y1983i3p231-237.html
 [7]: http://www.sitmo.com/eq/671
 [8]: http://www.er.ethz.ch/teaching/Margrabe_Option.pdf
 [9]: http://www.montegodata.co.uk/ "http://www.montegodata.co.uk/"
 [10]: http://del.icio.us/popular/SAS
 [11]: http://del.icio.us/popular/Base
 [12]: http://del.icio.us/popular/ETS
 [13]: http://del.icio.us/popular/SAS9.2
 [14]: http://del.icio.us/popular/Financial%20Functions
 [15]: http://del.icio.us/popular/Options
 [16]: http://del.icio.us/popular/Call
 [17]: http://del.icio.us/popular/Put
 [18]: http://del.icio.us/popular/Pricing
 [19]: http://del.icio.us/popular/Black-Scholes%20model
 [20]: http://del.icio.us/popular/Black%20model
 [21]: http://del.icio.us/popular/Black-76
 [22]: http://del.icio.us/popular/Garman-Kohlhagen%20model
 [23]: http://del.icio.us/popular/Margrabe%20model
 [24]: http://del.icio.us/popular/Futures%20Option
 [25]: http://del.icio.us/popular/Stock%20Option
 [26]: http://del.icio.us/popular/Currency%20Option
 [27]: http://del.icio.us/popular/Exchange%20Option
 [28]: http://del.icio.us/popular/Financial%20Engineering