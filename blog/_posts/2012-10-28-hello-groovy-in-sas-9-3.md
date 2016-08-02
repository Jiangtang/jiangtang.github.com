---
author: Jiangtang Hu
title: Hello Groovy in SAS 9.3
excerpt:
layout: post
category:
  - SAS
tags:
  - Groovy
  - JAVA
  - JSON
  - SAS
post_format: [ ]
---
[![groovy-logo-medium][2]][2]

> see, it’s hip to be square   
> ‘cuz SAS has a new [PROC that’s GROOVY][2]   
> -Chris Hemedinger, *[Poetry on our own terms][3]*    

These days I played [Proc Groovy][2] (new in SAS 9.3) for a while because [Groovy][4] natively supports [JSON][5] (JavaScript Object Notation) data format. I downloaded much JSON data in the past few weeks([Github][6] archive for example). 

> *——–I’m a line separator ———*
> 
> *DO wish SAS can also support JSON in the following release, in a way similar to the existing XML Libname engine, ODS XML markup and SAS XML Mapper!*
> 
> *UPDATE 20121030: I submitted a ticket on [SASware Ballot][7] on this idea and get a feedback that SAS will support JSON since 9.4, both reading and writing. That’s cool.*
> 
> *——–I’m a line separator end———*

[Groovy][8] is a dynamic language running in a JVM (Java Virtual Machine) and looks like a lightweight version of JAVA. Don’t know why Groovy was chosen but it is nice to have (at least *to parse JSON data*) and it’s in Base SAS!

# Set UP

Back to Proc Groovy. To make it work, you should first set a JDK(Java Development Kit; or at least a JVM, also called JRE, Java Runtime Environment) and install Groovy. I test in a Windows 7 machine with SAS 9.3:

*   Install a JDK (*or JVM*). Get a proper version for your machine. I have a [JDK7][9] installed in *C:Program FilesJavajdk1.7.0_09*. By the way, if your SAS 9.3 works well in a64 bit of Windows 7, there must be one JRE in *C:Program Files (x86)Javajre1.6.0_24*. 
*   Set up the windows environment variable for JRE. First, create a system variable ***JAVA_HOME*** with value of ***C:Program FilesJavajdk1.7.0_09***, then put ***%JAVA_HOME%bin*** to the existing system variable ***Path***. If you use a JVM, replace the value of JAVA_HOME as **C:Program FilesJavajre7 **or other proper directory.

*   Install [Groovy][10] using the latest version (current v2.05). Accept all the default settings and it will set the environment variable for Groovy. You will have the Groovy installed in *C:Program Files (x86)GroovyGroovy-2.0.5*.

*   Locate the ***sasv9.cfg*** file in *C:Program FilesSASHomeSASFoundation9.3nlsen*, find option ***–JREOPTIONS*** and add a line inside

> -Dtkj.app.class.path=C:Program Files (x86)GroovyGroovy-2.0.5embeddablegroovy-all-2.0.5.jar

That’s it.

# Hello World in Proc Groovy

> proc groovy;   
>     submit;   
>         def name=’World’;   
>         println "Hello $name!"   
>     endsubmit;   
> quit;

# Read JSON data

Use a simple example from *[JSON in wikipedia][11] (save it to a file, test.json)*:

>     {
>         "firstName": "John",
>         "lastName": "Smith",
>         "age": 25,
>         "address": {
>             "streetAddress": "21 2nd Street",
>             "city": "New York",
>             "state": "NY",
>             "postalCode": "10021"
>         },
>         "phoneNumber": [
>             {
>                 "type": "home",
>                 "number": "212 555-1234"
>             },
>             {
>                 "type": "fax",
>                 "number": "646 555-4567"
>             }
>         ]
>     }

    The following codes simple demonstrate how to:

*   read JSON file 
*   print JSON file 
*   extract JSON values 
*   output values into SAS macro variables 

options nosource;

proc groovy;  
  
    submit; </p> 
        import groovy.json.*</font>

        def input=new File(‘a:testtest.json’).text  
  
        def output = new JsonSlurper().parseText(input)

        println output      
        println "" </p> 
        output.each {println it}   </font>

        println ""

        println output.address.streetAddress  
  
        println "Street Address: $output.address.streetAddress" </p> 
        println output.address["streetAddress"]        </font>

  
        exports = [fName1:output['firstName']]      
        exports.put(‘fName2′, output['firstName'])    
           
        endsubmit; </p> 
quit;</font>

%put fName1: &fName1;  
  
%put fName2: &fName2;

    The output in LOG window:

    [![JsoninSAS_Groovy][13]][13]



Happy Groovying!

# References

[*Parse JSON in SAS with Groovy – part 2*][13]* *by Simon Dawson

<http://groovy.codehaus.org/Documentation>

[*Overview: GROOVY Procedure*][2]* *in support.sas.com

 []: http://dl.dropbox.com/u/69732603/groovy-logo-medium.png
 [2]: http://support.sas.com/documentation/cdl/en/proc/65145/HTML/default/viewer.htm#p1x8agymll9gten1ocziihptcjzj.htm
 [3]: http://blogs.sas.com/content/sasdummy/2011/10/21/poetry-on-our-own-terms/
 [4]: http://groovy.codehaus.org/
 [5]: http://www.json.org/
 [6]: http://www.githubarchive.org/
 [7]: https://communities.sas.com/community/support-communities/ballot
 [8]: http://en.wikipedia.org/wiki/Groovy_(programming_language)
 [9]: http://www.oracle.com/technetwork/java/javase/downloads/index.html
 [10]: http://groovy.codehaus.org/Download
 [11]: http://en.wikipedia.org/wiki/JSON
 []: http://dl.dropbox.com/u/69732603/JsoninSAS_Groovy.png
 [13]: http://blog.willmakeaplan.com/?p=18