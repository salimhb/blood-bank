---
title: git Push (it) origin master
slug: git-push-it-origin-master
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
wordpress_id: 51
wordpress_url: http://blog.railslove.com/?p=51
published_at: 2008-10-28 16:31:06.000000000 +01:00
categories:
- railslove
---
We all love git!
And we all love to push our lovely code into a git repository. But the git push-command is more pleasant if your run it with this alias:
<pre code="ruby">
<del datetime="2008-10-29T13:35:16+00:00">alias gitpush=\ 
'/Applications/Firefox.app/Contents/MacOS/firefox \
http://www.youtube.com/watch?v=BCV5yGKWjv4; \
git push origin master'</del>
</pre>
<strong>Update:</strong> <a href="http://sebastiankippe.de/">Sebastian</a> gives me the hint, to open this <a href="http://www.youtube.com/watch?v=BCV5yGKWjv4">youtube-Movie</a> with the <code>open</code> command:

<pre code="ruby">
alias gitpush=\ 
'open http://www.youtube.com/watch?v=BCV5yGKWjv4; \
git push origin master'
</pre>

