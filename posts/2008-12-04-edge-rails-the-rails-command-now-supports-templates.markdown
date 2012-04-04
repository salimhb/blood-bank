---
title: ! '[edge Rails] the rails command now supports templates'
slug: edge-rails-the-rails-command-now-supports-templates
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 60
wordpress_url: http://blog.railslove.com/?p=60
published_at: 2008-12-04 01:40:59.000000000 +01:00
categories:
- edge-rails
- rails
- cool-stuff-on-github
tags:
  keyword:
  - rails
  - edge-rails
  - edgerails
  - rg
---
Setting up a new Rails project is pretty boring. Installing plugins, gems, adding initializers, etc. always the same monotonous work. - not fun. 

That's why there have been quite a lot of starter apps. Most of them are git repositories with blank Rails apps bundled with plugins and extensions. But those are unflexible and the cloning of different repos somehow feels not right. - it's better but still not fun. 

I've also tried to avoid the boring setup work with several tools. My first very, very hackish attempt was <a href="http://github.com/bumi/kickrails/tree/master">kickrails</a>. A stupid ruby script that preceduraly runs all the build commands for me. - not fun either.

But then came <a href="http://github.com/jeremymcanally/rg/tree">RG</a>. An awesome über cool project developed by <a href="http://github.com/jeremymcanally">Jeremy McAnally.</a> RG allows you to kickstart your Rails app using templates written in ruby. <strong>- fun!</strong> ;) One command and your done. RG runs the rails command and setups all the stuff to get you started based on templates.

I've <a href="http://github.com/bumi/rg">created a fork</a>, added some more helpers and used it for several projects. It turned out great. 

<strong>Anyway what I wanted to tell is: <a href="http://github.com/rails/rails/commit/e8cc4b116c460c524961a07da92da3f323854c15">RG just got added to Rails core</a></strong>. This means the <em>rails </em>command now supports templates for building your inital apps. Running <em>rails -m/--template my_super_cool.template</em> not only generates the default rails skeleton for you but also applies the template which installs plugins, gems, extensions, initializes a git repository, etc.  - <strong>pretty awesome - <strong>fun!</strong> </strong>

I'm as excited as I've been when I've ran the <em>rails</em> command for the first time. 

How do you setup your rails app? Now compare that to: 
<a href="http://www.flickr.com/photos/bumi/3081208668/" title="RG template by Bumi, on Flickr"><img src="http://farm4.static.flickr.com/3241/3081208668_59b161bba5_o.jpg" width="442" height="274" alt="RG template" /></a>
Isn't rails great?!

 
