---
title: channelthing - a big picture
slug: channelthing-a-big-picture
author: jan_kus
published: true
author_name: Jan
author_email: jan@railslove.com
author_url: http://www.railslove.com
wordpress_id: 242
wordpress_url: http://blog.railslove.com/?p=242
published_at: 2009-05-16 19:45:14.000000000 +02:00
categories:
- railslove
- channelthing
tags:
  keyword:
  - channelthing
  - collaboration
  - team
  - work
  - mail
  - communication
  - kommunikation
  - kollaboration
---
Bald (!) ist es soweit - unsere "nigelnagelneues" <a href="http://channelthing.com">channelthing</a>-Release wird für unsere Alpha-User released. Fast täglich erreichen uns mittlerweile neugierige Anfragen und um die Vorfreude noch ein bisschen anzuheizen, möchten wir euch heute die Kern-Features von channelthing vorstellen.

<h2>Also, was ist channelthing?</h2>
channelthing ist ein Microblogging-Tool für Teams, mit dem Nachrichten und Dokumente ausgetauscht werden können. Alle Informationen werden zentral zugänglich in einem Online-Kanal gespeichert, aufbereitet und annotierbar; der Begriff "Informationen" ist dabei weit gefasst: wir möchten sämtliche multimedialen Schnippsel einfangen, die bisher über E-Mail, File-Server oder Dropbox-ähnliche Service verteilt wurden. Diese können sowohl über ein Webinterface im Blog-Stil oder direkt per E-Mail an einen Channel gesendet werden. Über verschiedene Wege (RSS, E-Mail, ...) verteilt der Channel die Informationen dann wieder an ihre Empfänger.

Jedes Team-Mitglied entscheidet bei channelthing, wie und wann es Nachrichten empfangen möchte. So können z.B. eingehende E-Mails direkt weitergeleitet werden oder nur einmal am Tag gebündelt als Zusammenfassung.

<h2>Wie ist der Service aufgebaut?</h2>
In channelthing gehört jeder <em>Coworker</em> - das ist unsere Bezeichnung für einen Benutzer - einer oder mehreren <em>Companies</em> an und kann in beliebig vielen <em>Channels</em> seiner Companies mitarbeiten. Als Mitglied einer Company hat man automatisch Zugang zu deren Channels.

Darüber hinaus können Coworker aber auch in Channels fremder Companies eingeladen werden und dort mitarbeiten - ohne, dass sie Mitglied der Company werden und ohne, dass sie Zugriff auf übrige Channels dieser Company haben. Dies ist dann sinnvoll, wenn z.B. Freelancer in einem Projekt eingebunden werden.

<h3>Scopes und Logins</h3>
Die Company ist in channelthing das höchste verbindende Element zwischen Coworkers. Daher befindet sich jeder Coworker während der channelthing-Nutzung in einem Company-Scope, d.h. es werden in allen Ansichten der Anwendung nur die Informationen angezeigt, die die jeweils ausgewählte Company betreffen, bis man sich zu einem bewussten Scope-Switch entscheidet und in eine andere Company wechselt.

Allerdings besitzt jeder Coworker genau einen channelthing-Login. Egal wie vielen Companies oder Channels er angehört - alle sind über ein globales Dashboard erreichbar.

<h3>Gemütlich quatschen in der Lounge</h3>
Jede Company besitzt beliebig viele Channels. Damit jedoch nicht für jedes Gesprächsthema ein neuer Channel gestartet werden muss, existiert für den gemütlichen Plausch zwischendurch die Company Lounge. Sie funktioniert genauso wie ein Channel auch, verbindet aber immer alle Mitglieder einer Company.

<h3>Projektbezogen arbeiten in Channels</h3>
Sie sind das Herzstück von channelthing. Hier treffen sich Coworker, um Themen- oder Projekt-bezogene Informationen zu sammeln, um Vorgehen zu planen, Termine zu finden, Dokumente oder Links auszutauschen und zu kommentieren. Wie bereits erwähnt müssen sie dabei nicht zwangsweise der ursprünglichen Company angehören, sondern können auch als "Externe" oder Freelancer in einem Channel mitarbeiten.

<a href="http://www.ipernity.com/doc/koos/4821995"><img src="http://u1.ipernity.com/11/19/95/4821995.a15d3564.500.jpg" width="500" height="333" alt="Channelthing channel view" border="0"/></a>

<h3>Agieren und reagieren</h3>
Ob in der Company-Lounge oder im Channel: Das Teilen von Informationen soll einfach wie möglich von der Hand gehen - und daher existiert dafür auch nur ein Textfeld, das allerdings ein bisschen schlauer ist als andere. Du kannst Coworker mit einen @ direkt ansprechen und damit zur Reaktion auffordern, mittels #hashtags werden Nachrichten direkt getagged und sind so anschließend über sie Suche auffindbar oder abonnierbar. Auch Orts-Informationen können über eine L:-Syntax gekennzeichnet werden. Links zu Bildern oder Videos werden natürlich interpretiert und Texte mit einem abschließendem Fragezeichen? als Frage an das Team deklariert.

<h3>Unlimited Uploads</h3>
Allein Textinformationen reichen natürlich meist nicht aus und channelthing erwartet es geradezu, dass du es mit Dokumenten fütterst. Lade mehrere Dateien auf einmal hoch und schreibe noch währenddessen einen kurzen Text dazu. Audio-Dateien werden anschließend in einem Player abspielbar und Bilder verkleinert angezeigt. Über eine gesicherte Verbindung können deine Coworker die Dateien auch herunterladen.

<h3>Suchen und filtern</h3>
Last but not least: die Suchfunktion. Was nutzt ein Informationsspeicher, wenn man an die Informationen nicht mehr herankommt? Aus dieser Überlegung heraus, legen wir auf die Such- und Filtermöglichkeiten besonders wert.

<a href="http://www.ipernity.com/doc/koos/4823678"><img src="http://u1.ipernity.com/11/36/78/4823678.4a06e4cc.500.jpg" width="500" height="49" alt="Channelthing - Filter" border="0"/></a>

Zurzeit sind "Coworker"- und "Message Type"-Filter sowie eine Volltextsuche vorhanden, in der Entwicklung befinden sich außerdem eine Indizierung und Volltextsuche von hochgeladenen Text-Dokumenten (z.B. PDF), sowie eine als Feed oder per E-Mail abonnierbare Suche über Tags/Coworker-Kombinationen.

<h3>It's all scriptified</h3>
JavaScript macht channelthing an vielen Ecken noch runder: Sei es der Hintergrund-Upload bei Dokumenten, das Einladen von Coworkern oder das Ändern von Company-Logos ohne Reload. Wir legen wert darauf, dass der kreative Arbeitsprozess nicht durch unnötige Kontextwechsel aus dem Fokus rückt.

Wenn dein Rechner allerdings aus Sicherheitsgründen kein JavaScript erlaubt: keine Sorge, bei uns läuft auch alles ohne.

<h3>Wann gehts los?</h3>
Das aktuelle alpha-Release liegt gerade auf unserem Staging-System und wird sich noch ein paar kritischen Tests unterziehen müssen. Vermissen wir noch eine Funktion? Wie fühlt es sich an? Um diese Fragen zu klären haben wir ein paar Leute aus unseren engsten Entwickler-Kreis eingeladen. 
Voraussichtlich in der nächsten Woche wird es dann soweit sein, dann werden wir auch weitere Einladungen rausschicken. Falls noch nicht gemacht, <a href="http://channelthing.com/" title="channelthing &alpha;">tragt euch am besten direkt in unseren Verteiler ein</a>!

<h2>One more thing... ;-)</h2>
Zusammen mit <a href="http://twitter.com/flxmllr">@flxmllr</a> werkeln wir gerade auch noch an einem iPhone-Client für channelthing. Seid gespannt!

(via <a href="http://blog.channelthing.com/2009/05/20/channelthing-a-big-picture/">Channelthing Blog</a>)
