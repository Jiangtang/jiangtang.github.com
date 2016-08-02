---
author: Jiangtang Hu
title: WordPress and Black Friday
excerpt:
layout: post
category:
  - Computer
tags:
  - Black Friday
  - Blog
  - GIThub
  - jekyll
  - PHP
  - WordPress
post_format: [ ]
---
Yes it’s BLACK that today this WordPress based blog was down for a while with a 500 error:

> The website encountered an error while retrieving <http://www.jiangtanghu.com/blog/>. It may be down for maintenance or configured incorrectly.

 I checked web log and it says:

> [24-Nov-2012 02:58:49] PHP Parse error:  syntax error, unexpected T\_STRING, expecting ‘,’ or ‘;’ in ../public\_html/jiangtanghu/blog/wp-content/plugins/wp-conditional-captcha/wp-conditional-captcha.php on line 401

So the problem comes from a WordPress plugin “[Conditional CAPTCHA for WordPress][1]” . The line 401 in *wp-conditional-captcha.php* is

> <li><input type="radio" name="pass\_action" id="pass\_action\_hold" value="hold" <?php checked( $opts['pass\_action'], ‘hold’);?> /> <label for="pass\_action\_hold"><?php _e(‘Queue the comment for moderation’, ‘wp-conditional-captcha’);?></label></li>

I use WordPress v3.4.2 and “[Conditional CAPTCHA for WordPress][1]” v3.2.6. I didn’t notice this error before and it may be a compatibility issue (I know 0 about PHP). So my solution: delete the plugin.

Furthermore, I plan to switch to Github+[jekyll][2] and get rid of WordPress (sorry, you are wonderful; I’m just an emotional customer in this crazy Black Friday) .

 [1]: http://wordpress.org/extend/plugins/wp-conditional-captcha/
 [2]: https://github.com/mojombo/jekyll