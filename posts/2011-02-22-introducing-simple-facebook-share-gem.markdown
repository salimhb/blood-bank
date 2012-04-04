---
title: Introducing simple Facebook Share gem
slug: introducing-simple-facebook-share-gem
author: mike_poltyn
published: true
author_name: mike
author_email: mike@railslove.com
author_url: http://mike.poltyn.com
wordpress_id: 831
wordpress_url: http://blog.railslove.com/?p=831
published_at: 2011-02-22 18:56:00.000000000 +01:00
categories:
- rails
---
I really love how JavaScript can help you integrate social media into your application. But using the same code over, and over again is just annoying.  Therefore, when I was working on inserting a <a href="http://developers.facebook.com/docs/reference/rest/stream.publish/">Facebook share button</a> here and there into our app, I thought, why do I have to repeat everything over and over? So, after a day of hacking, I came up with a simple <a href="https://github.com/holek/facebook_share">gem <tt>facebook_share</tt></a>. This gem will insert any JavaScript needed for Facebook share buttons to work.
<div style="text-align: center;"><a href="http://blog.railslove.com/wp-content/uploads/2011/02/fb-share-confirm.png"><img class="aligncenter size-medium wp-image-833" title="Facebook Share demo" src="http://blog.railslove.com/wp-content/uploads/2011/02/fb-share-confirm-300x210.png" alt="Facebook Share demo" width="300" height="210" /></a></div>
<h2>How does it work?</h2>
Well, that's rather simple. After the gem is installed (<tt>gem install facebook_share</tt>), add this snippet to your ApplicationHelper, and you're almost ready to go.

<script src="https://gist.github.com/838761.js?file=application_helper.rb"></script>

Then create file <tt>config/initializers/facebook_share.rb</tt> with the content below (later versions will automate this process, too). Remember that every parameter here is optional, also that you can include more parameters.

<script src="https://gist.github.com/838761.js?file=facebook_share.rb"></script>

After you type your Facebook application ID, you're ready to go!
<h2>Is it that easy?</h2>
Yes, it's that easy. If you want to share current page, all you have to do is:

<script src="https://gist.github.com/838761.js?file=simple_share.html.erb"></script>

<h2>But how do I customize it?</h2>
What if you have more items I want to share? Or the default selector doesn't work for your application. Maybe you want to use Dojo? Everything is customizable. For example, you can customize your default settings with <tt>facebook_share.rb</tt> initializer, and then override these settings while calling helper methods. I will show you couple of examples and showcase most of public methods in the gem.

If you edited your config initializer, at most of the times you won't need to pass any parameters to the helper functions, but for the sake of the examples, let's say you're running both Dojo and jQuery in your project, you have several Facebook applications you want to use, etc.

<h3>Example 1: Different selector</h3>
<script src="https://gist.github.com/838761.js?file=example_1.html.erb"></script>
will produce:
<script src="https://gist.github.com/838761.js?file=example_1.out.html"></script>

<h3>Example 2: But I already have my JS part!</h3>
Probably you already have your Facebook app initialized in your layout and put the <tt>#fb-root</tt> div tag in there.

<script src="https://gist.github.com/838761.js?file=example_2.html.erb"></script>
will produce:
<script src="https://gist.github.com/838761.js?file=example_2.out.html"></script>

You can easily switch which JavaScript snippets you want to use.

<h3>Example 3: Can I initialize any Facebook application?</h3>
Yes, you can. Albeit this gem being mostly for sharing links on Facebook, it can also be used to ease initialization of a Facebook app. For example, it you feed your facebook_share initializer like so:

<script src="https://gist.github.com/838761.js?file=example_3_facebook_share.rb"></script>

You can simply do:

<script src="https://gist.github.com/838761.js?file=example_3.html.erb"></script>

in your application layout to get:

<script src="https://gist.github.com/838761.js?file=example_3.out.html"></script>

Notice how <tt>locale</tt>'s value of <tt>pl</tt> was transformed into <tt>pl_PL</tt> to meet Facebook expectations, and how only relevant values are included in the Facebook initialization script. Watch out for wrong locales, though, and do not use <tt>:locale => "en"</tt>, as it will produce <tt>en_EN</tt>, and Facebook will not recognize this code as a proper language.

<h3>Example 4: I want my share link to show a different title!</h3>
Sometimes you might want to put a more relevant title about what you want people to share on Facebook. Not a problem, every method accepts the same set of parameters (which, by default are configured in <tt>facebook_share.rb</tt> initializer), and within these parameters you can define any <a href="http://developers.facebook.com/docs/reference/javascript/fb.ui/">FB.ui</a> parameters, and they will be passed on to that function.

<script src="https://gist.github.com/838952.js?file=example_4.html.erb"></script>

<script src="https://gist.github.com/838952.js?file=example_4.out.html"></script>

<h3>Example 5: But I don't use jQuery/Dojo!</h3>
Again, not a problem, if you have configured your facebook_share initializer, that's how you can do it:

<script src="https://gist.github.com/838952.js?file=example_5.html.erb"></script>

<script src="https://gist.github.com/838952.js?file=example_5.out.html"></script>

<h2>That's all, folks</h2>
I wrote this gem to help us all with the tedious task of copy/pasting the same Facebook JS code over and over again. I hope some people will find it useful.

In the meantime, install it, play with it, <a href="https://github.com/Holek/facebook_share">grab source code on github</a>, fork it and code it up!
