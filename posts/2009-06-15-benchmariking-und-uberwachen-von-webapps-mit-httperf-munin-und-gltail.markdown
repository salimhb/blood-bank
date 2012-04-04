---
title: Benchmariking und Überwachen von Webapps mit httperf, munin und gltail
slug: benchmariking-und-uberwachen-von-webapps-mit-httperf-munin-und-gltail
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
wordpress_id: 419
wordpress_url: http://blog.railslove.com/?p=419
published_at: 2009-06-15 23:46:03.000000000 +02:00
categories:
- cool-stuff-on-github
- monitoring
- server
tags:
  keyword:
  - gltail
  - monitoring
  - server
  - statistics
  - stats
  - munin
  - httperf
---
Für unser letztes Projekt war Benchmarking und klare Aussagen über die Auslastung des Servers ein wichtiger Punkt. Daher haben wir uns ein paar Tools herangezogen die uns geholfen haben unsere Webapplikation (visuell) "im Griff" zu behalten.

<h2>Benchmarking mit httperf</h2>
<a href="http://www.hpl.hp.com/research/linux/httperf/">Httperf</a> ist in erster Linie ein Benchmarking-Tool dass die Durchsatzrate von Requests eines Webservers messen kann. Von httperf wird mit einer fixen Rate diese Requests an den Server geschickt und mit den angekommenen Replies verglichen. Der Output gibt uns Informationen zu der Dauer dieses Tests, der Fehlrate (Anzahl der nicht erhaltenen Replies).

Einen Beispielhaften Output kann man <a href="http://pastie.org/512879">hier</a> einsehen.

Das Ergebnis einer Messung sind:
<ul>
<li>Daten über die TCP-Verbindungen</li>
<li>RequestDaten</li>
<li>Ergebnisse der empfangenen Replies</li>
<li>CPU-und Netzdaten</li>
<li>Auswertung der aufgetretenen Fehler (Timeouts)</li>
</ul>

Sehr interessant dabei ist das Resultat der Reply rate:

<code>
Reply rate [replies/s]: min 0.0 avg 4.9 max 10.8 stddev 4.2 (40 samples)
</code>

Diese gibt uns eine Auskunft über den Durchschnitt und die Standardabweichung der Antwortzeit. Diese Messungen sind genauer je mehr Stichproben während der ganzen Messung entnommen wurden. Durch die Optimierung des Programmcodes können diese Werte dann demensprechend verbessersert und dadurch eine schnellere Antwortzeit gemessen werden. Mehr Informationen zu httperf sind aus dem <a href="http://www.hpl.hp.com/research/linux/httperf/docs.php">Manual</a> zu entnehmen. Weitere Informationen kann man auch im Blogpost von <a href="http://agiletesting.blogspot.com/2005/04/http-performance-testing-with-httperf.html">Grig Gheorghiu</a> nachlesen. Wer ein bisschen tiefer in die Materie einsteigen möchte, dem empfehlen wir den Screencast von <a href="http://peepcode.com">Peepcode</a> "<a href="http://peepcode.com/products/benchmarking-with-httperf">Benchmarking with httperf</a>"

<h2>Monitoring mit Munin</h2>

Um die Server während der Produktivbetriebs visuell im Blick zu haben empiehlt sich die Benutzung von <a href="http://munin.projects.linpro.no/">Munin</a>. Mit Munin ist es möglich die verschiedenen Prozesse/Daten des Servers zu visualisieren. Dazu werden so genannte munin-nodes installiert (die zu überwachenden Server). Diese Nodes werden dann auf dem Munin-Server aggregiert, verarbeitet und Visualisiert.

<a href="http://www.ipernity.com/doc/koos/5139132"><img src="http://u1.ipernity.com/11/91/32/5139132.59332529.500.jpg" width="500" height="329" alt="Munin statistic graphs" border="0"/></a>

Standardmäßig bietet Munin Statistiken zu:
<ul>
<li>Filesystem usage (in %)</li>
<li> MySQL throughput</li>
<li> MySQL queries</li>
<li>...</li>
</ul>

Eine sehr schöne Eigenschaft von Munin ist, dass dieses Tool pluggable ist, d.h. es können verschiedene Skripte eingebunden werden. Wenn man Rails-Applikationen mit Phusion Passenger laufen lässt, stehen auf <a href="http://github.com">Github</a> <a href="http://gist.github.com/20319">zwei nette Skripte</a> zur Verfügung die man einfach in Munin einbinden kann. Mehr zu Munin-Plugins kann man in <a href="http://www.dcmanges.com/blog/rails-application-visualization-with-munin">diesem Blogpost</a> nachlesen.

<h2>Quasi-Echtzeitstatistiken mit glTail</h2>

Eine nette Ergänzung zur Überwachung von Webapplikationen ist <a href="http://www.fudgie.org/">gltail</a>. Gltail bietet eine (quasi-)Echtzeit Darstellung von log-Files jeder Art. Dies kann natürlich dazu verwendet werden, um z.B. die Apache-Logs, Production-logs, etc. zu visualizieren.

<a href="http://www.ipernity.com/doc/koos/5042502"><img src="http://u1.ipernity.com/11/25/02/5042502.7a176e85.500.jpg" width="500" height="294" alt="glTail" border="0"/></a>
