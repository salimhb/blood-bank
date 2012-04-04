---
title: ! '[edge Rails] application.rb is now application_controller.rb'
slug: edge-rails-applicationrb-is-now-application_controllerrb
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 56
wordpress_url: http://blog.railslove.com/?p=56
published_at: 2008-11-18 03:58:22.000000000 +01:00
categories:
- railslove
tags:
  keyword:
  - rails
  - edge-rails
---
<p>The file for the ApplicationController is now called /app/controllers/appliction_controller.rb - NO longer /app/controllers/application.rb
</p>
<p>
This is now in edge but I think it will not make it to the 2.2. release. (we will see this in 2.3) <br />
Be careful because this change currently breaks backwards compatibility and you need to rename it on existing projects on your own. 
</p>

