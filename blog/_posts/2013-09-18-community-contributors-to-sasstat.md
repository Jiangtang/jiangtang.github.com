---
id: 1271
title: Community Contributors to SAS/STAT
date: 2013-09-18T19:24:42+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=1271
permalink: /2013/09/18/community-contributors-to-sasstat/
categories:
  - SAS
  - statistics
tags:
  - SAS
  - statistics
---
> _<font size="1">I suppose it is tempting, if the only tool you have is a hammer, to treat everything as if it were a nail. &#8211; Abraham Maslow, The Psychology of Science, 1966</font>_

<font size="1">Yes it’s true: since I have a pretty rich </font>[<font size="1">collection of SAS list processing macros</font>](https://github.com/Jiangtang/SAS_ListProcessing)<font size="1">, I’d like my list container to hold everything itemized. Here is a nail I found in SAS/STAT online help.</font>

<font size="1">There are strong community contributing to the development of SAS/STAT software. Their names were list in the acknowledgements session of the </font>[<font size="1">SAS/STAT documentation</font>](http://support.sas.com/documentation/cdl/en/statug/66103/HTML/default/viewer.htm#chap0000018_chap0000018_sect006.htm) (some were former SAS employees)<font size="1">:</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="clip_image002" border="0" alt="clip_image002" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/09/clip_image002_thumb.jpg" width="513" height="137" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/09/clip_image002.jpg)

<font size="1">Since the name list was not in tabulate format, it is hardly to read. The following is a hammer’s way to get a table version of all the contributors and their institutions (only very basic list processing tricks used):</font>

  * <font size="1">copy all the free text and assign it into a macro variable </font>
  * <font size="1">count the number of elements in the value list </font>
  * <font size="1">do loop through the list </font>

> <font size="1" face="Courier New">filename list url "</font>[<font size="1" face="Courier New">https://raw.github.com/Jiangtang/SAS_ListProcessing/master/_ListProcessing";</font>](https://raw.github.com/Jiangtang/SAS_ListProcessing/master/_ListProcessing";)        <font size="1"><br /><font face="Courier New">%inc list;</font></font>
> 
> <font size="1" face="Courier New">%let name=%nrstr(Alan Agresti, University of Florida; Paul Allison, University of Pennsylvania; <font color="#ff0000">&#8230;</font> ); <br />%let n= %words(&name, delim=%str(;));</font>
> 
> <font size="1" face="Courier New">%macro doit(delim=%str(;)); <br />data name; <br />&#160;&#160;&#160; length a $100.; <br />&#160;&#160;&#160; %do i=1 %to &n; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; a="%qscan(%SUPERQ(name),&i,&delim)"; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; name=scan(a,1,","); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; institute=substr(a,length(name)+2); <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; output; <br />&#160;&#160;&#160; %end; <br />&#160;&#160;&#160; drop a; <br />run;&#160;&#160;&#160; <br />%mend; <br />%doit;</font>
> 
> <font size="1" face="Courier New">proc print data=name; <br />run;</font>

<font size="1">Then we just get the decent tabulate output (partial):</font>

[<font size="1"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="clip_image003" border="0" alt="clip_image003" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2013/09/clip_image003_thumb.gif" width="406" height="235" /></font>](http://www.jiangtanghu.com/blog/wp-content/uploads/2013/09/clip_image003.gif)

<font size="1">&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-</font>

<font size="1">Shameless Ad: I will have a talk on SAS list processing in the forthcoming </font>[<font size="1">SESUG (Oct 20-23, 2013) at St.Pete Beach, FL</font>](http://www.sesug.org/SESUG2013/index.php)<font size="1">. Welcome to drop by if you are on the spot!</font>

<font size="1">&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;&#8212;-</font>

<font size="1">I do have fun to read this list while I can see some familiar names like Alan Agresti, Paul Allison, Michael Friendly, Wayne Fuller, Frank E. Harrell Jr., Wolfgang M. Hartmann, Ronald W. Helms, Gary Koch, J. Philip Miller and Chris Olinger (#84), who is my current colleague! This finding is a bonus because I know Chris is is purely technical guy. He might be the only non-statistician in the list. I chatted with Chris and he said it’s due to his early contribution on ODS.</font>

<font size="1">The full report if you are interested in:</font>

<table border="1" cellspacing="0" cellpadding="2" width="526">
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">1</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Alan Agresti</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Florida</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">2</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Paul Allison</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Pennsylvania</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">3</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Douglas Bates</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Wisconsin</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">4</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">John Barnard Jr.</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Cleveland Clinic Foundation</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">5</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">David Binder (deceased)</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">formerly of David Binder Research</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">6</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Suzette Blanchard</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Frontier Science Technology Research Foundation</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">7</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Mary Butler Moore</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">formerly of University of Florida at Gainesville</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">8</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Wilbert P. Byrd</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Clemson University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">9</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Vincent Carey</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Harvard University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">10</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Sally Carson</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">RAND</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">11</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Love Casanova</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">CSC-FSG</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">12</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Helene Cavior</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Abacus Concepts</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">13</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Rao Chaganty</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Old Dominion University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">14</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">George Chao</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">DuPont Merek Pharmaceutical Company</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">15</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Colin Chen</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Fannie Mae</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">16</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Daniel M. Chilko</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">West Virginia University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">17</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Marc Cohen</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Fair Isaac Corporation</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">18</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Jan de Leeuw</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of California, Los Angeles</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">19</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Dave DeLong</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Duke University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">20</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Alex Dmitrienko</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Eli Lilly</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">21</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Sandra Donaghy</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">North Carolina State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">22</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">David B. Duncan</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Johns Hopkins University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">23</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Paul Eilers</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Leiden University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">24</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Scott Emerson</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Washington</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">25</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Michael Farrell</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Oak Ridge National Laboratory</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">26</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Stewart Fossceco</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">SLF Consulting</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">27</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Michael Friendly</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">York University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">28</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Rudolf J. Freund</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Texas A&M University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">29</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Wayne Fuller</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Iowa State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">30</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Andrzej Galecki</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Michigan</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">31</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">A. Ronald Gallant</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Duke University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">32</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Joseph Gardiner</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Michigan State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">33</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Charles Gates</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Texas A&M University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">34</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Thomas M. Gerig</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">North Carolina State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">35</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Francis Giesbrecht</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">North Carolina State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">36</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Harvey J. Gold</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">North Carolina State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">37</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Kenneth Goldberg</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Centocor Inc</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">38</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Robert J. Gray</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Harvard University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">39</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Donald Guthrie</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of California, Los Angeles</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">40</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Gerald Hajian</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Schering Plough Research Institute</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">41</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Bob Hamer</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of North Carolina at Chapel Hill</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">42</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Frank E. Harrell Jr.</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Vanderbilt University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">43</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Wolfgang M. Hartmann</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">&#160;</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">44</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Walter Harvey</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Ohio State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">45</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Douglas Hawkins</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Minnesota</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">46</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Xuming He</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Illinois at Urbana-Champaign</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">47</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Ronald W. Helms</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Rho, Inc.</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">48</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Joseph Hilbe</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Arizona State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">49</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Gerry Hobbs</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">West Virginia University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">50</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Ronald R. Hocking</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Texas A & M University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">51</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Nick Horton</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Smith College</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">52</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Julian Horwich</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Camp Conference Company</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">53</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Jason C. Hsu</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Ohio State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">54</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">David Hurst</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Alabama at Birmingham</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">55</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Joseph G. Ibrahim</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of North Carolina at Chapel Hill</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">56</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Emilio A. Icaza</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Louisiana State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">57</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Jun Jie</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Purdue University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">58</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Joerg Kaufman</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Bayer Schering Pharma AG</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">59</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">William Kennedy</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Iowa State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">60</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Gary Koch</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of North Carolina at Chapel Hill</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">61</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Roger Koenker</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Illinois at Urbana-Champaign</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">62</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Alexander Kolovos</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">SpaceTimeWorks LLC</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">63</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Kenneth L. Koonce</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Louisiana State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">64</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Rich La Valley</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Strategic Technology Solutions</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">65</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Russell V. Lenth</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Iowa</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">66</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Charles Lin</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">U.S. Census Bureau</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">67</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Danyu Lin</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of North Carolina</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">68</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Ardell C. Linnerud</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">North Carolina State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">69</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Ramon C. Littel</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Florida</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">70</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">George MacKenzie</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Oregon</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">71</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Brian Marx</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Louisiana State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">72</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">J. Jack McArdle</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Southern California</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">73</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Roderick P. McDonald</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Macquarie University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">74</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Alfio Marazzi</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Lausanne</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">75</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">J. Philip Miller</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Washington University Medical School</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">76</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">George Milliken</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Kansas State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">77</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Robert J. Monroe</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">North Carolina State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">78</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Robert D. Morrison</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Oklahoma State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">79</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Keith Muller</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Florida</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">80</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Anupama Narayanan</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Procter & Gamble Co</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">81</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Meltem Narter</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">&#160;</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">82</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Ralph G. O’Brien</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Cleveland Clinic Foundation</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">83</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Kenneth Offord</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Mayo Clinic</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">84</font>
    </th>
    
    <td class="l data" width="174">
      <font color="#ff0000" size="1">Christopher R. Olinger</font>
    </td>
    
    <td class="l data" width="317">
      <font color="#ff0000" size="1">d-Wise Technologies</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">85</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Christopher J. Paciorek</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Harvard University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">86</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Robert Parks</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Washington University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">87</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Richard M. Patterson</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Auburn University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">88</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Virginia Patterson</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Tennessee</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">89</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Cliff Pereira</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Oregon State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">90</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Hans-Peter Piepho</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Universität Hohenheim</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">91</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Edward Pollak</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Iowa State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">92</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Stephen Portnoy</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Illinois</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">93</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">John Preisser</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of North Carolina at Chapel Hill</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">94</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">C. H. Proctor</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">North Carolina State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">95</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Bahjat Qaqish</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of North Carolina at Chapel Hill</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">96</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Dana Quade</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of North Carolina at Chapel Hill</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">97</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Bill Raynor</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Kimberly Clark</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">98</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Georgia Roberts</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Statistics Canada</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">99</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">James Roger</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">GlaxoSmithKline (retired)</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">100</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Peter Rousseeuw</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Antwerp</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">101</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Donald Rubin</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Harvard University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">102</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Joseph L. Schafer</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Pennsylvania State University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">103</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Robert Schechter</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">AstraZeneca</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">104</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Shayle Searle</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Cornell University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">105</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Pat Hermes Smith</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">formerly of Ciba-Geigy</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">106</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Roger Smith</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">formerly of USDA</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">107</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Phil Spector</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of California, Berkeley</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">108</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Michael Speed</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Texas A&M University at College Station</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">109</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">William Stanish</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Statistical Insight</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">110</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Rodney Strand</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Orion Enterprises, LLC</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">111</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Walter Stroup</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Nebraska</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">112</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Robert Teichman</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">ICI Americas Inc.</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">113</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Terry M. Therneau</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Mayo Clinic</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">114</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Edward Vonesh</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Northwestern University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">115</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Grace Wahba</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Wisconsin at Madison</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">116</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Glenn Ware</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Georgia</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">117</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Peter H. Westfall</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Texas Tech University</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">118</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Edward W. Whitehorne</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">CI Partners, LLC</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">119</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">William Wigton</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">USDA</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">120</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">William Wilson</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of North Florida</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">121</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Philip Whittall</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Unilever (retired)</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">122</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Dong Xiang</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">&#160;</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">123</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Victor Yohai</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Buenos Aires</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">124</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Forrest W. Young (deceased)</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">formerly of University of North Carolina at Chapel Hill</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">125</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Ke-Hai Yuan</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of Notre Dame</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">126</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Ruben Zamar</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">University of British Columbia</font>
    </td>
  </tr>
  
  <tr>
    <th class="r rowheader" scope="row">
      <font size="1">127</font>
    </th>
    
    <td class="l data" width="174">
      <font size="1">Scott Zeger</font>
    </td>
    
    <td class="l data" width="317">
      <font size="1">Johns Hopkins University</font>
    </td>
  </tr>
</table>

<font size="1"></font>