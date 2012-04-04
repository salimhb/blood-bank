---
title: JSON Schema Baby
slug: json-schema-baby
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
wordpress_id: 1001
wordpress_url: http://blog.railslove.com/?p=1001
published_at: 2011-09-05 19:43:02.000000000 +02:00
categories:
- railslove
- rails
- ruby
tags:
  keyword:
  - rails
  - api
  - ruby
  - rabl
  - json
  - schema
  - design
---
<p>Building an application programming interface is not easy. Designing an API is more complex than just writing code. For a few projects we tried out different approaches to implement an API in Ruby on Rails. There are two main ways to make your resources accessible:</p>

<ul>
<li>using the standard to_json renderer built into Rails</li>
<li>building your own views</li>
</ul>

<h2>Using standard renderer provided by Rails</h2>

<p>In Rails 2.0 you have the possibility to using the respond_to block to expose your resource in whatever format you rewuire (xml, json, html). E.g.:</p>

<script src="https://gist.github.com/1176845.js?file=gistfile1.txt"></script>

<p>The same is possible in Rails 3.0 but a little bit easier:</p>

<script src="https://gist.github.com/1176847.js"></script>

<p>In these examples you can define the representation of your resource by defining the format you want the resource to be represented in. But in most cases you don't want to expose every attribute of your resource. To achieve this, you could use Rails' as_json method to create a custom JSON structure of your resource. E.g:</p>

<script src="https://gist.github.com/1176858.js"></script>

<p>As Jonathan Julian mentioned <a href="http://jonathanjulian.com/2010/04/rails-to_json-or-as_json/">in his blog post</a>, call as_json directly or override it in your model to customize your representation of your resource. Sounds easy so far. Summarizing this approach we can say:</p>

<ol>
<li>It is understandable and quite easy to use</li>
<li>You can easily customize the representation of your resources via the as_json method</li>
</ol>

<p>But the way how this approach is realized is not the best in my opinion, because it too much correlated with the models when we talking only about a "representation". That's why I like the second approch - building your own views.</p>

<h2>Customize it baby</h2>

<p>What does it exactly mean? Instead of just overriding the as_json method in your model, build a template that exposes your API. The easiest way is, e.g., to use RABL - Ruby API Templating Language.</p>

<p>As in the example before you define within your controller structure WHICH resources are being exposed, like:</p>

<script src="https://gist.github.com/1180699.js"></script>

<p>And within your RABL-Template now you can define HOW your resources should look:</p>

<script src="https://gist.github.com/1180701.js"></script>

<p>What happened here is that the representation of the resource is properly split from the resource using templates, like using .html-templates that belongs to your views. Thats great. You're very flexible to define how the respresentation should looks like without overriding some methods. The resource is exposed 'as it is' but the template takes the response of what representation exactly the API users should get. In general, that seems to be the right approach; and it really is, but for me it isn't going far enough. What I like to see is an even looser representation.</p> 

<h2>Here comes JSON-Schema</h2>

<p>Now we're going a step further and completely split our resource from the representation. Based on JSON-Schema (http://json-schema.org/) we're going to define one that is responsible how our resource is being represented. With this approach, it is also possible to define our yourself in which way you want to interpret the schema within your code. And it's fully decorrelated if you want to.</p>

<p>If found a very good approach for using the JSON-Schema for an API representation (sk_api_schema - https://github.com/salesking/sk_api_schema) - a Ruby library that defines the schema which takes care of the representation of their API resources.</p>

<p>How does it work? Your controllers are almost the same. E.g.:</p>

<script src="https://gist.github.com/1180702.js"></script>

<p>The only small difference is the object_as_json method, which is provided by your own schema library. This method takes the properties defined in the schema and looks them up on the object in question.</p>

<p>Within your schema for a single resource looks like this:</p>

<script src="https://gist.github.com/1180703.js"> </script>

<p>As you can see, the schema described everything:</p>

<ul>
<li>The <em>resource itself</em> - here a user</li>
<li>Its <em>properties</em> - the attributes of this resource</li>
<li><em>Links</em> belonging to this resource - These describe some nested resources which belong to this resource and you can also define search parameters here</li>
</ul>

<p>And there's even one more big advantage: publishing your JSON-Schema library gives your API users a good and clean documentation of your interface. You don't have to describe it anymore. Moreover, it could be possible to generate a nicer representation from your documentation. You can see an example of thishere: http://sk-api-browser.heroku.com/. This API browser reads the JSON-Schema here and generates a nice overview of the API.</p>

<h2>Summary</h2>

What I tried to describe here were some facts about how to implement an API with Ruby on Rails but more about how to split the resource itself from the representation in your webservice. For this you can use internal methods responsible for representing your resource, or create your own templates with defined libraries like RABL. Using JSON schema for the representation of your API is the most loosely coupled approach. With JSON schema you're don't care about the resource's representation within your code but reather within your schema. It's a description of whatever you want to expose to your clients.

<h2>Resources</h2>

<ul>
<li><a href="http://sk-api-browser.heroku.com/">A JSON schema browser</a></li>
<li><a href="https://github.com/salesking/sk_api_schema">SalesKing API schema</a></li>
<li><a href="http://json-schema.org/">JSON schema</a></li>
<li><a href="https://github.com/nesquena/rabl/wiki/Set-up-rabl-for-Ruby-on-Rails">Set up RABL for Ruby on Rails</a></li>
<li><a href="http://teohm.github.com/2011/05/using-rabl-in-rails-json-web-api">Using RABL in Rails JSON Web API</a></li>
<li><a href="https://github.com/nesquena/rabl">RABL</a></li>
<li><a href="http://www.rubyflow.com/items/5649-rabl-the-ruby-api-templating-language">RABL, The Ruby API Templating Language</a></li>
<li><a href="http://jonathanjulian.com/2010/04/rails-to_json-or-as_json/">Rails to_json or as_json?</a></li>
</ul>
