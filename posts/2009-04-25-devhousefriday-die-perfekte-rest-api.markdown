---
title: DevHouseFriday - Die perfekte REST-API
slug: devhousefriday-die-perfekte-rest-api
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
wordpress_id: 122
wordpress_url: http://blog.railslove.com/?p=122
published_at: 2009-04-25 13:23:22.000000000 +02:00
categories:
- railslove
- channelthing
- devhousefriday
---
Gestern hat natürlich unser wöchentlicher DevHouseFriday Talk stattgefunden. Diesesmal wurde in der Runde das Thema diskutiert, wie eine perfekte API aussehen kann. Die eine Antwort darauf wurde auch nicht erwartet, aber anhand <a href="http://apiwiki.twitter.com/Twitter-REST-API-Method%3A-users show">einiger</a> <a href="http://mite.yo.lk/api/projekte.html">Beispiele</a> im <a href="http://develop.github.com/">Netz</a> kamen viele Impulse aus der Runde die das Entwickeln einer "sauberen" API bestimmt helfen können.:
<ol>
<li>Schicke nicht "so viel wie möglich" mit einer Anfrage mit. Mach das immer abhängig von deinem Anwendungskontext - was ist relevant, was "könnte" relevant sein. Wenn du dir nicht sicher bist - lass lieber was weg. Das ist entscheidend während der Evolution deiner API - wenn viele unabhängige Clients deinen Service benutzen, kann das entfernen von Attributen die mit einem Response zurückgegeben werden, sehr problematisch werden. Aber berücksichtige das - eine API lebt.</li>
<li>Implementiere selber einen Client während der Gestaltung deiner API - probiere sie direkt aus.</li>
<li>Versioniere deine API. Damit kannst Du sie (mit Vorsicht) ausbauen oder Attribute wieder entnehmen, indem Du die Änderungen Versionierst. Bei der Versionierung gibt es drei Möglichkeiten: entweder du kennzeichnest die Version in der URI - über die URL (z.B. <a href="http://docs.amazonwebservices.com/AmazonSimpleDB/2007-11-07/DeveloperGuide/index.html?APIVersioning.html">Amazon</a> oder <a href="http://develop.github.com/p/general.html">Github</a>) oder einen Parameter oder du setzt deinen eigenen content-type für den Request. Bei der Veränderung der URL solltest man sich im klaren sein, dass zwei unterschiedliche Identifier (../v1/.. und ../v2/..) ein und die selber Ressource beschreiben.</li>
</ol>

Das waren meiner Meinung nach die drei wichtigsten Themen die wir gestern in der Runde angesprochen haben. Wir werden die Erkentnisse für die Entwicklung unserer API für <a href="http://channelthing.com">Channelthing</a> bestimmt mitnehmen und sind gespannt auf unseren ersten iPhone-Prototypen der sie direkt ausprobieren kann (danke an @flxmllr).

Freu mich schon aufs nächste DevHouseFriday!

<a href="http://www.ipernity.com/doc/koos/4683465"><img src="http://u1.ipernity.com/11/34/65/4683465.368be313.500.jpg" width="500" height="277" alt="The Perfect API talk #devhousefriday" border="0"/></a>

Btw.: stay in touch via unserem <a href="http://wiki.railslabs.com/index.php?title=Main_Page">wiki</a> und unserer <a href="http://www.facebook.com/group.php?gid=57051643796">facebook-guppe</a>
