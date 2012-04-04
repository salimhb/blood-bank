---
title: ! 'Kickstarting a Rails project #yai7d'
slug: kickstarting-a-rails-project
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 172
wordpress_url: http://blog.railslove.com/?p=172
published_at: 2009-04-30 00:50:32.000000000 +02:00
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
Die ersten Tage der "Boswell" Entwicklung waren bereits sehr produktiv. Die User stories waren für das Projekt schnell geschrieben und die ersten Interface Skizzen gezeichnet. Ich denke wir werden diese bestimmt nochmal in einem eignen Post veröffentlichen, jetzt aber erstmal zum initialen Rails Setup. 
Seit Version 2.3 werden ja Applikations-Templates unterstützt, die das Setup sehr einfach und schnell machen und die langweilige Installations-Arbeit abnehmen (<a href="http://blog.railslove.com/2008/12/04/edge-rails-the-rails-command-now-supports-templates/">siehe auch unseren Post von damals</a>)
Auf Github hat <a href="http://www.omgbloglol.com/">Jeremy McAnally</a> einige <a href="http://github.com/jeremymcanally/rails-templates/tree/master">Templates gesammelt</a>. Interessant sind auch die <a href="http://github.com/jeremymcanally/rails-templates/network">54 forks des Projektes</a>.

Für unsere Projekte - und eben für die 7 Tage "Boswell" App - haben wir unser eigenes Template:
<style type="text/css">
#gist-39969 .gist-data {
height:300px;
}
</style>
<script src="http://gist.github.com/39969.js"></script>

Ein einfaches <em>rails -m http://gist.github.com/raw/39969/d70e0ff89f59afbaad84593003db27349118bbac/railslove.rb MyNextMySpace </em>macht dann folgendes:
<ul>
	<li>Git repository anlegen und .gitignore füllen</li>
	<li>Gem Abhänigkeiten erstellen für: factory_girl, shoulda, will_paginate, mocha</li>
	<li>Plugins installieren: find_by_param, redirect_love, serialize_fu, limerick_rake, hoptoad_notifier, restful-authentication, annotate_models</li>
	<li>unnötige Dateien wie die index.html löschen</li>
	<li>Initializer z.B. für E-Mail und Hoptoad Konfiguration erstellen</li>
	<li>und benötigte Resourcen generieren</li>
</ul>

und damit Happy Coding! ;)
