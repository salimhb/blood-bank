---
title: ! 'fakebug.js '
slug: fakebugjs
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 58
wordpress_url: http://blog.railslove.com/?p=58
published_at: 2008-11-22 04:03:59.000000000 +01:00
categories:
- railslove
---
<p>So, we all use and love <a href="http://getfirebug.com">Firebug</a>. It makes developing and debugging Web Applications and especially JavaScript so much easier. Most of our JavaScript files contain at some point a <strong>console.log</strong> call.</p>
<p>
The stupid thing is when you forget to remove that debug statement the code breaks on all non-firebug browsers. Everything works fine on your browser but it just breaks on your client's browser without firebug. ;)<br />
To avoid that I've developed <strong>fakebug</strong>: fakebug adds a fake console functions if firebug is not available. 
</p>

<script src="http://gist.github.com/27085.js"></script>
