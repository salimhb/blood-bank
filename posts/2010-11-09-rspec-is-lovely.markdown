---
title: Rspec Is Lovely
slug: rspec-is-lovely
author: red_davis
published: true
author_name: reddavis
author_email: reddavis@gmail.com
author_url: http://redwriteshere.com/
wordpress_id: 739
wordpress_url: http://blog.railslove.com/?p=739
published_at: 2010-11-09 16:28:24.000000000 +01:00
categories:
- ruby
tags:
  keyword:
  - testing
  - rspec
---
Several months ago my choice of testing framework was TestUnit + Shoulda. Rspec looked good, but I didn't see what made it particularly special.

When working on a client project which was using Rspec I decided to properly look into it. What I found was that it made my tests incredibly organised and very easy to follow. Below are some methods I take when writing Rspec tests.
<h3>Describes</h3>
Don't skimp on them! If you find your "it"s becoming too long or <strong>describing</strong> too much then it is usually a good sign that you should be using a describe.

<script src="https://gist.github.com/669076.js?file=gistfile1.rb"></script>
<h3>Setting The Subject</h3>

I find setting the subject great for focussing your testing. Setting the subject tells Rspec...what the subject of the is test is. i.e. what these tests are in reference to.  <script src="https://gist.github.com/669090.js?file=gistfile1.rb"></script>

<h3>Its</h3>

This is probably easier to just show in code rather than describe...

<script src="https://gist.github.com/669093.js?file=gistfile1.rb"></script>

<h3>Context</h3>

This is great for outlining different outcomes for a method:

<script src="https://gist.github.com/669111.js?file=gistfile1.rb"></script>

<h3>Let</h3>

From the docs: "Generates a method whose return value is memoized after the first call."

<script src="https://gist.github.com/669118.js?file=gistfile1.rb"></script>

<h3>Specify</h3>

Specify is just like <strong>it</strong>. I like to use it when I am not testing against a subject:

<script src="https://gist.github.com/669129.js?file=gistfile1.rb"></script>

<h3>One Last Thing</h3>

You can specify Rspec configurations in a .rspec file. I have the color and profile options which: make pretty colours and will display the 10 slowest tests.

<script src="https://gist.github.com/669133.js?file=.rspec"></script>

That's not all! You should definitely look at the Rspec <a href="http://github.com/rspec/">source code</a>.

Happy Rspec'in!

Edit:

Thanks to <a href="http://twitter.com/bumi">@bumi</a> and <a href="http://twitter.com/clemensk">@clemensk</a> for reminding me about <strong>expect</strong>.

<script src="https://gist.github.com/669158.js?file=gistfile1.rb"></script>

Using expect is a lot nicer than using the good old lambda route:

<script src="https://gist.github.com/669202.js?file=gistfile1.txt"></script>
