---
title: Static content in your Rails application
slug: static-content-in-your-rails-application
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 472
wordpress_url: http://blog.railslove.com/?p=472
published_at: 2009-08-13 15:27:15.000000000 +02:00
categories:
- rails
- cool-stuff-on-github
- plugins
- yai7d
tags:
  keyword:
  - static-pages
  - content
---
<p>Our heros over at <a href="http://thoughtbot.com">thoughtbot.com</a> <a href="http://robots.thoughtbot.com/post/160768450/high-voltage">blogged about static pages</a> and their newly released Rails engine <a href="http://github.com/thoughtbot/high_voltage">high_voltage</a>. High Voltage helps you dealing with simple, stupid static content pages that nobody wants but everyone needs. ;) (With static pages I'm thinking of imprint, about us, etc.)</p>
<p>
In our projects we had a similar solution but to edit the pages more easily and without the need to deploy the whole application we're saving the content in the database. 
</p>
<p>
Because the database part was missing in high_voltage but I've really liked the idea to extract that feature into a rails engine I've created a <a href="http://github.com/bumi/high_voltage/tree/master">fork</a> last night.
</p>
<p>
My fork checks if there is a valid template file in views/pages/ - if not it checks the Database and renders the views/pages/show template.<br />
</p>
<h3>How to use it?</h3>

<p>
<strong>Installation</strong><br />
<code lang="bash">
script/plugin install git://github.com/bumi/high_voltage.git
</code>
</p>
<p>
<strong>Create pages</strong><br />
this is up to you. ;) <br />
You can add static files to your app/views/pages/ directory or create a database entry:
<code lang="ruby">
HighVoltage::Page.create(:title => "Hello world", :body => "High Voltage! High Voltage!")
</code>
</p>
<p>
<strong>That's it!</strong>
</p>
<p>
For more information check the <a href="http://robots.thoughtbot.com/post/160768450/high-voltage">original thoughtbot post"</a> - You should follow their blog anyway! - And have a look at the <a href="http://github.com/bumi/high_voltage/tree/master">readme</a>. 
</p>
<p>
Hope you like my addons.<br />
What are your solutions for static pages? 
</p>
