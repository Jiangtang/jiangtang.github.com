---
id: 782
title: Hello Groovy in SAS 9.3
date: 2012-10-28T23:07:12+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=782
permalink: /2012/10/28/hello-groovy-in-sas-9-3/
categories:
  - SAS
tags:
  - Groovy
  - JAVA
  - JSON
  - SAS
---
<font size="1"></font>

<font size="1"><a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/groovy-logo-medium.png"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="groovy-logo-medium" border="0" alt="groovy-logo-medium" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/groovy-logo-medium_thumb.png" width="240" height="120" /></a></font>

> <font size="1">see, it&#8217;s hip to be square <br />&#8216;cuz SAS has a new <a href="http://support.sas.com/documentation/cdl/en/proc/65145/HTML/default/viewer.htm#p1x8agymll9gten1ocziihptcjzj.htm" target="_blank">PROC that&#8217;s GROOVY</a> <br />-Chris Hemedinger, <em><a href="http://blogs.sas.com/content/sasdummy/2011/10/21/poetry-on-our-own-terms/" target="_blank">Poetry on our own terms</a></em>&#160;&#160;&#160; </font>

<font size="1">These days I played <a href="http://support.sas.com/documentation/cdl/en/proc/65145/HTML/default/viewer.htm#p1x8agymll9gten1ocziihptcjzj.htm" target="_blank">Proc Groovy</a> (new in SAS 9.3) for a while because <a href="http://groovy.codehaus.org/" target="_blank">Groovy</a> natively supports <a href="http://www.json.org/" target="_blank">JSON</a> (JavaScript Object Notation) data format. <font size="1">I downloaded much JSON data in the past few weeks(</font><font size="1"><a href="http://www.githubarchive.org/" target="_blank">Github</a> archive for example). </font></font>

> <font size="1"><em>&#8212;&#8212;&#8211;I&#8217;m a line separator &#8212;&#8212;&#8212;</em></font>
> 
> _<font size="1">DO wish SAS can also support JSON in the following release, in a way similar to the existing XML Libname engine, ODS XML markup and SAS XML Mapper!</font>_
> 
> _<font size="1">UPDATE 20121030: I submitted a ticket on <a href="https://communities.sas.com/community/support-communities/ballot" target="_blank">SASware Ballot</a> on this idea and get a feedback that SAS will support JSON since 9.4, both reading and writing. That’s cool.</font>_
> 
> <font size="1"><em>&#8212;&#8212;&#8211;I&#8217;m a line separator end&#8212;&#8212;&#8212;</em></font>

<font size="1"><a href="http://en.wikipedia.org/wiki/Groovy_(programming_language)" target="_blank">Groovy</a> is a dynamic language running in a JVM (Java Virtual Machine) and looks like a lightweight version of JAVA. Don’t know why Groovy was chosen but it is nice to have (at least <em>to parse JSON data</em>) and it’s in Base SAS!</font>

# <font style="font-weight: bold">Set UP</font>

<font size="1">Back to Proc Groovy. To make it work, you should first set a JDK(Java Development Kit; or at least a JVM, also called JRE, Java Runtime Environment) and install Groovy. I test in a Windows 7 machine with SAS 9.3:</font>

  * <font size="1">Install a JDK (<em>or JVM</em>). Get a proper version for your machine. I have a <a href="http://www.oracle.com/technetwork/java/javase/downloads/index.html" target="_blank">JDK7</a> installed in <em>C:Program FilesJavajdk1.7.0_09</em>. By the way, if your SAS 9.3 works well in a64 bit of Windows 7, there must be one JRE in <em>C:Program Files (x86)Javajre1.6.0_24</em>. </font>
  * <div align="left">
      <font size="1">Set up the windows environment variable for JRE. First, create a system variable <em><strong>JAVA_HOME</strong></em> with value of <em><strong>C:Program FilesJavajdk1.7.0_09</strong></em>, then put <em><strong>%JAVA_HOME%bin</strong></em> to the existing system variable <strong><em>Path</em></strong>. If you use a JVM, replace the value of JAVA_HOME as <strong>C:Program FilesJavajre7 </strong>or other proper directory.</font>
    </div>

  * <div align="left">
      <font size="1">Install <a href="http://groovy.codehaus.org/Download" target="_blank">Groovy</a> using the latest version (current v2.05). Accept all the default settings and it will set the environment variable for Groovy. You will have the Groovy installed in <em>C:Program Files (x86)GroovyGroovy-2.0.5</em>.</font>
    </div>

  * <div align="left">
      <font size="1">Locate the <em><strong>sasv9.cfg</strong></em> file in <em>C:Program FilesSASHomeSASFoundation9.3nlsen</em>, find option <em><strong>–JREOPTIONS</strong></em> and add a line inside</font>
    </div>

> <p align="left">
>   <font size="1">-Dtkj.app.class.path=C:Program Files (x86)GroovyGroovy-2.0.5embeddablegroovy-all-2.0.5.jar</font>
> </p>

<p align="left">
  <font size="1">That’s it.</font>
</p>

<h1 align="left">
  <font style="font-weight: bold">Hello World in Proc Groovy</font>
</h1>

> <font size="1" face="Courier New">proc groovy; <br />&#160;&#160;&#160; submit; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; def name=&#8217;World&#8217;; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; println "Hello $name!" <br />&#160;&#160;&#160; endsubmit; <br />quit;</font>

# <font style="font-weight: bold">Read JSON data</font>

Use a simple example from _<a href="http://en.wikipedia.org/wiki/JSON" target="_blank">JSON in wikipedia</a> (save it to a file, test.json)_:

> <pre><font size="1">{
    "firstName": "John",
    "lastName": "Smith",
    "age": 25,
    "address": {
        "streetAddress": "21 2nd Street",
        "city": "New York",
        "state": "NY",
        "postalCode": "10021"
    },
    "phoneNumber": [
        {
            "type": "home",
            "number": "212 555-1234"
        },
        {
            "type": "fax",
            "number": "646 555-4567"
        }
    ]
}</font></pre>

<pre><font size="1" face="Verdana">The following codes simple demonstrate how to:</font></pre>

  * <font size="1">read JSON file</font> 
  * <font size="1">print JSON file</font> 
  * <font size="1">extract JSON values</font> 
  * <font size="1">output values into SAS macro variables</font> 

options nosource;

<font face="Courier New">proc groovy;<br /> <br />&#160;&#160;&#160; submit; </p> 

<p>
  &#160;&#160;&#160;&#160;&#160;&#160;&#160; import groovy.json.*</font>
</p>

<p>
  <font face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; def input=new File(&#8216;a:testtest.json&#8217;).text<br /> <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; def output = new JsonSlurper().parseText(input)</font>
</p>

<p>
  <font face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; println output&#160;&#160;&#160; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; println "" </p> 
  
  <p>
    &#160;&#160;&#160;&#160;&#160;&#160;&#160; output.each {println it}&#160;&#160; </font>
  </p>
  
  <p>
    <font face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; println ""</font>
  </p>
  
  <p>
    <font face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; println output.address.streetAddress<br /> <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; println "Street Address: $output.address.streetAddress" </p> 
    
    <p>
      &#160;&#160;&#160;&#160;&#160;&#160;&#160; println output.address["streetAddress"]&#160;&#160;&#160;&#160;&#160;&#160;&#160; </font>
    </p>
    
    <p>
      <br /><font face="Courier New">&#160;&#160;&#160;&#160;&#160;&#160;&#160; exports = [fName1:output[&#8216;firstName&#8217;]]&#160;&#160;&#160; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; exports.put(&#8216;fName2&#8217;, output[&#8216;firstName&#8217;])&#160; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160;&#160; <br />&#160;&#160;&#160;&#160;&#160;&#160;&#160; endsubmit; </p> 
      
      <p>
        quit;</font>
      </p>
      
      <p>
        <font face="Courier New">%put fName1: &fName1;<br /> <br />%put fName2: &fName2;</font>
      </p>
      
      <pre><font size="1" face="Verdana">The output in LOG window:</font></pre>
      
      <pre><a href="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/JsoninSAS_Groovy.png"><img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="JsoninSAS_Groovy" border="0" alt="JsoninSAS_Groovy" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/10/JsoninSAS_Groovy_thumb.png" width="515" height="308" /></a></pre>
      
      <p align="left">
        <font size="1"></font>
      </p>
      
      <p>
        Happy Groovying!
      </p>
      
      <h1>
        <font style="font-weight: bold">References</font>
      </h1>
      
      <p>
        <a href="http://blog.willmakeaplan.com/?p=18" target="_blank"><font size="1"><em>Parse JSON in SAS with Groovy – part 2</em></font></a><em>&#160;</em><font size="1">by Simon Dawson</font>
      </p>
      
      <p>
        <a href="http://groovy.codehaus.org/Documentation"><font size="1">http://groovy.codehaus.org/Documentation</font></a>
      </p>
      
      <p>
        <a href="http://support.sas.com/documentation/cdl/en/proc/65145/HTML/default/viewer.htm#p1x8agymll9gten1ocziihptcjzj.htm" target="_blank"><font size="1"><em>Overview: GROOVY Procedure</em></font></a><em>&#160;</em><font size="1">in support.sas.com</font>
      </p>