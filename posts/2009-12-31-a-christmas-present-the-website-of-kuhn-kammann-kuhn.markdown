---
title: ! 'A christmas present: The website of Kuhn, Kammann & Kuhn'
slug: a-christmas-present-the-website-of-kuhn-kammann-kuhn
author: tim_schneider
published: true
author_name: Tim
author_email: tim@railslove.com
author_url: http://railslove.com
wordpress_id: 546
wordpress_url: http://blog.railslove.com/?p=546
published_at: 2009-12-31 01:43:48.000000000 +01:00
categories:
- railslove
---
What did you get for christmas?

We already made ourselves a first christmas present two weeks ago: the new website of <a href="http://www.kkk-ag.de/" title="Kuhn, Kammann & Kuhn - Home">Kuhn, Kammann & Kuhn</a> - a Cologne-based business communication agency. Well, more precisely: the guys from Kuhn, Kammann & Kuhn made theirselves a first christmas present, but nevertheless it&#x27;s also a great pleasure for us to see this jewel (ruby!) of a website working and growing in public.

<img src="http://img.skitch.com/20091230-gktyx3hegx3umieifekdjfrqes.jpg" alt="the new website of Kuhn, Kammann & Kuhn"/>

Back in october, when Wendelin from KKK asked us to build their new agency website, we thought "well, usually we&#x27;re building complex web apps, rarely corporate websites", but then their way to deal with both editorial and aggregated social media content in a constantly changing grid layout foo&sup1; grabbed our attention. And now, after eight days of exciting agile cooperation and several feature iterations, it&#x27;s done - and online.

<strong>What&#x27;s so special about this website?</strong>

On the one hand it&#x27;s this mix of a tag-based navigation and a flexible grid of content objects. No more static sitemaps! Tags basically work as content filters, but it&#x27;s not done at this point here: Every content object has its lifetime and is constantly fading until it isn&#x27;t visible anymore. In addition to the tags and visibilities of an object, every collection of content objects is a well prepared composition of different content types, which gets slightly shuffled to look nicer without loosing the chronology of its items. Finally all objects are positioned and animated by a piece of JavaScript, which handles any combination of small and large boxes.

<strong>Hands on Superfeedr</strong>

Beside their editorial content, the KKK people want <a href="http://www.kkk-ag.de/news" title="Kuhn, Kammann & Kuhn | news">to aggregate</a> a bunch of Twitter-Accounts and Weblogs constantly. Because we don&#x27;t like the hassle with grabbing and parsing a growing number of feeds, we&#x27;re using the <a href="http://superfeedr.com/" title="Superfeedr : Real-time feed parsing in the cloud for web-developers">Superfeedr API</a> for the first time in this project. There&#x27;s a handy (but incomplete) Rails plugin <a href="http://github.com/empika/Superfeedr-PubSubHubbub-Rails-Plugin/">on Github</a> you might want to use to subscribe and unsubscribe to feeds, but the HTTP POST notification parsing part isn&#x27;t covered. So <a href="http://github.com/pauldix/feedzirra/" title="pauldix's feedzirra at master - GitHub">Feedzirra</a> helped us to get down to the beef. After two weeks of running the app with Superfeedr we&#x27;re not missing one feed entry, but the time period between publishing a tweet and Superfeedr&#x27;s POST notification is often longer than the promised 15 minutes - yet. We&#x27;ll see, seems like a painless feed grabbing solution anyway, if real-time doesn&#x27;t mean instant delivery in your biz.

Enjoy surfing the new website of <a href="http://www.kkk-ag.de/" title="Kuhn, Kammann & Kuhn - Home">Kuhn, Kammann & Kuhn</a>!

&sup1; <small>It's hard to find the right words. You have to <del datetime="2009-12-30T23:36:17+00:00">see</del> <em>feel</em> it...</small>
