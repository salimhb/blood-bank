---
title: Using Scalarium CLI
slug: using-scalarium-cli
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
wordpress_id: 789
wordpress_url: http://blog.railslove.com/?p=789
published_at: 2011-01-13 10:41:57.000000000 +01:00
categories:
- railslove
---
In one of our projects we've used <a href="https://github.com/railslove/Scalarium-CLI">Scalarium CLI gem</a> for an automatic deployment to amazon ec2 servers in combination with our <a href="https://github.com/defunkt/cijoe">CI Server - CIJoe</a>. Its really easy.

The only thing to do is to require the Scalarium CLI and the scalarium.yml in your setup recipe:

<script src="https://gist.github.com/777585.js?file=gistfile1.rb"></script>

<script src="https://gist.github.com/777589.js?file=gistfile1.rb"></script>

Then use your 'build worked' template (e.g.: build_worked.erb) to fire the deployment after your app was successful build:

<script src="https://gist.github.com/777590.js?file=gistfile1.txt"></script>

Thats it!

For more information about Scalarium CLI look at <a href="http://blog.railslove.com/2010/12/29/scalarium-cli/">reds blogpost</a> or on <a href="https://github.com/railslove/Scalarium-CLI">github</a>!
