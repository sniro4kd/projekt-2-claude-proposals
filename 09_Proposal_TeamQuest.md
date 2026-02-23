# Project Proposal

| | |
|---|---|
| Firma | ERP_Champion GmbH |
| Projekt | TeamQuest |
| Product Owner | Frank Niederbronn B.Sc. |
| Projektlaufzeit | März – Juni 2026 |
| Budget | 20.000 Euro |
| Version | 2.0 |
| Datum | 23.02.2026 |
| Dokumentenverantwortlicher | Frank Niederbronn |

---

ERP_Champion GmbH plant, das eigene Kundenportal um eine interaktive Teambuilding-Komponente zu erweitern. Hintergrund ist, dass unsere Unternehmenskunden zunehmend nach digitalen Möglichkeiten fragen, um verteilte Teams zusammenzubringen — insbesondere seit der Zunahme von Remote-Arbeit. Unser Vertrieb hat in Kundengesprächen wiederholt den Wunsch nach einem „spielerischen Element" gehört, das Teams nutzen können, um Zusammenarbeit und Kommunikation zu üben. Daraus entstand die Idee für **TeamQuest**: ein browserbasiertes kooperatives Rätselspiel, das in Echtzeit von mehreren Spielern gemeinsam gespielt wird.

## Spielkonzept und Ablauf

Das Grundprinzip von TeamQuest basiert auf **asymmetrischer Information**. Das bedeutet: In jeder Spielrunde sieht jeder Spieler nur einen Teil der für die Lösung notwendigen Informationen. Kein einzelner Spieler kann ein Rätsel allein lösen — nur durch aktive Kommunikation und Kooperation im Team gelingt es, die Aufgaben zu bewältigen. Das Spiel ist damit bewusst als Teamübung konzipiert und nicht als kompetitives Gegeneinander.

Ein typischer Spielablauf sieht folgendermaßen aus: Ein Spieler erstellt einen neuen Spielraum und erhält dafür einen sechsstelligen Raum-Code, den er an seine Mitspieler weitergibt. Diese treten dem Raum über die Eingabe des Codes bei. In der Lobby sehen alle verbundenen Spieler, wer bereits im Raum ist und wer sich als „bereit" markiert hat. Das Spiel kann gestartet werden, sobald mindestens zwei und maximal vier Spieler im Raum sind und alle den Bereitschaftsstatus gesetzt haben. Der Raum-Ersteller fungiert dabei als Host und kann die Spieleinstellungen konfigurieren — insbesondere das Zeitlimit pro Runde, wobei Optionen von 5, 10 und 15 Minuten zur Verfügung stehen sollten, sowie den Schwierigkeitsgrad.

Jede Spielrunde besteht aus einer Abfolge von drei bis fünf Rätseln steigender Schwierigkeit. Zwischen den Rätseln soll ein kurzer Übergangsbildschirm angezeigt werden, der den bisherigen Fortschritt des Teams visualisiert. Am Ende einer Runde wird die Gesamtperformance angezeigt: wie viele Rätsel gelöst wurden, wie lange das Team insgesamt gebraucht hat und wie effizient die Kommunikation war (gemessen an der Anzahl der Chat-Nachrichten im Verhältnis zur Lösungsgeschwindigkeit).

## Rätseltypen

Zum Launch sollen mindestens drei grundlegend verschiedene Rätseltypen implementiert werden, die jeweils unterschiedliche Formen der Zusammenarbeit erfordern:

**Symbolrätsel:** Bei diesem Typ sieht ein Teil der Spieler eine Anordnung von abstrakten Symbolen auf einem Gitter, während die anderen Spieler eine Legende besitzen, die jedem Symbol eine Zahl, einen Buchstaben oder eine Farbe zuordnet. Das Team muss gemeinsam über den Chat kommunizieren, um einen Code zu entschlüsseln. Die Symbole und deren Zuordnungen sollen bei jedem Spiel zufällig generiert werden, damit sich Lösungen nicht einfach merken oder nachschlagen lassen. Die Komplexität kann über die Anzahl der Symbole und die Länge des zu entschlüsselnden Codes gesteuert werden — bei leichteren Schwierigkeitsgraden sind es beispielsweise 4 Symbole und ein 3-stelliger Code, bei höheren bis zu 8 Symbole und ein 6-stelliger Code.

**Kooperatives Labyrinth:** Hier sieht ein Spieler — der „Navigator" — den vollständigen Grundriss eines Labyrinths von oben, kann aber die Position der Spielfigur nicht sehen. Ein anderer Spieler — der „Pilot" — steuert die Spielfigur und sieht seine unmittelbare Umgebung (einen Ausschnitt von wenigen Feldern um sich herum), aber nicht den Gesamtplan. Zusätzlich gibt es Hindernisse und Fallen im Labyrinth, die nur der Pilot sehen kann, während Schlüssel und Türen nur auf der Karte des Navigators eingezeichnet sind. Bei mehr als zwei Spielern erhalten zusätzliche Spieler die Rolle von „Spähern", die jeweils nur bestimmte Bereiche des Labyrinths einsehen können und beispielsweise Hinweise zu Fallen geben. Das Labyrinth soll bei jedem Spiel prozedural generiert werden, wobei sichergestellt sein muss, dass ein Lösungsweg existiert. Die Spielfigur wird über die Pfeiltasten oder WASD gesteuert, und die Bewegung soll in Echtzeit für alle sichtbar sein — der Navigator sieht die Position des Piloten auf seiner Karte, und die Späher sehen die Figur in ihren jeweiligen Ausschnitten.

**Logik-Puzzle (Einstein-Rätsel-Variante):** Bei diesem Rätseltyp erhält jeder Spieler eine andere Teilmenge von Hinweisen, die zusammen die Lösung eines kombinatorischen Logikproblems ergeben. Beispielsweise: „Es gibt fünf Häuser in einer Reihe, jedes hat eine andere Farbe, einen anderen Bewohner und ein anderes Haustier." Ein Spieler weiß, dass „der Bewohner des roten Hauses einen Hund hat", ein anderer weiß, dass „das blaue Haus links vom grünen steht", und so weiter. Kein Spieler hat genug Informationen, um das Rätsel allein zu lösen. Die Hinweise sollen so generiert werden, dass das Rätsel eine eindeutige Lösung hat — dies erfordert einen Generierungsalgorithmus, der zunächst eine gültige Lösung erzeugt und daraus Hinweise ableitet. Die Spieler geben ihre gemeinsame Lösung in eine tabellarische Eingabeoberfläche ein, die anzeigt, welche Felder bereits ausgefüllt sind.

Es wäre wünschenswert, dass in Zukunft weitere Rätseltypen ergänzt werden können, ohne die bestehende Architektur grundlegend umbauen zu müssen. Die Rätsel-Logik sollte daher sauber von der Darstellungsschicht und der Kommunikationsschicht getrennt sein.

## Kommunikation und Echtzeit

Ein zentrales Element des Spiels ist die Kommunikation zwischen den Spielern. Da das Spiel auf asymmetrischer Information basiert, ist ein **integrierter Echtzeit-Textchat** unverzichtbar. Der Chat soll als seitliches Panel neben dem Spielfeld angezeigt werden und während des gesamten Spiels sichtbar sein. Nachrichten sollen in Echtzeit bei allen Spielern im Raum erscheinen — eine Verzögerung von mehr als ein bis zwei Sekunden wäre für das Spielerlebnis inakzeptabel.

Die Echtzeit-Synchronisation betrifft aber nicht nur den Chat, sondern alle spielrelevanten Aktionen. Wenn ein Spieler eine Figur bewegt, einen Code eingibt oder ein Rätsel löst, muss dies sofort bei allen anderen Spielern sichtbar sein. Der Server soll dabei die **zentrale Autorität** über den Spielzustand sein — das heißt, kein Client darf eigenständig den Spielstatus verändern, sondern alle Aktionen werden an den Server gesendet, dort validiert und dann an alle Clients verteilt. Dies ist wichtig, um Inkonsistenzen zu vermeiden, wenn beispielsweise zwei Spieler gleichzeitig den letzten Teil eines Codes eingeben.

Uns ist bewusst, dass bei einer Web-Applikation Verbindungsabbrüche vorkommen können — sei es durch instabiles WLAN, Mobilfunk oder einfach durch einen kurzzeitig geschlossenen Browser-Tab. Für solche Fälle sollte ein Reconnect-Mechanismus vorhanden sein: Wenn ein Spieler die Verbindung verliert, sollte er innerhalb eines angemessenen Zeitfensters (etwa 60 Sekunden) wieder beitreten können, ohne dass das Spiel für die anderen Spieler unterbrochen wird. Die verbleibenden Spieler sollten sehen, dass ein Mitspieler die Verbindung verloren hat, und das Zeitlimit sollte in dieser Phase pausiert werden. Wenn der Spieler nicht rechtzeitig zurückkehrt, soll das Spiel trotzdem fortgesetzt werden können.

## Bestenliste und Spielerprofile

Jeder Spieler soll beim erstmaligen Betreten der Anwendung einen Nickname wählen können — eine vollständige Benutzerregistrierung mit E-Mail und Passwort ist für den Moment nicht vorgesehen, da das Spiel niederschwellig zugänglich sein soll. Der Nickname wird im Browser gespeichert und beim nächsten Besuch wiederverwendet.

Es soll eine persistente **Bestenliste** geführt werden, die Teams nach ihrer Gesamtlösungszeit über alle Rätsel einer Runde sortiert. Die schnellsten Teams stehen oben. Die Bestenliste soll den Team-Namen (den der Host beim Erstellen des Raums festlegen kann), die Namen der Mitspieler, die Lösungszeit und den gespielten Schwierigkeitsgrad anzeigen. Es soll nach Schwierigkeitsgrad gefiltert werden können, damit Teams sich mit anderen vergleichen können, die unter gleichen Bedingungen gespielt haben.

## Gestaltung und Benutzeroberfläche

Die Benutzeroberfläche soll modern und ansprechend gestaltet sein, aber gleichzeitig klar und aufgeräumt, damit der Fokus auf dem Spielgeschehen bleibt. Das Branding von ERP_Champion soll erkennbar sein — Logo im Header, Unternehmensfarben als Akzente — aber das Spiel soll nicht wie eine Unternehmensanwendung wirken, sondern Spaß machen. Die Zielgruppe sind Erwachsene in einem beruflichen Kontext, keine Kinder.

Das Layout soll auf Desktops und Tablets funktionieren. Auf dem Desktop ist das Spielfeld im Zentrum, der Chat rechts daneben und die Spielerinformationen (verbundene Spieler, Countdown, Fortschritt) oben. Auf Tablets soll der Chat über einen ausklappbaren Bereich erreichbar sein, damit das Spielfeld den vollen Bildschirm nutzen kann. Eine Smartphone-Version ist aufgrund der Komplexität der Rätseldarstellung vorerst nicht vorgesehen — es wäre aber gut, wenn Smartphone-Nutzer zumindest einen freundlichen Hinweis bekommen, dass die Anwendung auf einem größeren Bildschirm besser funktioniert.

## Architektur

Die Architektur soll sich an unserem bestehenden Technologie-Stack orientieren, damit unsere hauseigenen Entwickler das Produkt später weiterentwickeln und warten können. Auf der Client-Seite soll eine moderne Single-Page-Application im Browser laufen, die über eine bidirektionale Echtzeit-Verbindung mit dem Server kommuniziert. Für spielrelevante Echtzeitdaten (Spielzüge, Chat, Statusupdates) soll eine WebSocket-basierte Verbindung genutzt werden. Für nicht-zeitkritische Operationen wie das Laden der Bestenliste oder die Lobby-Verwaltung genügt eine klassische REST-API.

Die folgende Skizze zeigt den geplanten Aufbau:

```
┌──────────────────────────────────────────────────────────┐
│                   Browser (Client)                       │
│  ┌────────────────────────────────────────────────────┐  │
│  │           SPA (Vue / React / etc.)                 │  │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────────────┐   │  │ 
│  │  │Spielfeld │ │  Chat    │ │ Lobby / Liste    │   │  │ 
│  │  └──────────┘ └──────────┘ └──────────────────┘   │  │ 
│  └──────────┬─────────────┬───────────────────────────┘  │
│             │             │                              │
│        WebSocket      REST API                           │
└─────────────┼─────────────┼──────────────────────────────┘
              │             │                               
              ▼             ▼                               
┌──────────────────────────────────────────────────────────┐
│                  Application Server                      │
│                                                          │
│  ┌────────────────┐    ┌─────────────────────┐           │
│  │ WebSocket Hub  │    │  REST Controller    │           │
│  │ (Echtzeit-     │    │  (Lobby, Besten-    │           │
│  │  Kommunikation)│    │   liste, Profil)    │           │
│  └───────┬────────┘    └──────────┬──────────┘           │
│          │                        │                      │
│          ▼                        ▼                      │
│  ┌────────────────────────────────────────────────┐      │
│  │             Game Engine                        │      │
│  │  ┌─────────────┐  ┌────────────────────┐      │      │ 
│  │  │Room Manager │  │ Rätsel-Generator  │      │      │  
│  │  │(Lobby,      │  │ (Prozedural,       │      │      │ 
│  │  │ Sessions)   │  │  Plugin-fähig)     │      │      │ 
│  │  └─────────────┘  └────────────────────┘      │      │ 
│  └───────────────────────┬────────────────────────┘      │
│                          │                               │
│                          ▼                               │
│  ┌────────────────────────────────────────────────┐      │
│  │          Persistenzschicht                     │      │
│  │       (Bestenliste, Spielstände)               │      │
│  └────────────────────────────────────────────────┘      │
└──────────────────────────────────────────────────────────┘
```

Der Application Server hält die laufenden Spielräume im Arbeitsspeicher, da die Latenzanforderungen für Echtzeitspiele einen Datenbankzugriff bei jedem Spielzug nicht erlauben. Erst am Ende eines Spiels werden die Ergebnisse in die Datenbank geschrieben. Die Rätsel-Generierung soll als austauschbare Komponente entworfen werden, damit neue Rätseltypen später ergänzt werden können, ohne die übrige Architektur zu verändern.

## Deployment und Betrieb

Das System soll mittels Docker containerisiert werden, sodass es über ein einfaches `docker-compose up` gestartet werden kann. Dies umfasst sowohl den Application Server als auch die Datenbank und den Webserver für die Auslieferung des Frontends. Unsere Kunden sollen das Spiel bei Bedarf auch auf eigenen Servern hosten können, daher ist eine unkomplizierte Installation wichtig. Eine Dokumentation für den Betrieb (README mit Schritt-für-Schritt-Anleitung) ist Teil der erwarteten Liefergegenstände.

## Qualität und Tests

Es sollte nochmals gesondert untersucht werden, ob die prozedural generierten Rätsel stets lösbar und ausgewogen sind. Insbesondere beim Logik-Puzzle muss sichergestellt werden, dass die generierten Hinweise eine eindeutige Lösung ergeben. Beim Labyrinth muss garantiert sein, dass ein Pfad vom Start zum Ziel existiert. Wir erwarten, dass die Qualität der Rätselgenerierung durch automatisierte Tests (z.B. Simulation von 1000 generierten Rätseln auf Lösbarkeit) nachgewiesen wird.

Da das Spiel von Teams in einem professionellen Umfeld genutzt wird, ist Zuverlässigkeit wichtig. Der Algorithmus zur Generierung der Rätsel darf nicht länger als 2 Sekunden benötigen. WebSocket-Verbindungen müssen stabil über die gesamte Dauer einer Spielrunde gehalten werden. Das System sollte mindestens 10 gleichzeitige Spielräume mit je 4 Spielern unterstützen, ohne dass die Performance spürbar einbricht.

Bugfixing und neue Features sollen später von unseren hauseigenen Entwicklern gemacht werden. Daher ist sauberer, gut dokumentierter und testbarer Code wichtiger als eine maximale Feature-Menge. Lieber weniger Features, die robust funktionieren, als viele halbfertige.

Um trotz des recht geringen Budgets ein passendes Produkt zu erstellen, sollen Werkstudenten dies komplett umsetzen. HR empfiehlt hier Studierende des Studienganges AI von der HS Offenburg, da nur diese über die fachliche Tiefe verfügen.

---

Projekt genehmigt:

Offenburg, den 23.02.2026

*\_\_\_\_Jack Berlinthal\_\_\_\_\_*

ERP_Champion GmbH
Dr. Jack Berlinthal
CEO / CIO ERP_Champion GmbH
