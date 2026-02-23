# Project Proposal

| | |
|---|---|
| Firma | ERP_Champion GmbH |
| Projekt | DataPulse |
| Product Owner | Frank Niederbronn B.Sc. |
| Projektlaufzeit | März – Juni 2026 |
| Budget | 20.000 Euro |
| Version | 2.0 |
| Datum | 23.02.2026 |
| Dokumentenverantwortlicher | Frank Niederbronn |

---

Die Vertriebsabteilung von ERP_Champion GmbH arbeitet derzeit mit einer Vielzahl von Informationsquellen: Wetterdaten für die Logistikplanung, Finanzdaten für die Kalkulation, Nachrichtenfeeds für die Marktbeobachtung und interne Kennzahlen aus unseren eigenen Systemen. Bislang müssen die Mitarbeiter morgens ein halbes Dutzend verschiedene Webseiten und Tools öffnen, um sich einen Überblick zu verschaffen. Das kostet Zeit, ist fehleranfällig und führt dazu, dass wichtige Veränderungen zu spät bemerkt werden.

Wir wollen das ändern. **DataPulse** soll ein **browserbasiertes, konfigurierbares Echtzeit-Dashboard** werden, auf dem jeder Mitarbeiter sich die für ihn relevanten Informationsquellen individuell zusammenstellen kann. Das System soll Daten aus verschiedenen externen Quellen automatisch abrufen, aufbereiten und visuell darstellen. Bei bestimmten Schwellenwerten soll das System den Benutzer aktiv benachrichtigen, damit kritische Veränderungen nicht übersehen werden.

## Dashboard und Widget-System

Das zentrale Konzept von DataPulse ist ein **frei konfigurierbares Dashboard**, das aus einzelnen Widgets zusammengesetzt wird. Ein Widget ist ein visuelles Element, das eine bestimmte Information darstellt — etwa ein Liniendiagramm mit dem Temperaturverlauf der letzten 24 Stunden, eine Tabelle mit aktuellen Schlagzeilen oder eine einzelne große Zahl, die den aktuellen EUR/USD-Wechselkurs anzeigt.

Jeder Benutzer soll mehrere Dashboards anlegen können, die er frei benennt und zwischen denen er wechseln kann — beispielsweise ein „Morgen-Briefing"-Dashboard, ein „Logistik"-Dashboard und ein „Finanzen"-Dashboard. Innerhalb eines Dashboards sollen die Widgets per **Drag & Drop** frei angeordnet werden können. Die Widgets sollen in einem Raster-Layout platziert werden, wobei jedes Widget in seiner Größe veränderbar sein soll (mindestens die Unterscheidung zwischen klein, mittel und groß). Das Layout — also die Position, Größe und Konfiguration aller Widgets — muss persistent gespeichert werden, damit der Benutzer beim nächsten Login sein Dashboard genauso wiederfindet, wie er es verlassen hat.

An Widget-Typen sollen mindestens die folgenden zur Verfügung stehen: ein **Liniendiagramm** für zeitbasierte Verläufe, ein **Balkendiagramm** für Vergleiche, eine **Gauge-Anzeige** (Tachometer-artig) für einzelne Werte mit Skala, eine **Tabelle** für tabellarische Daten wie Nachrichtenlisten oder Aktienkurse, eine **Karte** (Map) für standortbezogene Daten wie Wetterstationen, und eine **Einzelwert-Anzeige** für prominente Kennzahlen wie den aktuellen Bitcoin-Kurs. Jedes Widget soll individuell konfigurierbar sein: Der Benutzer wählt die Datenquelle, den Zeitraum (wo relevant), Farben und Schwellenwerte. Jedes Widget soll einen visuellen Indikator haben, der anzeigt, wann die Daten zuletzt aktualisiert wurden.

Die Widgets sollen sich in einem konfigurierbaren Intervall automatisch aktualisieren, ohne dass die Seite neu geladen werden muss. Sinnvolle Intervall-Optionen wären 10 Sekunden, 30 Sekunden, 1 Minute und 5 Minuten — je nach Datenquelle und Bedarf. Bei der Aktualisierung darf die Benutzeroberfläche nicht einfrieren oder ruckeln; die Daten sollen im Hintergrund geladen und dann sanft in die bestehende Anzeige eingeblendet werden.

## Externe Datenquellen

Das System soll Daten von mindestens **drei verschiedenen externen APIs** beziehen. Wir stellen uns folgende Quellen vor, wobei das Entwicklungsteam nach Rücksprache auch Alternativen vorschlagen kann:

**Wetterdaten:** Aktuelle Wetterdaten und Vorhersagen für konfigurierbare Standorte. Dienste wie OpenWeatherMap bieten kostenlose API-Zugänge mit ausreichendem Kontingent für unsere Zwecke. Interessant für uns sind aktuelle Temperatur, Niederschlag, Wind und eine 5-Tage-Vorhersage. Ein Mitarbeiter in der Logistik könnte sich so ein Widget erstellen, das ihm das Wetter an den Standorten der wichtigsten Auslieferungslager anzeigt.

**Finanzdaten:** Wechselkurse und nach Möglichkeit auch Aktienkurse. Dienste wie die Frankfurter Exchangerates API oder Alpha Vantage bieten kostenlose Zugänge. Für unsere internationalen Vertriebsmitarbeiter ist es wichtig, die wichtigsten Wechselkurse (EUR/USD, EUR/GBP, EUR/CHF) im Blick zu haben und bei größeren Veränderungen benachrichtigt zu werden.

**Nachrichtenfeeds:** Aktuelle Schlagzeilen zu konfigurierbaren Themen oder Branchen. Dienste wie NewsAPI.org oder GNews liefern strukturierte Nachrichtendaten. Ein Mitarbeiter könnte sich ein Widget einrichten, das Nachrichten zu einem bestimmten Branchenstichwort zeigt — etwa „Automotive" oder „Supply Chain".

Darüber hinaus wäre es wünschenswert, wenn das Team eine vierte Datenquelle eigener Wahl integriert — etwa GitHub-Repository-Statistiken für das Entwicklungsteam, öffentliche Verkehrsdaten, Luftqualitätsdaten oder ähnliches.

Eine wesentliche Herausforderung bei der Integration externer APIs ist der Umgang mit **Rate Limits**. Die meisten kostenlosen API-Pläne erlauben nur eine begrenzte Anzahl von Anfragen pro Minute oder pro Tag. Das System muss daher eine **Caching-Schicht** implementieren, die API-Antworten zwischenspeichert und nur bei Bedarf neue Anfragen stellt. Die Cache-Dauer soll pro Datenquelle konfigurierbar sein — Wetterdaten ändern sich beispielsweise nur alle 10–30 Minuten, während Finanzdaten häufiger aktualisiert werden sollten.

Ebenso muss das System robust mit **API-Ausfällen** umgehen. Wenn eine externe API nicht erreichbar ist oder Fehler liefert, darf das nicht zum Absturz des gesamten Dashboards führen. Stattdessen soll das betroffene Widget die zuletzt verfügbaren Daten mit einem Hinweis „Letzte Aktualisierung: vor X Minuten — Datenquelle derzeit nicht erreichbar" anzeigen und im Hintergrund erneut versuchen, die Daten abzurufen. Wichtig ist, dass API-Schlüssel niemals im Frontend-Code sichtbar sein dürfen — alle externen API-Aufrufe müssen über das Backend als Proxy laufen.

## Alerting und Benachrichtigungen

Ein besonders wichtiges Feature für unsere Vertriebsmitarbeiter ist die Möglichkeit, **Schwellenwert-basierte Benachrichtigungen** einzurichten. Für jedes Widget, das einen numerischen Wert darstellt, soll der Benutzer Regeln definieren können — beispielsweise „Benachrichtige mich, wenn der EUR/USD-Kurs unter 1,05 fällt" oder „Benachrichtige mich, wenn die Temperatur am Standort München über 35°C steigt".

Wenn ein Schwellenwert überschritten wird, soll der Benutzer auf zwei Wegen benachrichtigt werden: erstens über eine **Browser-Push-Notification**, die auch erscheint, wenn der Benutzer gerade einen anderen Tab geöffnet hat, und zweitens optional per **E-Mail**, falls der Benutzer diese Option aktiviert hat. Jeder Benutzer soll eine **Alert-Historie** einsehen können, die die letzten Benachrichtigungen mit Zeitstempel, ausgelöstem Schwellenwert und aktuellem Wert auflistet.

Es muss darauf geachtet werden, dass das Alerting-System nicht ständig dieselbe Benachrichtigung verschickt, wenn ein Wert dauerhaft über dem Schwellenwert liegt. Eine sinnvolle Lösung wäre, dass ein Alert erst dann erneut ausgelöst wird, wenn der Wert zwischenzeitlich wieder unter den Schwellenwert gefallen ist und ihn dann erneut überschreitet — oder alternativ nach einer konfigurierbaren Cooldown-Periode.

## Benutzerverwaltung und Sicherheit

DataPulse soll eine **Benutzerregistrierung** mit E-Mail-Adresse und Passwort bieten. Das Passwort muss serverseitig sicher gehasht werden — Klartext-Speicherung ist selbstverständlich ausgeschlossen. Es sollen gängige Passwortregeln durchgesetzt werden (Mindestlänge, Kombination aus Groß-/Kleinbuchstaben und Zahlen). Die Session-Verwaltung soll so gestaltet sein, dass ein Benutzer nach dem Login für eine angemessene Dauer (z.B. 24 Stunden) eingeloggt bleibt, ohne sich ständig neu anmelden zu müssen, aber gleichzeitig inaktive Sessions automatisch ablaufen.

Da jeder Benutzer seine Dashboard-Konfigurationen und Alert-Regeln auf dem Server speichert, ist eine saubere Trennung der Benutzerdaten essenziell — kein Benutzer darf die Daten eines anderen einsehen oder verändern können. Das System soll gegen gängige Angriffsvektoren geschützt sein, insbesondere Cross-Site Scripting (XSS), Cross-Site Request Forgery (CSRF) und SQL Injection. Da die Nachrichten aus externen Quellen vom Benutzer nicht kontrolliert werden können, muss besonderes Augenmerk auf die Sanitization von angezeigten Inhalten gelegt werden.

Darüber hinaus muss das System DSGVO-konform sein: Jeder Benutzer soll seine eigenen Daten exportieren und auf Wunsch vollständig löschen können — einschließlich aller gespeicherten Dashboard-Konfigurationen, Alert-Regeln und der Alert-Historie.

## Gestaltung und Benutzeroberfläche

Die Oberfläche soll professionell und modern wirken — schließlich wird sie im Arbeitsalltag genutzt und muss auf den ersten Blick übersichtlich und nicht überladen sein. Ein dunkles und ein helles Farbschema (Dark Mode / Light Mode) wären wünschenswert, da viele Mitarbeiter den Dark Mode bevorzugen, insbesondere wenn sie das Dashboard den ganzen Tag geöffnet haben. Das Branding von ERP_Champion (Logo, Primärfarben) soll dezent eingebunden sein.

Auf dem **Desktop** soll das volle Dashboard mit allen Drag & Drop-Funktionen verfügbar sein. Auf **Tablets** soll zumindest eine Nur-Lese-Ansicht des Dashboards möglich sein, auch wenn Drag & Drop dort eingeschränkt sein darf. Auf **Smartphones** soll es eine vereinfachte Ansicht geben, die die Widgets untereinander in einer einspaltigen Liste darstellt. Wenn eine vollwertige Smartphone-Unterstützung den Rahmen sprengen würde, soll zumindest ein freundlicher Hinweis erscheinen, der auf die Desktop-Version verweist.

## Architektur

```
┌───────────────────────────────────────────────────────────────┐
│                     Browser (Client)                          │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │             SPA (Vue / React / etc.)                    │  │
│  │  ┌────────────┐ ┌────────────┐ ┌────────────────────┐  │  │ 
│  │  │ Dashboard  │ │  Widget-   │ │ Alert-Verwaltung   │  │  │ 
│  │  │ Canvas     │ │  Konfig.   │ │ + Historie         │  │  │ 
│  │  │ (Drag&Drop)│ │  Panel     │ │                    │  │  │ 
│  │  └────────────┘ └────────────┘ └────────────────────┘  │  │ 
│  │        │              │               │                │  │ 
│  │        └──────────────┴───────────────┘                │  │ 
│  │                       │                                │  │ 
│  │             Service Worker (Push)                      │  │ 
│  └───────────────────────┼────────────────────────────────┘  │ 
│                          │                                   │ 
│                      REST API                                │ 
└──────────────────────────┼────────────────────────────────────┘
                           │                                     
                           ▼                                     
┌───────────────────────────────────────────────────────────────┐
│                   Application Server                          │
│                                                               │
│  ┌──────────────────┐  ┌──────────────────┐                  │ 
│  │ REST Controller  │  │  Alert Engine    │                  │ 
│  │ (Dashboard CRUD, │  │  (Schwellenwert- │                  │ 
│  │  Auth, Profile)  │  │   Überwachung,   │                  │ 
│  │                  │  │   Notifications) │                  │ 
│  └────────┬─────────┘  └────────┬─────────┘                  │ 
│           │                     │                             │
│           ▼                     ▼                             │
│  ┌──────────────────────────────────────────┐                 │
│  │         API-Proxy & Cache                │                 │
│  │  (Rate-Limit-Management, Retry-Logik,   │                 │ 
│  │   Fehlerbehandlung, TTL-basierter Cache) │                 │
│  └──────────┬──────────────┬───────────────┘                 │ 
│             │              │                                  │
│     ┌───────┘              └───────┐                          │
│     ▼                              ▼                          │
│  ┌──────────────┐       ┌──────────────────────┐              │
│  │  Datenbank   │       │  Externe APIs        │              │
│  │  (Benutzer,  │       │  (Wetter, Finanzen,  │              │
│  │   Dashboards,│       │   Nachrichten, ...)  │              │
│  │   Alerts)    │       │                      │              │
│  └──────────────┘       └──────────────────────┘              │
└───────────────────────────────────────────────────────────────┘
```

Besonders wichtig ist die **API-Proxy-Schicht** im Backend: Alle externen API-Aufrufe laufen über den Server, nicht direkt vom Browser. Dadurch werden API-Schlüssel geschützt, Rate Limits zentral verwaltet und Caching effizient umgesetzt. Die Alert Engine läuft als Hintergrundprozess, der bei jeder Datenaktualisierung prüft, ob Schwellenwerte überschritten wurden, und gegebenenfalls Benachrichtigungen auslöst.

## Deployment und Betrieb

Das gesamte System soll über Docker containerisiert und per `docker-compose` startbar sein. Unsere Kunden sollen DataPulse bei Bedarf auch auf eigenen Servern betreiben können. Daher ist eine saubere Konfiguration über Umgebungsvariablen wichtig — insbesondere für API-Schlüssel, Datenbankverbindung und SMTP-Zugangsdaten. Eine verständliche Installationsanleitung ist Teil der erwarteten Liefergegenstände.

Für den E-Mail-Versand soll das System über SMTP konfigurierbar sein. Für die Entwicklungs- und Testphase empfehlen wir einen Dienst wie Mailtrap, der E-Mails abfängt und in einer Weboberfläche anzeigt, anstatt sie wirklich zu versenden.

## Qualität und Tests

Das System soll mit einer gründlichen Teststrategie entwickelt werden. Insbesondere erwarten wir, dass die Fehlerbehandlung für externe APIs sorgfältig getestet wird — was passiert, wenn eine API ein unerwartetes Format zurückliefert? Was, wenn sie eine 429 (Too Many Requests) zurückgibt? Was, wenn sie gar nicht erreichbar ist? Diese Szenarien sollen durch Mock-basierte Tests abgedeckt sein.

Das Alerting-System muss zuverlässig und korrekt sein — ein fehlender oder ein falscher Alert kann für unsere Vertriebsmitarbeiter ernsthafte Konsequenzen haben. Daher erwarten wir hier eine besonders hohe Testabdeckung.

Die allgemeine Code-Coverage soll mindestens 70% betragen. Die Performance soll so sein, dass ein Dashboard mit 10 Widgets innerhalb von 3 Sekunden vollständig geladen ist.

Bugfixing und neue Features sollen später von unseren hauseigenen Entwicklern gemacht werden. Daher ist sauberer, gut strukturierter und gut dokumentierter Code essenziell. Die API soll über Swagger/OpenAPI dokumentiert sein.

Um trotz des recht geringen Budgets ein passendes Produkt zu erstellen, sollen Werkstudenten dies komplett umsetzen. HR empfiehlt hier Studierende des Studienganges AI von der HS Offenburg, da nur diese über die fachliche Tiefe verfügen.

---

Projekt genehmigt:

Offenburg, den 23.02.2026

*\_\_\_\_Jack Berlinthal\_\_\_\_\_*

ERP_Champion GmbH
Dr. Jack Berlinthal
CEO / CIO ERP_Champion GmbH
