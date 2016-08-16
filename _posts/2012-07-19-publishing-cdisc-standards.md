---
id: 630
title: Is There Any Better Way? Publishing Process For CDISC Standards Documentation
date: 2012-07-19T01:54:10+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=630
permalink: /2012/07/19/publishing-cdisc-standards/
categories:
  - CDISC
  - Industry Review
  - misc
  - SAS
tags:
  - CDISC
  - GIThub
  - Markdown
  - publishing
  - reStructuredText
  - SDTM
---
# &#160;

# <font style="font-weight: bold">1. The Pain</font>

<font size="1">I read from Lex Jansen (</font><a href="https://twitter.com/lexjansen" target="_blank"><font size="1">@LexJansen</font></a><font size="1">) that <a href="http://www.cdisc.org/sdtm" target="_blank">CDISC SDTM v1.3 and SDTMIG v3.1.3 were newly released</a></font><font size="1"></font><font size="1">. It’s pretty nice since CDISC SDTM was <a href="http://www.jiangtanghu.com/blog/2012/03/28/rtp_cdisc_q1/" target="_blank">supposed to be released semiannually</a> in the new publishing cycle. We can see the team put great efforts on this new version, but frankly speaking, this delivery (the way to display, not the content itself) is far away elegant.</font>

<font size="1">The new SDTM Implementation Guide (IG) v1.3 is just a temporary workaround shipment, as an embedded file “<em>How to Use SDTMIG 3.1.3</em>” indicates, </font>

> <font size="1">SDTMIG 3.1.3 is presented as an annotated version of SDTMIG 3.1.2. This approach was taken for SDTMIG in order for the document to be released quickly without an extensive rewrite. The content presented as annotations will be incorporated into a single version of documentation in a future release.</font>

<font size="1">What does “annotated” mean? When you replace “should” to “must” in the file,</font>

  * <font size="1">strikethrough the word “should”</font> 
  * <font size="1">insert the replacement “must”, and</font> 
  * <font size="1">add a sticky note to indicate the change above</font> 

[<img style="background-image: none; border-right-width: 0px; margin: 3px auto 5px; padding-left: 0px; padding-right: 0px; display: block; float: none; border-top-width: 0px; border-bottom-width: 0px; border-left-width: 0px; padding-top: 0px" title="SDTMv313" border="0" alt="SDTMv313" src="http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/SDTMv313_thumb.png" width="471" height="167" />](http://www.jiangtanghu.com/blog/wp-content/uploads/2012/07/SDTMv313.png)

<font size="1">This is annoying. There are 143 sticky notes throughout the whole documentation, including replacement, deleting, files attachment and such and the reason, is said to ensure “the document to be released quickly without an extensive rewrite”. BUT 143 sticky notes in a PDF file! it’s already huge editing effort ever!</font>

# <font style="font-weight: bold">2. The Reason (<em>or The Conjecture</em>)</font>

<font size="1">Almost everybody complains of Microsoft Office Excel and Word, but Ура(!), they are still dominant in our working spaces (<em>especially heavy in clinical world? I’m not sure</em>). I didn’t have any personal connection with CDISC publishing team, but from the documentation released, I’m pretty confident that these files (SDTMIG v3.1.3 and others) were edited in Word and then published into PDF via Adobe products (very common practice, isn’t it?).</font>

<font size="1">Now you may understand why CDISC publishing team delivered this “annotated”&#160; version due to limited time and human resource (although editing 143 sticky notes was also a big work load). The clue is Word! Word! Word! </font>

<font size="1">Microsoft Word is extremely popular for its WYSIWYG (What You See Is What You Get), but it can&#8217;t separate contents from formats and it will a disaster when maintaining a frequent updated Word file by multiple users. In this CDISC SDTMIG case,&#160; there are about 143 <font color="#ff0000">content</font> updates supplied by CDISC community worldwide, but when applying such content updates to the original Word file, you are always reasonable to worry about that such updates would change something(<em>yes SOMETHING</em>) unexpectedly!</font> <font size="1">The biggest concern for CDISC standard files, I guess, again with confidence, is if such updates destroy the in-text links&#160; or other cross references which offers the nice navigation throughout the documentation.</font>

<font size="1">So, this “annotated” version at least is safe (<em>and SAFE is much more important than what it looks</em>): no links proven worktable in v3.1.2 will broken in this time pushing new release, and things would get better in the future (from the same source, “<em>How to Use SDTMIG 3.1.3</em>”):</font>

> <font size="1">CDISC is currently discussing how future documentation will be published ensure documentation is easy to navigate and read and at the same time easy to maintain.</font> 

# 3. The Prospective

<font size="1">Yes I will end with a (set of) suggestion(s). The bottom line is no Word anymore and I promise no additional cost and pain compared to digging into Microsoft Word and Adobe Acrobat.</font>

<font size="1">Take SDTM IG v3.1.3 as a demo project:</font>

  * <font size="1">Convert all the contents of SDTM IG v3.1.2 (from PDF, or original Word) to a text based format. Personally I prefer </font><a href="http://daringfireball.net/projects/markdown/" target="_blank"><font size="1">Markdown</font></a> <font size="1">and <a href="http://docutils.sourceforge.net/docs/ref/rst/introduction.html" target="_blank">reStructuredText</a>. Actually it doesn’t matter which one is chosen for test purpose, because such text based formats can be easily transferred (much easier than from Word/PDF). The benefits of these two formats are separation of contents and formats, and very intuitive to learn (much easier than HTML; <a href="http://docutils.sourceforge.net/docs/user/rst/quickref.html" target="_blank">almost WYSIWYG</a>). This task is machine doable somehow but also needs manually modification. But all in all,&#160; </font><font size="1">it is not a big deal, it is only about 300 pages. </font>
  * <font size="1">Edit these text files according to the new SDTM IG v3.1.3 updates. </font>
  * <font size="1">Distribute these text files (and rendered output files in PDF/ HTML formats) to a vendor supported or self hosted collaborating site, like <a href="https://github.com/" target="_blank">GitHub</a>.</font> 
  * <font size="1">Call for CDISC team members and users to </font><font size="1">report any issues and even encourage them to directly edit them online (don’t worry, it won’t be mess; we are in a version control system like <a href="https://github.com/" target="_blank">GitHub</a>).&#160; </font>
  * <font size="1">Then the next version will come out naturally (and peacefully).</font> 

<font size="1">then I’m looking forward to hearing your ideas.</font>

# 4. Additional Notes

<font size="1">The markup standards mentioned above in my proposal, </font>&#160;<a href="http://daringfireball.net/projects/markdown/" target="_blank"><font size="1">Markdown</font></a> <font size="1">and <a href="http://docutils.sourceforge.net/docs/ref/rst/introduction.html" target="_blank">reStructuredText</a>, are not replacement for CDISC metadata standard, <a href="http://www.cdisc.org/odm" target="_blank">ODM</a> and its XML derivatives <a href="http://www.cdisc.org/define-xml" target="_blank">Define.xml</a>. Instead, they are better formats to get rid of Microsoft Word for community collaborating of editing the “narrative” parts of models (the PDF files we read from CDISC), for example, SDTMIG we discussed before. </font>