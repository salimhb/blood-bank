---
title: Make email a better citizen of the modern HTTP world...
slug: make-email-a-better-citizen-of-the-modern-http-world
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 265
wordpress_url: http://blog.railslove.com/?p=265
published_at: 2009-05-12 02:10:59.000000000 +02:00
categories:
- railslove
---
<p>We're currently adding some mail-in functionality to some web applications. You know like emailing stuff to an application which then does fancy things with it.<br /> And honestly the code for this really sucks. It works... but I'm not very happy with our solution: </p>
<p>
The mailserver is running on an extra machine so we connect via IMAP fetch the emails and parse the raw data. If everything is OK, the email is moved to a special backup folder.<br />
There are some other solutions like <a href="http://github.com/entp/astrotrain/tree/master">Astrotrain</a> which pipes the email to a script but these aren't better...
</p>
<p>So one question hits my head over and over again:<br />
<strong>Why is this so hard? What did you mailserver developers do in the last fiveish years???!!! Did anything in the email world change?</strong>
</p>
<p><strong>Here is my wishlist for you:</strong><br /></p>
<ul>
<li>simple REST interface to the mailboxes (POST,GET, PUT, DELETE)</li>
<li>JSON and XML representation of emails</li>
<li>permalink for every email</li>
<li>atom and rss feeds of mailboxes</li>
<li>support for <a href="http://webhooks.org">webhooks</a></li>
<li>that means HTTP push notification for new emails</li>
<li>OAuth Authentication(?)</li>
<li>do only mail! stay focused! - no calendar and other stupid stuff</li>
</ul>
<p>
In short: <strong>Build an easy to use simple restful API for email which stupid web developers like I am can use to build awesome stuff upon.</strong><br />
This would make email a much better citizen in the modern HTTP web world.
</p>

