--- 
title: "Marker-Cluster f&Atilde;&frac14;r die Google Map "
slug: marker-cluster-fur-die-google-map
author: michael_bumann
published: true
author_name: Bumi
author_email: michael@railslove.com
author_url: http://
wordpress_id: 183
wordpress_url: http://blog.railslove.com/?p=183
published_at: 2009-05-05 19:05:46 +02:00
categories: 
- railslove
- app-in-7-days
- yai7d
tags: 
  keyword: 
  - googlemaps
  - yai7d
  - boswell
  - cluster
  - marker
---
Jeder der schon mal versucht hat viele Marker auf einer Google map anzuzeigen wird schnell ferststellen, dass das kein Spass macht. Zum einen sieht die Karte dann bei einem niedrigen Zoomlevel sehr un&Atilde;&frac14;bersichtlich aus - man sieht eigentlich die Karte vor Marker nicht mehr- und zum anderen sinkt die Performance des Browsers bei vielen Markern starkt.
Jeder Marker besteht aus vielen einzelnen DOM-Elementen. Und bei mehreren Tausend Marken macht das Verarbeiten und Anzeigen dieser Vielzahl an DOM-Elementen dem Browser schwer zu schaffen. 

Um dieses Problem zu l&Atilde;&para;sen gibt es die M&Atilde;&para;glichkeit die Marker zu einzelnen Clustern zusammenzuf&Atilde;&frac14;gen. Ein guter Einstieg in dieses Thema ist der Blogpost von <a href="http://www.svennerberg.com">Gabriel Svennerberg</a> zum Thema <a href="http://www.svennerberg.com/2009/01/handling-large-amounts-of-markers-in-google-maps/ ">Handling Large Amounts of Markers in Google Maps</a>. Hier werden verschiedene Methoden zum Clustern von Markern und vor allem ein Benchmark zur Ladezeit vorgestellt.

In den Kommentaren st&Atilde;&para;sst man aber auf eine L&Atilde;&para;sung von <a href="http://googlegeodevelopers.blogspot.com/2009/04/markerclusterer-solution-to-too-many.html">Xiaoxi Wu im Google Geo Developers Blog</a>. Hier werden die einzelnen DOM-Elemente in einen Cluster zusammengefasst, wenn er in einem vorgegebenem Range liegt. In einem <a href="http://gmaps-utility-library.googlecode.com/svn/trunk/markerclusterer/1.0/examples/speed_test_example.html">Demo</a> kann man entsprechende Speed-Tests mit diesem Verfahren ausprobieren. Das Laden von ca. 500 Markern dauert ca. 331 ms. was gegen&Atilde;&frac14;ber dem Benchmark von Gabriel Svennerberg eine akzeptable Ladezeit ist.

<a href="http://www.ipernity.com/doc/koos/4775979"><img src="http://u1.ipernity.com/11/59/79/4775979.6aed4963.240.jpg" width="240" height="222" alt="Clustering Markers on a google map" border="0"/></a>

F&Atilde;&frac14;r unser #yai7d-Projekt "Boswell" mussten wir zus&Atilde;&curren;tzliche Modifikationen in das Skript einbauen um die einzelnen geclusterten Objekte auszulesen.

Der Post kommt mit einer kleinen Verz&Atilde;&para;gerung durch die entstandenen Feiertage. Unser erstes #yai7d-Projekt ist aber abgeschlossen. Wir werden sehr bald dadr&Atilde;&frac14;ber Bloggen!

Viel Spass beim Clustering!
