---
author: Jiangtang Hu
title: >
  Is There Any Better Way? Publishing
  Process For CDISC Standards
  Documentation
excerpt:
layout: post
category:
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
post_format: [ ]
---
#  

# 1. The Pain

I read from Lex Jansen ([@LexJansen][1]) that [CDISC SDTM v1.3 and SDTMIG v3.1.3 were newly released][2]. It’s pretty nice since CDISC SDTM was [supposed to be released semiannually][3] in the new publishing cycle. We can see the team put great efforts on this new version, but frankly speaking, this delivery (the way to display, not the content itself) is far away elegant.

The new SDTM Implementation Guide (IG) v1.3 is just a temporary workaround shipment, as an embedded file “*How to Use SDTMIG 3.1.3*” indicates, 

> SDTMIG 3.1.3 is presented as an annotated version of SDTMIG 3.1.2. This approach was taken for SDTMIG in order for the document to be released quickly without an extensive rewrite. The content presented as annotations will be incorporated into a single version of documentation in a future release.

What does “annotated” mean? When you replace “should” to “must” in the file,

*   strikethrough the word “should” 
*   insert the replacement “must”, and 
*   add a sticky note to indicate the change above 

[![SDTMv313][5]][5]

This is annoying. There are 143 sticky notes throughout the whole documentation, including replacement, deleting, files attachment and such and the reason, is said to ensure “the document to be released quickly without an extensive rewrite”. BUT 143 sticky notes in a PDF file! it’s already huge editing effort ever!

# 2. The Reason (*or The Conjecture*)

Almost everybody complains of Microsoft Office Excel and Word, but Ура(!), they are still dominant in our working spaces (*especially heavy in clinical world? I’m not sure*). I didn’t have any personal connection with CDISC publishing team, but from the documentation released, I’m pretty confident that these files (SDTMIG v3.1.3 and others) were edited in Word and then published into PDF via Adobe products (very common practice, isn’t it?).

Now you may understand why CDISC publishing team delivered this “annotated”  version due to limited time and human resource (although editing 143 sticky notes was also a big work load). The clue is Word! Word! Word! 

Microsoft Word is extremely popular for its WYSIWYG (What You See Is What You Get), but it can’t separate contents from formats and it will a disaster when maintaining a frequent updated Word file by multiple users. In this CDISC SDTMIG case,  there are about 143 content updates supplied by CDISC community worldwide, but when applying such content updates to the original Word file, you are always reasonable to worry about that such updates would change something(*yes SOMETHING*) unexpectedly! The biggest concern for CDISC standard files, I guess, again with confidence, is if such updates destroy the in-text links  or other cross references which offers the nice navigation throughout the documentation.

So, this “annotated” version at least is safe (*and SAFE is much more important than what it looks*): no links proven worktable in v3.1.2 will broken in this time pushing new release, and things would get better in the future (from the same source, “*How to Use SDTMIG 3.1.3*”):

> CDISC is currently discussing how future documentation will be published ensure documentation is easy to navigate and read and at the same time easy to maintain. 

# 3. The Prospective

Yes I will end with a (set of) suggestion(s). The bottom line is no Word anymore and I promise no additional cost and pain compared to digging into Microsoft Word and Adobe Acrobat.

Take SDTM IG v3.1.3 as a demo project:

*   Convert all the contents of SDTM IG v3.1.2 (from PDF, or original Word) to a text based format. Personally I prefer [Markdown][5] and [reStructuredText][6]. Actually it doesn’t matter which one is chosen for test purpose, because such text based formats can be easily transferred (much easier than from Word/PDF). The benefits of these two formats are separation of contents and formats, and very intuitive to learn (much easier than HTML; [almost WYSIWYG][7]). This task is machine doable somehow but also needs manually modification. But all in all,  it is not a big deal, it is only about 300 pages. 
*   Edit these text files according to the new SDTM IG v3.1.3 updates. 
*   Distribute these text files (and rendered output files in PDF/ HTML formats) to a vendor supported or self hosted collaborating site, like [GitHub][8]. 
*   Call for CDISC team members and users to report any issues and even encourage them to directly edit them online (don’t worry, it won’t be mess; we are in a version control system like [GitHub][8]).  
*   Then the next version will come out naturally (and peacefully). 

then I’m looking forward to hearing your ideas.

# 4. Additional Notes

The markup standards mentioned above in my proposal,  [Markdown][5] and [reStructuredText][6], are not replacement for CDISC metadata standard, [ODM][9] and its XML derivatives [Define.xml][10]. Instead, they are better formats to get rid of Microsoft Word for community collaborating of editing the “narrative” parts of models (the PDF files we read from CDISC), for example, SDTMIG we discussed before.

 [1]: https://twitter.com/lexjansen
 [2]: http://www.cdisc.org/sdtm
 [3]: http://www.jiangtanghu.com/blog/2012/03/28/rtp_cdisc_q1/
 []: http://dl.dropbox.com/u/69732603/SDTMv313.png
 [5]: http://daringfireball.net/projects/markdown/
 [6]: http://docutils.sourceforge.net/docs/ref/rst/introduction.html
 [7]: http://docutils.sourceforge.net/docs/user/rst/quickref.html
 [8]: https://github.com/
 [9]: http://www.cdisc.org/odm
 [10]: http://www.cdisc.org/define-xml