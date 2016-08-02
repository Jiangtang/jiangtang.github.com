---
id: 794
title: WordPress and Black Friday
date: 2012-11-23T23:04:03+00:00
author: Jiangtang Hu
layout: post
guid: http://www.jiangtanghu.com/blog/?p=794
permalink: /2012/11/23/wordpress-and-black-friday/
categories:
  - Computer
tags:
  - Black Friday
  - Blog
  - GIThub
  - jekyll
  - PHP
  - WordPress
---
<font size="1">Yes it’s BLACK that today this WordPress based blog was down for a while with a 500 error:</font>

> <font size="1">The website encountered an error while retrieving </font>[<font size="1">http://www.jiangtanghu.com/blog/</font>](http://www.jiangtanghu.com/blog/)<font size="1">. It may be down for maintenance or configured incorrectly.</font>

 <font size="1">I checked web log and it says:</font>

> <font size="1">[24-Nov-2012 02:58:49] PHP Parse error:&#160; syntax error, unexpected T_STRING, expecting &#8216;,&#8217; or &#8216;;&#8217; in ../public_html/jiangtanghu/blog/wp-content/plugins/wp-conditional-captcha/wp-conditional-captcha.php on line 401</font>

<font size="1">So the problem comes from a WordPress plugin “</font><a href="http://wordpress.org/extend/plugins/wp-conditional-captcha/" target="_blank"><font size="1">Conditional CAPTCHA for WordPress</font></a><font size="1">” . The line 401 in <em>wp-conditional-captcha.php</em> is</font>

> <font size="1"><li><input type="radio" name="pass_action" id="pass_action_hold" value="hold" <?php checked( $opts[&#8216;pass_action&#8217;], &#8216;hold&#8217;);?> /> <label for="pass_action_hold"><?php _e(&#8216;Queue the comment for moderation&#8217;, &#8216;wp-conditional-captcha&#8217;);?></label></li></font>

<font size="1">I use WordPress v3.4.2 and “</font><a href="http://wordpress.org/extend/plugins/wp-conditional-captcha/" target="_blank"><font size="1">Conditional CAPTCHA for WordPress</font></a><font size="1">” v3.2.6. I didn’t notice this error before and it may be a compatibility issue (I know 0 about PHP). So my solution: delete the plugin.</font>

<font size="1">Furthermore, I plan to switch to Github+</font><a href="https://github.com/mojombo/jekyll" target="_blank"><font size="1">jekyll</font></a> <font size="1">and get rid of WordPress (sorry, you are wonderful; I&#8217;m just an emotional customer in this crazy Black Friday) .</font>