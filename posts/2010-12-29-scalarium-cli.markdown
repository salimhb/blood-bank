---
title: Scalarium CLI
slug: scalarium-cli
author: red_davis
published: true
author_name: reddavis
author_email: reddavis@gmail.com
author_url: http://redwriteshere.com/
wordpress_id: 780
wordpress_url: http://blog.railslove.com/?p=780
published_at: 2010-12-29 19:28:38.000000000 +01:00
categories:
- ruby
- oss
tags:
  keyword:
  - ruby
  - gem
  - scalarium
  - ec2
  - cli
---
<img src="http://blog.railslove.com/wp-content/uploads/2010/12/zeppelin.png" alt="zeppelin" title="zeppelin" width="200" height="100" class="aligncenter size-full wp-image-782" />

We use <a href="http://www.scalarium.com/">Scalarium</a> for a number of client and in house projects. It's awesome; you should check it out if you use, or plan to use Amazons EC2.

However, currently, the only way to deploy your application is to login to the Scalarium website and press the deploy button. This is pretty simple but I miss a CLI.

So let me introduce you to the <a href="https://github.com/railslove/Scalarium-CLI">Scalarium CLI gem</a>.

First things first...Install the gem.

<script src="https://gist.github.com/758779.js?file=gistfile1.txt"></script>

Add scalarium.yml in your config folder. It should look something like:

<script src="https://gist.github.com/758765.js?file=scalarium.yml"></script>

You will find the slug of the application inside the URL:

<img src="https://img.skitch.com/20101229-nygy9t86d85ea8gjw5133kxjbj.jpg" alt="scalarium slug" /><br/><br/>

Then from the Root directory, just run:

<script src="https://gist.github.com/758772.js?file=gistfile1.txt"></script>

Or if you wish to run migrations:

<script src="https://gist.github.com/758774.js?file=gistfile1.txt"></script>

For more information just check out the <a href="https://github.com/railslove/Scalarium-CLI/blob/master/README.md">README</a>.
