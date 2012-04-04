---
title: No magic behind it but everytime worth to remember
slug: rspec-refactoring-and-shared-example-groups
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
wordpress_id: 1160
wordpress_url: http://blog.railslove.com/?p=1160
published_at: 2011-11-23 23:18:49.000000000 +01:00
categories:
- railslove
---
<h2>Rspec Refactoring and Shared Example Groups</h2>

Today we had lightning talks about specs refactoring. Jan showed us some tricks based on his experiences from our latest open source project: <a href="http://railsrunners.org">railsrunners.org</a> (<a href="https://github.com/railslove/railsrunners">Github</a>):

<h2>Some simple spec principles</h2>

<ul>
<li>Use clear descriptions for your specs in combination of using "describe"-, "context"-blocks</li>
<li>Use contexts and descriptions properly, e.g.: <code> describe "#edit"; context "with valid params"; etc.</code></li>
<li>Use the --format documentation parameter to check your descriptions for specs, describes, and contexts. E.g.: <code>rspec spec/controllers/participants_controller_spec.rb --format documentation</code></li>
<li>Instead of manually creating associated models in your tests just to pass validations, FactoryGirl can automatically create them for you, e.g.:</li>

<script src="https://gist.github.com/1389942.js?file=gistfile1.rb"></script>

<li>Then instead of:</li>

<script src="https://gist.github.com/1389938.js?file=gistfile1.rb"></script>

<li>You'd simply have:</li>

<script src="https://gist.github.com/1389934.js?file=gistfile1.rb"></script>

<li>Write one assertion per test.</li>
<li>Stub requests using FakeWeb (<strong>Update: or WebMock or any other Request-Mocking-Helper</strong>), e.g.: FakeWeb.register_uri(:get, "http://static-maps-generator.appspot.com/url?msid=#{@future_run.msid}&size=950x300", :body => response)</li>
<li>Controller specs should only test the behaviour of your controller. Model specs test the behaviour of your model. Don't mix the two! E.g.: do not test after_ or before_ save callbacks in your controller tests.</li>
</ul>

Take a look at the railsrunners Github repository: <a href="https://github.com/railslove/railsrunners">Github</a>

<h2>Shared example groups</h2>

Sometimes you want to test the same behaviour in various specs or contexts. To keep your code DRY, you can use RSpec's shared example groups:

<script src="https://gist.github.com/1389943.js?file=gistfile1.rb"></script>

If needed, you can move the shared example group to a spec helper and require that wherever you need to test for 'successful responses'.

<h2>Further reading:</h2>

<a href="https://www.relishapp.com/rspec/rspec-core/v/2-0/docs/example-groups/shared-example-group">https://www.relishapp.com/rspec/rspec-core/v/2-0/docs/example-groups/shared-example-group</a>
<a href="http://rspec.info/documentation/">http://rspec.info/documentation/</a>
<a href="http://blog.davidchelimsky.net/2010/11/07/specifying-mixins-with-shared-example-groups-in-rspec-2/">http://blog.davidchelimsky.net/2010/11/07/specifying-mixins-with-shared-example-groups-in-rspec-2/</a>
