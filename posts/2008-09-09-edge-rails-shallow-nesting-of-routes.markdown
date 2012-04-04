---
title: ! '[edge Rails] shallow nesting of routes'
slug: edge-rails-shallow-nesting-of-routes
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 33
wordpress_url: http://blog.railslove.com/?p=33
published_at: 2008-09-09 15:59:13.000000000 +02:00
categories:
- railslove
- edge-rails
- rails
tags:
  keyword:
  - rails
  - edge-rails
  - rubyonrails
  - shallow
---
Ok, finally. This is the first post of a series about some new exciting edge rails features. ;)

Here at Railslove most of our projects are living on the edge (thanks to <a href="http://github.com/evilchelu/braid/tree/master">braid</a>!) ;) and we try to keep close track of what's happening in the <a href="http://github.com/rails/rails/commits/master">rails master branch.</a>

Today I've found a commit that is actually a few days old but this will clean up a lot of my nested routes.

Imagine your application has a User who has_many :posts which again has_many :comments. Your routes would look something like:

<pre lang="rails">
map.resources :users do |user|
  user.resources :posts do |post|
    post.resources :comments
  end
end
</pre>
This defines the following helpers and URLs
<pre>
users_url #=> /users/
user_posts_url #=> /users/1/posts/
user_post_comments_url #=> /users/1/posts/10/comments
</pre>

however only the full nested routes are available.
/posts/10 or /comments/10 are not available and you need to declare those seperately:
<pre lang="rails">
map.resources :posts do |post|
  post.resources :comments
end
map.resources :comments
</pre>

<a href="http://github.com/rails/rails/commit/83c6ba18899a9f797d79726ca0078bdf618ec3d4">This commit</a> now allows you to add a :shallow => true option which does this automatically for you. This is great and shortens the routes.rb a lot. 
The example above would then just look like:

<pre lang="rails">
map.resources :users, :shallow => true do |user|
  user.resources :posts, :shallow => true do |post|
    post.resources :comments
  end
end
</pre>
and post_url, comment_url, post_comments_url,... get also defined. 

<strong>very nice!</strong>

Have a look at the <a href="http://github.com/rails/rails/commit/83c6ba18899a9f797d79726ca0078bdf618ec3d4">commit message and source code</a> for more information.

<p>
Update:<br />
<a href="http://www.dipl-wirt-inf.de/">Georg</a> of <a href="https://www.salesking.eu/">SalesKing.eu</a> fame pointed me to <a href="http://ryandaigle.com/articles/2008/9/7/what-s-new-in-edge-rails-shallow-routes">Ryan's great post about the :shallow option.</a></p>
