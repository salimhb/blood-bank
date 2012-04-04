---
title: ! 'deliciousLOG - a tumble log from your delicious.com stream '
slug: deliciouslog-a-tumble-log-from-your-deliciouscom-stream
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 43
wordpress_url: http://blog.railslove.com/?p=43
published_at: 2008-10-09 00:37:51.000000000 +02:00
categories:
- app-a-day
tags:
  keyword:
  - appaday
  - delicious
  - tumble
  - embedit
---
We just deployed a nice simple <a href="http://deliciouslog.com">web app called <strong>deliciousLog</strong>.</a> It turns your <a href="http://delicious.com">delicious</a> bookmarks into a nice colorful tumblelog. What you tag on delicious gets automatically posted on your <span style="text-decoration: line-through;">tumble</span> deliciousLog. The cool thing is, that it not only shows the links but the content. So if you bookmark a clip on youtube the movie will be displayed. If you tag a product on amazon the image will be displayed.

This currently works with:
<ul>
	<li> Flickr</li>
	<li> Quik</li>
	<li> Viddler</li>
	<li> YouTube</li>
	<li> OVI</li>
	<li> Google Video</li>
	<li> Sevenload Video</li>
	<li> .[jpg|gif|png] URL</li>
	<li> Twitter (twictur.es)</li>
	<li> Amazon product</li>
	<li> Slideshare</li>
	<li>and more to come</li>
</ul>
So head over and create your <strong><a href="http://deliciouslog.com">deliciousLog</a>. </strong>

This is mine: <a href="http://deliciouslog.com/derbumi">deliciousLog.com/derbumi</a> - seems like I haven't been very active on delicious lately. :D

We've developed <a href="http://deliciouslog.com">deliciousLog</a> in about two hours and it is a demonstration of <a href="http://redwriteshere.com/">Red's</a> awesome <a href="http://github.com/bumi/embedit">embedit gem</a>.
The app will be OpenSource and published on <a href="http://github.com">github</a>.

<strong>Update:</strong>

<strong>API: </strong>I've forgot to mention that deliciousLog has an API. So you can get your stream as RSS, XML and JSON.
the URL is: deliciouslog.com/{username}.[xml | js | rss]
