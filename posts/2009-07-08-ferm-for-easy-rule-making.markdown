--- 
title: ferm - for Easy Rule Making
slug: ferm-for-easy-rule-making
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
wordpress_id: 450
wordpress_url: http://blog.railslove.com/?p=450
published_at: 2009-07-08 14:07:19 +02:00
categories: 
- server
tags: 
  keyword: 
  - iptables
  - ferm
  - firewall
  - linux
---
"Easy to use" Firewallregeln w&Atilde;&frac14;rde ich dazu sagen. Wer keine Lust hat sich mit iptables rumzuschlagen und seinen Server vor eventuellen Angreifern sch&Atilde;&frac14;tzen m&Atilde;&para;chte, dem bietet <a href="http://ferm.foo-projects.org/">ferm</a> eine einfache und chicke M&Atilde;&para;glichkeit komplexe Firewallregeln zu verwalten. Das ganze in unter 1 Minute*. Unter Debian einfach:
<code>
# apt-get install ferm
</code>

und ggf. das Anpassen der Konfigurationsdatei:

<code>
# joe /etc/ferm/ferm.conf
</code>

<strong>Update:</strong> Ich habe noch eine simple Konfigurationsdatei hinzugef&Atilde;&frac14;gt, die praktisch out-of-the-box mitkommt:

<script src="http://gist.github.com/142775.js"></script>

Es empfielt sich jedoch vorerst das lesen der <a href="http://ferm.foo-projects.org/download/2.0/ferm.html">Dokumentation</a>. Entsprechende Beispielskripte finden sich auch auf der <a href="http://ferm.foo-projects.org/">Ferm-Homepage</a> unter dem Abschnitt "Dokumentation".
Den Perl-Code gibt es noch oben drauf unter <a href="http://repo.or.cz/w/ferm.git">http://repo.or.cz/w/ferm.git</a>.

*Je nach verf&Atilde;&frac14;gbarer Downloadgeschwindigkeit :D
