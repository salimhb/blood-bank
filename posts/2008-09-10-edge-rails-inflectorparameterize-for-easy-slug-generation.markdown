---
title: ! '[edge Rails] Inflector.parameterize for easy slug generation'
slug: edge-rails-inflectorparameterize-for-easy-slug-generation
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 36
wordpress_url: http://blog.railslove.com/?p=36
published_at: 2008-09-10 09:57:10.000000000 +02:00
categories:
- edge-rails
- rails
tags:
  keyword:
  - rails
  - edge-rails
  - parameterize
  - niceurls
  - slugs
---
David has just commited an <strong>parameterize</strong> method for easy slug generation. This means it strips out all special characters so that it can be savely used in URLs. It replaces anything but a-z and 0-9 with a "-" (you can pass a custom seperator).
<strong>Example to generate nice URLs for your models:</strong>
<pre lang="ruby">
def to_param
  "#{id}-#{name.parameterize}"
end
</pre>
<pre lang="ruby">
"$%hello I'm a sentence with & a löt òf SPECIAL chars+".parameterize #=> -hello-i-m-a-sentence-with-a-lt-f-special-chars-
</pre>

My <a href="http://github.com/bumi/find_by_param/tree/master">find_by_param</a> plugin, that helps you a lot with working with nice URLs, uses a custom encoding method to do this. Perhaps I will change that some time soon. ;)

<p>
<strong>Update:</strong><br />
The <a href="http://github.com/rails/rails/commit/b8e8be83e952163e225f9b38bd7251cba9c44f38#comments">comments on the commit</a> pointed to two really nice projects:
1. <a href="http://github.com/rsl/stringex/tree/master">stringex</a> - which is a bit of a overkill. *tries to solve everything* but creates really aweseome slugs by translating special chars ($ to dollar, etc.)<br />
2. <a href="http://github.com/henrik/slugalizer/tree/master">slugalizer</a> - a ruby slugalizer which ses ActiveSupport for platform-consistent normalization. It also does nice formatting like: Åh, räksmörgåsar! => ah-raksmorgasar"
</p>
<p>
<strong>Update2 </strong><br />
This feature was <a href="http://github.com/rails/rails/commit/1ddde91303883b47f2215779cf45d7008377bd0d">extended earlier today</a>.  Not nice conversions like Malmö = malmo or Garçons = garcons are supported. 

