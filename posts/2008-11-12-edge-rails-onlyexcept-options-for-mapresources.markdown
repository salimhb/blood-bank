---
title: ! '[edge Rails] :only/:except options for map.resources '
slug: edge-rails-onlyexcept-options-for-mapresources
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 54
wordpress_url: http://blog.railslove.com/?p=54
published_at: 2008-11-12 18:09:29.000000000 +01:00
categories:
- edge-rails
- rails
tags:
  keyword:
  - edge-rails
  - routes
  - memory
---
Today a nice option for the routes was <a href="http://github.com/rails/rails/commit/44a3009ff068bf080de6764a8c884fbf0ceb920e">commited to the Rails edge</a>.

map.resources now allows the option :only and :except to specify which routes should be created. Both options accept :none, :all, one action name or an array of action names.
For example:
<pre lang="rails">
map.resources :user, :only => :create
# GET /users fails
# only POST /users is available

map.resources :comments, :except => [:update, :destroy]
# GET /comments etc. works
# PUT /comments/1  fails
# DELETE /comments/1 fails
</pre>

If you have a lot of resources in your routes this allows you to cut memory consumption.
