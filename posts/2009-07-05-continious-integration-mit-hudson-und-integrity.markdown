---
title: Continious integration mit Hudson und Integrity
slug: continious-integration-mit-hudson-und-integrity
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
wordpress_id: 442
wordpress_url: http://blog.railslove.com/?p=442
published_at: 2009-07-05 14:41:04.000000000 +02:00
categories:
- railslove
- rails
- cool-stuff-on-github
- continious-integration
tags:
  keyword:
  - cc
  - hudson
  - integrity
  - continious
  - integration
  - tests
---
<a href="http://martinfowler.com/articles/continuousIntegration.html">Continious Integration</a> ist ein wichtiger Bestandteil von Software, vor allem wenn mehrere Beteiligte am Projekt Teilnehmen. Nach jedem Push wird dann der aktuelle Code vom CI-System ausgecheckt und die gewünschten rake-Tasks ausgeführt. Neben dem schon bekannten <a href="http://cruisecontrolrb.thoughtworks.com/">CrusieControll.rb</a> gibt es noch zwei andere interesannte Cnotinious Integration Tools die ich kurz vorstellen möchte: <a href="http://integrityapp.com/">Integrity</a> und <a href="https://hudson.dev.java.net/">Hudson</a>.

<h2>Integrity</h2>
Integrity ist sehr einfach gestrickt. Nach der relativ <a href="http://integrityapp.com/#setup">simplen installation</a> kann man verschiedene Projekte hinzufügen. Der einzige "overhead" der noch ensteht, ist das zusammenstellen eines rake-tasks den Integrity nach jedem pull ausführt. Dieser einfacher rake-Task kann als Einstieg dienen:

<script src="http://gist.github.com/140958.js"></script>

Nach jedem Build können die Entwickler auch über die zu <a href="http://integrityapp.com/#notifiers">verfügung stehenden Notifier (Email, Campfire, IRC, ...)</a> über den Stand informiert werden. Weiterhin gibt es auch ein <a href="http://github.com/calavera/integrity-growl/tree/master">Growl-Plugin</a> und <a href="http://integrity-menu.com/">Dashboard-Widget</a>. Der Build der Applikation wird über Github via einem POST-Webhook zu Integrity angetriggert.

Der einzige Nachteil ist, dass <a href="http://groups.google.com/group/integrityapp/browse_thread/thread/d4c7a2d15b4bca19">bei lang-andauernden Builds der entsprechende Webserver einen Timeout erreicht</a>. Der kann natürlich hochgesetzt werden.

<a href="http://www.ipernity.com/doc/koos/5307600"><img src="http://u1.ipernity.com/11/76/00/5307600.fa483a9f.500.jpg" width="500" height="288" alt="Integrity" border="0"/></a>

<h2>Hudson</h2> 
Hudson ist eine weitere Alternative. Es ist ein Java-Basiertes CI-System und wird out-of-the-box mit einem Webserver ausgeliefert. Entsprechende Debian-Packages gibt es <a href="http://weblogs.java.net/blog/kohsuke/archive/2008/06/debian_packages.html">hier</a>. Hudson bietet gegenüber Integrity mehr Konfigurationsmöglichkeiten, daher dauert es ein bisschen länger bis man sein neues CI-System am laufen hat. <a href="http://wiki.hudson-ci.org/display/HUDSON/Meet+Hudson">Meet-Hudson</a> bietet eine gute Übersicht über Hudson.

Der oben schon vorgestellte Rake-Task kann ebenfalls für Hudson verwendet werden. Allerdings müssen Plugins für eine Rake- und Githubunterstützung installiert werden (<a href="http://wiki.hudson-ci.org/display/HUDSON/Git+Plugin">Git-Plugin</a> und <a href="http://wiki.hudson-ci.org/display/HUDSON/Rake+plugin">Rake-Plugin</a>).

Bei Hudson ist der initiale Konfigurationsaufwand zwar geringer als bei Integrity, dafür müssen viele Plugins installiert und konfiguriert werden um seine "perfekte" CI-Umgebung ans laufen zu bekommen. Unschön an Hudson ist die fehlende unterstützung des triggern eines Builds über einen POST-Webhook. Stattdessen kann dies nur über ein GET getriggert, was aber seitens Github nicht unterstützt wird. Eine Alternative ist das periodische abprüfen von Änderungen in der Repository.

<a href="http://www.ipernity.com/doc/koos/5307598"><img src="http://u1.ipernity.com/11/75/98/5307598.9ca4f9ba.500.jpg" width="500" height="317" alt="Hudson" border="0"/></a>
