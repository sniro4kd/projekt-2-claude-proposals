# Project Proposal: EventHub - Event-Management-Plattform

## Projekteckdaten

Die CultureConnect GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung einer Event-Management-Plattform. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 30.000 Euro. Ansprechpartner ist Michael Braun (Product Owner). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von KI-Assistenten.

---

## 1. Ausgangssituation und Projektziel

Die CultureConnect GmbH organisiert kulturelle Veranstaltungen in der Region - Konzerte, Ausstellungen, Workshops. Aktuell werden Buchungen per Telefon, E-Mail und über verschiedene externe Ticketing-Plattformen abgewickelt. Das führt zu einem ineffizienten Prozess mit vielen manuellen Schritten, Medienbrüchen und hohem Fehlerrisiko.

Ziel ist die Entwicklung einer integrierten Event-Management-Plattform, die den gesamten Prozess digitalisiert: von der Erstellung einer Veranstaltung über den Ticketverkauf und die Zahlungsabwicklung bis hin zum Check-In am Einlass und der Nachbereitung mit Statistiken.

---

## 2. Besondere Herausforderung: Event-Driven Architecture

Das System soll auf einer Event-Driven Architecture (EDA) basieren. Bei diesem Architekturansatz kommunizieren Komponenten nicht direkt miteinander, sondern über Ereignisse (Events), die in einer Message Queue publiziert werden.

Warum dieser Ansatz? Erstens erreicht man lose Kopplung zwischen Komponenten - der Buchungsservice muss nicht wissen, wer auf eine erfolgreiche Buchung reagiert. Zweitens ermöglicht es Echtzeit-Updates - wenn ein Ticket verkauft wird, kann das sofort auf dem Dashboard erscheinen. Drittens gewährleistet es Skalierbarkeit für Spitzenlasten, etwa wenn für ein beliebtes Konzert der Vorverkauf startet und hunderte Menschen gleichzeitig buchen wollen.

Event Sourcing bedeutet, dass nicht nur der aktuelle Zustand gespeichert wird, sondern alle Ereignisse, die zu diesem Zustand geführt haben. Bei einer Buchung wären das: TicketReserved, PaymentReceived, TicketIssued. Aus diesen Events lässt sich der Zustand jederzeit rekonstruieren.

---

## 3. Gewünschte Funktionalität

### Event-Verwaltung

Veranstaltungen werden mit allen relevanten Informationen angelegt: Titel, Beschreibung, Datum und Uhrzeit, Veranstaltungsort, maximale Kapazität. Pro Veranstaltung können verschiedene Ticketkategorien definiert werden - Stehplatz, Sitzplatz, VIP.

Die Preisgestaltung ist flexibel: Early-Bird-Preise für Frühbucher, reguläre Preise, Last-Minute-Angebote. Veranstaltungen durchlaufen verschiedene Status: Entwurf (noch nicht sichtbar), Veröffentlicht (buchbar), Ausverkauft, Abgesagt.

Wiederkehrende Veranstaltungen wie eine wöchentliche Jazz-Session sollten als Serie angelegt werden können. Bei Veranstaltungen mit Sitzplätzen wäre die Verwaltung eines Saalplans hilfreich. Der Import von Veranstaltungen aus externen Quellen im iCal-Format könnte die Datenpflege erleichtern.

### Ticketing und Buchung

Besucher können Tickets online auf der Website auswählen und buchen. Ein Warenkorb ermöglicht die Buchung mehrerer Tickets in einer Transaktion.

Während des Checkout-Prozesses werden die gewählten Tickets reserviert - für eine begrenzte Zeit, typischerweise 10 Minuten. Wenn die Zahlung nicht in dieser Zeit abgeschlossen wird, werden die Tickets wieder freigegeben. Dies verhindert, dass jemand den letzten Platz "blockiert" ohne zu kaufen.

Die Zahlungsabwicklung erfolgt über einen Payment-Provider wie Stripe oder PayPal - für das Projekt im Sandbox/Testmodus. Nach erfolgreicher Zahlung werden E-Tickets per E-Mail versendet, mit QR-Code für die Validierung am Einlass.

Für ausverkaufte Veranstaltungen wäre eine Warteliste sinnvoll - wenn jemand storniert, rückt der nächste auf der Liste nach. Gutschein-Codes für Rabattaktionen sind ein weiteres nützliches Feature.

### Check-In und Einlass

Am Veranstaltungstag benötigt das Personal eine Scanner-App, um Tickets zu validieren. QR-Codes werden gescannt und gegen die Datenbank geprüft: Ist das Ticket gültig? Wurde es bereits verwendet?

Der Replay-Schutz ist wichtig - ein einmal gescanntes Ticket darf nicht ein zweites Mal akzeptiert werden. Alle Check-Ins werden in Echtzeit an das Backend gemeldet.

Für den Fall, dass das Netzwerk am Einlass instabil ist, sollte eine Offline-Validierung mit späterer Synchronisation möglich sein. Live-Statistiken zeigen, wie viele Besucher bereits eingecheckt haben und wie viele noch erwartet werden (No-Shows).

### Benachrichtigungen

Das System versendet automatisch E-Mails: Buchungsbestätigung direkt nach dem Kauf, Erinnerung einige Tage vor der Veranstaltung (konfigurierbar), Information bei Absage oder Änderung.

Bei Absagen müssen alle Ticketinhaber benachrichtigt werden. E-Mail-Templates sollten anpassbar sein. Wenn durch eine Stornierung ein Platz frei wird, könnten Personen auf der Warteliste automatisch benachrichtigt werden. Web-Push-Benachrichtigungen wären eine Ergänzung für Browser-Nutzer.

### Reporting und Analytics

Veranstalter benötigen Einblick in ihre Zahlen: Wie viele Tickets wurden für welche Veranstaltung verkauft? In welchen Kategorien? Wie entwickelt sich der Verkauf über die Zeit?

Umsatzberichte zeigen die finanziellen Ergebnisse. Check-In-Raten zeigen, wie viele der verkauften Tickets auch eingelöst wurden - wichtig für die Planung von Catering und Personal. Verkaufstrends als Diagramme helfen beim Marketing. Export nach Excel oder CSV ermöglicht weitere Analysen.

### Öffentliche Website

Die öffentlich zugängliche Website zeigt alle kommenden Veranstaltungen. Besucher können nach Datum, Kategorie oder Ort filtern. Die Event-Detailseiten müssen SEO-optimiert sein, damit sie in Suchmaschinen gefunden werden.

Responsives Design ist Pflicht - viele Besucher nutzen Smartphones. Social-Media-Sharing-Buttons erleichtern die Verbreitung. Eine Suchfunktion rundet das Angebot ab.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. Als Message Broker kommt RabbitMQ zum Einsatz. Für Event Sourcing kann EventStoreDB oder PostgreSQL mit entsprechendem Schema verwendet werden.

Die "Read Database" (für schnelle Abfragen, nach dem CQRS-Pattern) ist PostgreSQL. Redis dient als Cache und für die temporäre Speicherung von Ticket-Reservierungen.

Das Frontend wird mit Vue.js 3 oder Nuxt 3 entwickelt - Nuxt ermöglicht Server-Side-Rendering für bessere SEO. Die Scanner-App ist eine PWA, die auch offline funktioniert.

E-Mail-Versand erfolgt über SendGrid oder Mailgun (im Sandbox-Modus), Zahlungen über Stripe (im Testmodus). Das System wird via Docker deployed.

---

## 5. Event-Driven Architecture im Detail

Das System muss mindestens folgende Domain Events implementieren: Ein Event wird angelegt (EventCreated), veröffentlicht (EventPublished), abgesagt (EventCancelled). Tickets werden reserviert (TicketReserved), die Reservierung läuft ab (TicketReservationExpired). Eine Buchung wird erstellt (BookingCreated), die Zahlung geht ein (PaymentReceived), das E-Ticket wird ausgestellt (TicketIssued). Am Einlass wird gescannt (CheckInProcessed). Bei Stornierung wird erstattet (RefundProcessed).

Event Handler müssen idempotent sein - das heißt, wenn dasselbe Event versehentlich zweimal verarbeitet wird, darf das keine unerwünschten Nebenwirkungen haben. Dead-Letter-Queues fangen fehlerhafte Nachrichten auf, die nicht verarbeitet werden konnten.

Das Saga Pattern koordiniert verteilte Transaktionen: Reservierung → Zahlung → Ticketausstellung. Wenn die Zahlung fehlschlägt, muss die Reservierung zurückgenommen werden (Kompensation).

---

## 6. Qualitätsanforderungen

Das System muss 500 gleichzeitige Buchungsvorgänge verarbeiten können - etwa beim Vorverkaufsstart eines populären Konzerts. Race Conditions bei der Ticket-Reservierung müssen verhindert werden - wenn nur noch ein Ticket übrig ist und zwei Personen gleichzeitig buchen, darf nur eine Buchung erfolgreich sein.

Die Buchungsbestätigung muss innerhalb von 5 Sekunden erfolgen. Das System sollte horizontal skalierbar sein, um bei Bedarf weitere Instanzen hinzuzufügen.

Garantierte Nachrichtenverarbeitung (at-least-once) stellt sicher, dass keine Events verloren gehen. Circuit Breaker schützen vor Kaskadenfehlern, wenn externe Services (Payment, E-Mail) nicht erreichbar sind.

---

## 7. Dokumentations- und Testanforderungen

Neben der V-Modell-Standarddokumentation ist eine Event Storming Dokumentation Pflicht - das Ergebnis des Workshops, in dem die Domain Events identifiziert wurden.

Die Testdokumentation umfasst spezielle Event-basierte Tests: Werden Events korrekt publiziert? Reagieren Handler korrekt? Sind Handler idempotent? Contract-Tests validieren, dass Event-Schemas eingehalten werden.

Lasttests sind kritisch: 500 gleichzeitige Buchungen müssen funktionieren. Chaos-Tests prüfen die Resilienz: Was passiert, wenn der Message Broker kurz ausfällt? Kann das System sich erholen?

---

## 8. Forschungskomponente: Event Storming und Saga Pattern

Das Team muss einen Event Storming Workshop durchführen. Im "Big Picture Event Storming" (2-3 Stunden) werden alle Domain Events identifiziert, Aggregates definiert und Bounded Contexts abgegrenzt. Im "Design Level Event Storming" (2-3 Stunden) werden Commands und Events verfeinert, Read Models identifiziert und Policies definiert.

Das Saga Pattern für die Buchungstransaktion muss implementiert und dokumentiert werden: die Schritte von der Reservierung über die Zahlung zur Ticketausstellung, die Kompensationslogik bei Fehlern, und das Timeout-Handling für abgelaufene Reservierungen. Ein Zustandsdiagramm visualisiert die möglichen Pfade und Fehlerszenarien.

---

Offenburg, den 13.01.2026

Lisa Hartmann
Geschäftsführerin CultureConnect GmbH
