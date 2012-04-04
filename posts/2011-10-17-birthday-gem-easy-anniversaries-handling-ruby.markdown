---
title: ! '"Birthday" gem for easy anniversaries handling'
slug: birthday-gem-easy-anniversaries-handling-ruby
author: mike_poltyn
published: true
author_name: mike
author_email: mike@railslove.com
author_url: http://mike.poltyn.com
wordpress_id: 1112
wordpress_url: http://blog.railslove.com/?p=1112
published_at: 2011-10-17 11:59:10.000000000 +02:00
categories:
- plugins
tags:
  keyword:
  - activerecord-activesupport-gem-rubygems-birthday-anniversaries
---
While working on one of our client projects, I was asked to create a search for users' birthdays. Instantly, I remembered what problems I had with it in the past, like taking care of not only finding the right dates by only day and month, but also, checking for birthdays today, any upcoming birthdays, or even just looking up user's age based on that information.

So, to never ever repeat that code again (and to keep the code DRY), I've decided to write a simple gem specifically for this stuff. And thus the <a href="https://github.com/railslove/birthday"><tt>birthday</tt> gem</a> was born.

<h3>Requirements</h3>
The gem has been tested against Rails 3 (3.0.9) and Rails 2 (2.3.14), and depends on ActiveRecord and ActiveSupport (for inflections), making it a perfect fit for Rails. It is possible to use it outside Rails project, but you are required to use ActiveRecord as your ORM framework.

The gem works with MySQL and PostgreSQL adapters, but you can <a href="https://github.com/railslove/birthday/blob/master/README.md">write your own adapters</a>, if you need to. If you do so, it would be good to fork the gem and add it there for everybody to use. :)

<h3>So, how does it actually work?</h3>

Handling birthdays wasn't that easy before. Here's what you have to do in your model:

<script src="https://gist.github.com/1292297.js?file=user.rb"></script>

That's all. This one line enables extra actions on the "birthday" field (of DATE or DATETIME types) in your database. For example from now on you can search for birthdays
<ul>
<li>on a specific date:
<script src="https://gist.github.com/1292297.js?file=birthday_console"></script>
</li>
<li>between a specific range:
<script src="https://gist.github.com/1292297.js?file=birthday_console_2"></script>
</li>
<li>and even at the turn of the years:
<script src="https://gist.github.com/1292297.js?file=birthday_console_3"></script>
</li>
</ul>

All these methods are essentially scopes, so you could also do something like:
<script src="https://gist.github.com/1292297.js?file=birthday_console_5"></script>

On top of that, you get convenience methods for single records, like getting the age:
<script src="https://gist.github.com/1292297.js?file=birthday_console_4"></script>

You can get any field to behave like this. For example, let's say we want marriage anniversaries:
<script src="https://gist.github.com/1292297.js?file=marriage.rb"></script>

And it's done, from now on you have convenient scopes to search and handle anniversaries:

<script src="https://gist.github.com/1292297.js?file=marriage_console"></script>

<h3>Final words</h3>

I've done this gem, because I never ever want to write this piece of code again, I'd rather spend my time on actually coding the important stuff in applications, than to fiddle around with dates and birthdays. Hope this gem will be of some use to you. If not, fork it, and patch it to your needs! :)
