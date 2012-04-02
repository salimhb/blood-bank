--- 
title: "Kickstarting a Rails project #yai7d"
slug: kickstarting-a-rails-project
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 172
wordpress_url: http://blog.railslove.com/?p=172
published_at: 2009-04-30 00:50:32 +02:00
categories: 
- app-in-7-days
- yai7d
tags: 
  keyword: 
  - rg
  - yai7d
  - boswell
  - rails-templates
  - kickstart
---
Die ersten Tage der "Boswell" Entwicklung waren bereits sehr produktiv. Die User stories waren f&Atilde;&frac14;r das Projekt schnell geschrieben und die ersten Interface Skizzen gezeichnet. Ich denke wir werden diese bestimmt nochmal in einem eignen Post ver&Atilde;&para;ffentlichen, jetzt aber erstmal zum initialen Rails Setup. 
Seit Version 2.3 werden ja Applikations-Templates unterst&Atilde;&frac14;tzt, die das Setup sehr einfach und schnell machen und die langweilige Installations-Arbeit abnehmen (<a href="http://blog.railslove.com/2008/12/04/edge-rails-the-rails-command-now-supports-templates/">siehe auch unseren Post von damals</a>)
Auf Github hat&Acirc;&nbsp;<a href="http://www.omgbloglol.com/">Jeremy McAnally</a> einige <a href="http://github.com/jeremymcanally/rails-templates/tree/master">Templates gesammelt</a>. Interessant sind auch die <a href="http://github.com/jeremymcanally/rails-templates/network">54 forks des Projektes</a>.

F&Atilde;&frac14;r unsere Projekte - und eben f&Atilde;&frac14;r die 7 Tage "Boswell" App - haben wir unser eigenes Template:
<style type="text/css">
#gist-39969 .gist-data {
height:300px;
}
</style>
<script src="http://gist.github.com/39969.js"></script>

Ein einfaches <em>rails -m&Acirc;&nbsp;http://gist.github.com/raw/39969/d70e0ff89f59afbaad84593003db27349118bbac/railslove.rb MyNextMySpace </em>macht dann folgendes:
<ul>
	<li>Git repository anlegen und .gitignore f&Atilde;&frac14;llen</li>
	<li>Gem Abh&Atilde;&curren;nigkeiten erstellen f&Atilde;&frac14;r:&Acirc;&nbsp;factory_girl, shoulda, will_paginate, mocha</li>
	<li>Plugins installieren:&Acirc;&nbsp;find_by_param,&Acirc;&nbsp;redirect_love,&Acirc;&nbsp;serialize_fu,&Acirc;&nbsp;limerick_rake,&Acirc;&nbsp;hoptoad_notifier, restful-authentication,&Acirc;&nbsp;annotate_models</li>
	<li>unn&Atilde;&para;tige Dateien wie die index.html l&Atilde;&para;schen</li>
	<li>Initializer z.B. f&Atilde;&frac14;r E-Mail und Hoptoad Konfiguration erstellen</li>
	<li>und ben&Atilde;&para;tigte Resourcen generieren</li>
</ul>

und damit Happy Coding! ;)
