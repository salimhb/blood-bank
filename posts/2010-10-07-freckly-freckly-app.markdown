---
title: Freckly + Freckly App
slug: freckly-freckly-app
author: red_davis
published: true
author_name: reddavis
author_email: reddavis@gmail.com
author_url: http://redwriteshere.com/
wordpress_id: 690
wordpress_url: http://blog.railslove.com/?p=690
published_at: 2010-10-07 19:51:46.000000000 +02:00
categories:
- railslove
- cool-stuff-on-github
- ruby
- oss
tags:
  keyword:
  - freckle
  - pivotal-tracker
  - oss
---
At Railslove we use Freckle and Pivotal Tracker for our client projects.

We wanted a super simple dashboard that just showed us a list of our Pivotal projects and the total number of hours we've worked on that project.

You can find the project over <a href="http://github.com/railslove/Freckly-App">here</a>.

I will eventually get round to writing some decent documentation for it, but to <em>roughly</em> get started:

<script src="http://gist.github.com/615328.js?file=gistfile1.txt"></script>

As an added bonus, I didn't like any of the existing Ruby library so we bundled the code we were using and <a href="http://github.com/railslove/Freckly">released it as a gem</a>. It currently only two of the API calls, mainly because that is all we needed. I do plan on extending the gem to cover the whole API.

Heres a quick run through

<script src="http://gist.github.com/615309.js?file=gistfile1.txt"></script>

<script src="http://gist.github.com/615312.js?file=gistfile1.rb"></script>
