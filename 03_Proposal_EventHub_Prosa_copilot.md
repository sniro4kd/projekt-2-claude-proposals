# Project Proposal: EventHub - Event-Management-Plattform (Copilot-Version)

## Projekteckdaten

Die CultureConnect GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung einer Event-Management-Plattform. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 30.000 Euro. Ansprechpartner ist Michael Braun (Product Owner). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von GitHub Copilot (Claude Haiku/Sonnet).

---

## 1. Ausgangssituation und Projektziel

Die CultureConnect GmbH organisiert kulturelle Veranstaltungen - Konzerte, Ausstellungen, Workshops. Aktuell werden Buchungen per Telefon und E-Mail abgewickelt, was zu ineffizienten Prozessen führt.

Ziel ist die Entwicklung einer Event-Management-Plattform, die den Prozess digitalisiert: von der Erstellung einer Veranstaltung über den Ticketverkauf bis zum Check-In am Einlass.

---

## 2. Fachlicher Hintergrund

Das System soll eine klassische Web-Architektur mit REST-API verwenden. Für Echtzeit-Updates (z.B. Ticket-Verfügbarkeit) kann SignalR eingesetzt werden.

---

## 3. Gewünschte Funktionalität

### Event-Verwaltung (Kernfunktionalität)

Veranstaltungen werden mit Titel, Beschreibung, Datum, Uhrzeit, Veranstaltungsort und maximaler Kapazität angelegt. Pro Veranstaltung können verschiedene Ticketkategorien definiert werden - Stehplatz, Sitzplatz.

Veranstaltungen haben Status: Entwurf, Veröffentlicht, Ausverkauft, Abgesagt.

### Ticketing und Buchung (Kernfunktionalität)

Besucher können Tickets online auswählen und buchen. Während des Checkouts werden Tickets für 10 Minuten reserviert.

Die Zahlungsabwicklung erfolgt über Stripe im Testmodus. Nach erfolgreicher Zahlung werden E-Tickets per E-Mail versendet mit QR-Code.

### Check-In (Kernfunktionalität)

Am Veranstaltungstag werden QR-Codes gescannt und gegen die Datenbank geprüft. Ein einmal gescanntes Ticket darf nicht erneut akzeptiert werden.

Statistiken zeigen, wie viele Besucher eingecheckt haben.

### Öffentliche Website (Kernfunktionalität)

Die Website zeigt alle kommenden Veranstaltungen. Besucher können nach Datum filtern. Responsives Design für Desktop und Mobile.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. PostgreSQL speichert alle Daten.

Das Frontend wird mit Vue.js 3 entwickelt.

E-Mail-Versand erfolgt über SendGrid (Sandbox-Modus), Zahlungen über Stripe (Testmodus).

Das System wird via Docker deployed.

---

## 5. Qualitätsanforderungen

Das System muss 20 gleichzeitige Buchungsvorgänge verarbeiten können. Race Conditions bei der Ticket-Reservierung müssen verhindert werden.

Buchungsbestätigung innerhalb von 10 Sekunden.

---

## 6. Dokumentations- und Testanforderungen

V-Modell-Standarddokumentation. Die Testdokumentation umfasst Unit- und Integrationstests.

Mindestens 20 Unit-Tests, 10 Integrationstests. Code-Coverage über 60%.

Ein einfacher Lasttest mit 20 gleichzeitigen Buchungen.

---

## 7. Vereinfachte Forschungskomponente

Das Team dokumentiert den Buchungsablauf (Reservierung -> Zahlung -> Ticketausstellung) und beschreibt, wie mit Fehlern umgegangen wird (z.B. Zahlung schlägt fehl -> Reservierung aufheben).

Ein Report von 4-5 Seiten beschreibt den Ablauf mit Sequenzdiagramm.

---

## Hinweis zur KI-Unterstützung

Dieses Projekt ist für die Bearbeitung mit GitHub Copilot (Claude Haiku/Sonnet) ausgelegt. Copilot unterstützt bei:
- Code-Vervollständigung und Boilerplate-Generierung
- Einfachen Debugging-Aufgaben
- Code-Erklärungen und Dokumentation

Die Studierenden müssen aktiv die Architekturentscheidungen treffen und den generierten Code verstehen und überprüfen.

---

Offenburg, den 13.01.2026

Lisa Hartmann
Geschäftsführerin CultureConnect GmbH
