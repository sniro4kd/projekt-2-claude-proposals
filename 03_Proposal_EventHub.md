# Project Proposal: EventHub - Event-Management-Plattform

---

| Eigenschaft | Wert |
|-------------|------|
| **Firma** | CultureConnect GmbH |
| **Projekt** | EventHub |
| **Product Owner** | Michael Braun |
| **Projektlaufzeit** | März - Juli 2026 |
| **Budget** | 30.000 Euro |
| **Version** | 1.0 |
| **Datum** | 13.01.2026 |
| **Zielgruppe** | 6-7 Studierende, 4.-6. Semester Angewandte Informatik |
| **Aufwand pro Person** | 30-40 Stunden (mit KI-Assistenten) |

---

## 1. Projektbeschreibung

### 1.1 Hintergrund

Die CultureConnect GmbH organisiert kulturelle Veranstaltungen (Konzerte, Ausstellungen, Workshops) in der Region. Aktuell werden Buchungen per Telefon, E-Mail und verschiedene Ticketing-Plattformen abgewickelt - ein ineffizienter Prozess mit vielen manuellen Schritten.

Es soll eine **Event-Management-Plattform** entwickelt werden, die den gesamten Prozess von der Veranstaltungserstellung bis zur Nachbereitung digitalisiert.

### 1.2 Besondere Herausforderung: Event-Driven Architecture

Das System soll auf einer **Event-Driven Architecture (EDA)** basieren, um:
- Lose Kopplung zwischen Komponenten zu erreichen
- Echtzeit-Updates zu ermöglichen
- Skalierbarkeit für Spitzenlasten (Ticketverkauf) zu gewährleisten
- Externe Systeme einfach integrieren zu können

---

## 2. Funktionale Anforderungen

### 2.1 Event-Verwaltung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-101 | Das System MUSS Veranstaltungen mit Titel, Beschreibung, Datum, Ort, Kapazität anlegen | Muss |
| FA-102 | Das System MUSS verschiedene Ticketkategorien pro Event unterstützen | Muss |
| FA-103 | Das System MUSS Preise pro Kategorie und Zeitraum (Early Bird, Regular, Last Minute) verwalten | Muss |
| FA-104 | Das System MUSS Events als Entwurf, Veröffentlicht, Ausverkauft, Abgesagt markieren | Muss |
| FA-105 | Das System MUSS wiederkehrende Events (Serien) unterstützen | Soll |
| FA-106 | Das System SOLL Veranstaltungsorte mit Saalplan verwalten | Soll |
| FA-107 | Das System KANN Events aus externen Quellen importieren (iCal) | Kann |

### 2.2 Ticketing und Buchung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-201 | Das System MUSS Tickets online buchbar machen | Muss |
| FA-202 | Das System MUSS einen Warenkorb für mehrere Tickets bieten | Muss |
| FA-203 | Das System MUSS Tickets reservieren während des Checkout (10 Min Timeout) | Muss |
| FA-204 | Das System MUSS Zahlungen über einen Payment-Provider abwickeln (Stripe/PayPal Sandbox) | Muss |
| FA-205 | Das System MUSS nach Zahlung E-Tickets per E-Mail versenden | Muss |
| FA-206 | Das System MUSS QR-Codes für Ticket-Validierung generieren | Muss |
| FA-207 | Das System SOLL Wartelisten für ausverkaufte Events bieten | Soll |
| FA-208 | Das System SOLL Gutschein-Codes unterstützen | Soll |
| FA-209 | Das System KANN Sitzplatzauswahl bei Saalplan-Events bieten | Kann |

### 2.3 Check-In und Einlass

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-301 | Das System MUSS eine Check-In App für Scanner-Personal bieten | Muss |
| FA-302 | Das System MUSS QR-Codes scannen und validieren können | Muss |
| FA-303 | Das System MUSS bereits verwendete Tickets erkennen (Replay-Schutz) | Muss |
| FA-304 | Das System MUSS Check-Ins in Echtzeit an das Backend melden | Muss |
| FA-305 | Das System SOLL Offline-Validierung mit Sync unterstützen | Soll |
| FA-306 | Das System SOLL Einlass-Statistiken live anzeigen | Soll |

### 2.4 Benachrichtigungen und Kommunikation

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-401 | Das System MUSS Bestätigungs-E-Mails bei Buchung senden | Muss |
| FA-402 | Das System MUSS Erinnerungs-E-Mails vor dem Event senden (konfigurierbar) | Muss |
| FA-403 | Das System MUSS bei Absage alle Ticketinhaber benachrichtigen | Muss |
| FA-404 | Das System SOLL E-Mail-Templates anpassbar machen | Soll |
| FA-405 | Das System SOLL Wartelisten-Benachrichtigungen bei Stornierung senden | Soll |
| FA-406 | Das System KANN Push-Benachrichtigungen über Web Push senden | Kann |

### 2.5 Reporting und Analytics

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-501 | Das System MUSS Verkaufszahlen pro Event anzeigen | Muss |
| FA-502 | Das System MUSS Umsatzberichte generieren | Muss |
| FA-503 | Das System MUSS Check-In-Raten anzeigen (no-shows) | Muss |
| FA-504 | Das System SOLL Verkaufstrends visualisieren (Diagramme) | Soll |
| FA-505 | Das System SOLL Export nach Excel/CSV bieten | Soll |
| FA-506 | Das System KANN A/B-Test Ergebnisse für Marketing auswerten | Kann |

### 2.6 Öffentliche Website

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-601 | Das System MUSS eine öffentliche Event-Übersicht bieten | Muss |
| FA-602 | Das System MUSS Filterung nach Datum, Kategorie, Ort bieten | Muss |
| FA-603 | Das System MUSS SEO-optimierte Event-Detailseiten haben | Muss |
| FA-604 | Das System MUSS responsives Design (Mobile-First) haben | Muss |
| FA-605 | Das System SOLL Social Media Sharing ermöglichen | Soll |
| FA-606 | Das System SOLL eine Suchfunktion bieten | Soll |

---

## 3. Nicht-funktionale Anforderungen

### 3.1 Event-Driven Architecture (KRITISCH)

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-701 | Das System MUSS auf Event-Driven Architecture basieren | Muss |
| NFA-702 | Das System MUSS RabbitMQ oder Apache Kafka als Message Broker nutzen | Muss |
| NFA-703 | Das System MUSS mindestens 5 verschiedene Domain Events definieren | Muss |
| NFA-704 | Das System MUSS Event Sourcing für Buchungen implementieren | Muss |
| NFA-705 | Das System SOLL CQRS (Command Query Responsibility Segregation) nutzen | Soll |
| NFA-706 | Das System MUSS idempotente Event-Handler haben | Muss |

### 3.2 Performance und Skalierbarkeit

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-801 | Das System MUSS 500 gleichzeitige Buchungsvorgänge verarbeiten können | Muss |
| NFA-802 | Das System MUSS Ticket-Reservierungen atomar und race-condition-frei handhaben | Muss |
| NFA-803 | Buchungsbestätigung MUSS innerhalb von 5 Sekunden erfolgen | Muss |
| NFA-804 | Das System SOLL horizontal skalierbar sein | Soll |

### 3.3 Zuverlässigkeit

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-901 | Das System MUSS garantierte Nachrichtenverarbeitung (at-least-once) bieten | Muss |
| NFA-902 | Das System MUSS Dead-Letter-Queues für fehlerhafte Nachrichten haben | Muss |
| NFA-903 | Das System MUSS Transaktionen über Services hinweg konsistent halten (Saga Pattern) | Muss |
| NFA-904 | Das System SOLL Circuit Breaker für externe Services implementieren | Soll |

---

## 4. Technische Vorgaben

### 4.1 Tech-Stack

| Komponente | Technologie | Begründung |
|------------|-------------|------------|
| Backend | C# / ASP.NET Core 9 | Firmenstandard |
| Message Broker | RabbitMQ | Einfacher Einstieg in EDA |
| Event Store | EventStoreDB oder PostgreSQL | Event Sourcing |
| Read Database | PostgreSQL | Abfragen |
| Cache | Redis | Session, Reservierungen |
| Frontend | Vue.js 3 / Nuxt 3 | SSR für SEO |
| Scanner App | Vue.js PWA | Offline-fähig |
| E-Mail | SendGrid/Mailgun (Sandbox) | Transaktionale E-Mails |
| Payment | Stripe (Testmodus) | Standard Payment API |
| Container | Docker, Docker Compose | Deployment |

### 4.2 Event-Driven Architektur

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           Clients                                        │
├───────────────┬───────────────┬───────────────┬─────────────────────────┤
│  Public Web   │  Admin Portal │  Scanner App  │    External Systems     │
│  (Nuxt SSR)   │  (Vue SPA)    │  (Vue PWA)    │    (Webhooks)           │
└───────┬───────┴───────┬───────┴───────┬───────┴────────────┬────────────┘
        │               │               │                     │
        ▼               ▼               ▼                     ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                         API Gateway (Traefik)                            │
└─────────────────────────────────┬───────────────────────────────────────┘
                                  │
        ┌─────────────────────────┼─────────────────────────┐
        │                         │                         │
        ▼                         ▼                         ▼
┌───────────────┐       ┌───────────────┐       ┌───────────────┐
│ Booking       │       │ Event         │       │ Notification  │
│ Service       │       │ Service       │       │ Service       │
│ (Commands)    │       │ (Queries)     │       │ (Async)       │
└───────┬───────┘       └───────┬───────┘       └───────┬───────┘
        │                       │                       │
        │    ┌──────────────────┼───────────────────────┘
        │    │                  │
        ▼    ▼                  ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                         RabbitMQ (Message Broker)                        │
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌─────────────┐       │
│  │ booking.    │ │ ticket.     │ │ payment.    │ │ checkin.    │       │
│  │ created     │ │ reserved    │ │ completed   │ │ processed   │       │
│  └─────────────┘ └─────────────┘ └─────────────┘ └─────────────┘       │
└─────────────────────────────────┬───────────────────────────────────────┘
                                  │
        ┌─────────────────────────┼─────────────────────────┐
        │                         │                         │
        ▼                         ▼                         ▼
┌───────────────┐       ┌───────────────┐       ┌───────────────┐
│ EventStoreDB  │       │ PostgreSQL    │       │ Redis         │
│ (Event Store) │       │ (Read Model)  │       │ (Cache/Res.)  │
└───────────────┘       └───────────────┘       └───────────────┘
```

### 4.3 Domain Events (Mindestens zu implementieren)

```csharp
// Pflicht-Events
EventCreated           // Neues Event angelegt
EventPublished         // Event veröffentlicht
TicketReserved         // Ticket für Warenkorb reserviert
TicketReservationExpired // Reservierung abgelaufen
BookingCreated         // Buchung erstellt
PaymentReceived        // Zahlung eingegangen
TicketIssued           // E-Ticket generiert und versendet
CheckInProcessed       // Ticket am Einlass gescannt
EventCancelled         // Event abgesagt
RefundProcessed        // Rückerstattung durchgeführt
```

---

## 5. Pflichtdokumentation nach V-Modell

### 5.1 Erforderliche Dokumente

| Phase | Dokument | Besonderheit |
|-------|----------|--------------|
| Anforderungen | Lastenheft | Event-Katalog definieren |
| Spezifikation | Pflichtenheft | CQRS/ES-Patterns beschreiben |
| Entwurf | High-Level-Design | Event-Flow-Diagramme |
| Entwurf | Low-Level-Design | Event Schemas (JSON) |
| Entwurf | Event Storming Dokumentation | **PFLICHT** |
| Projektmanagement | ADRs | Mind. 5, davon 2 zu EDA |
| Projektmanagement | Projektprotokoll | Mit Event-Storming Workshop |

### 5.2 Pflicht-Testdokumentation

| Dokument | Inhalt | Spezielle Anforderungen |
|----------|--------|-------------------------|
| **Mastertestplan** | Teststrategie inkl. Event-basierter Tests | EDA-Teststrategie beschreiben |
| **Komponententest-Spezifikation** | Unit-Tests für Event Handler | Mind. 50 Testfälle |
| **Integrationstest-Spezifikation** | Tests für Event-Flows | Mind. 20 Testfälle |
| **Contract-Test-Spezifikation** | Event-Schema-Validierung | **PFLICHT** - Mind. 15 Tests |
| **Systemtest-Spezifikation** | E2E-Buchungsszenarien | Mind. 15 Szenarien |
| **Lasttest-Spezifikation** | Concurrent Booking Tests | **PFLICHT** - Mind. 5 Szenarien |
| **Chaos-Test-Spezifikation** | Fehlerszenarien (Broker down, etc.) | Mind. 5 Szenarien |
| **Komponententest-Report** | Ergebnisse Unit-Tests | Coverage >80% |
| **Integrationstest-Report** | Event-Flow-Ergebnisse | Alle Flows dokumentiert |
| **Contract-Test-Report** | Schema-Validierung | Alle Events geprüft |
| **Systemtest-Report** | E2E-Ergebnisse | Mit Screenshots |
| **Lasttest-Report** | Performance-Ergebnisse | Mit Grafiken, Bottlenecks |
| **Chaos-Test-Report** | Resilienz-Ergebnisse | Recovery-Zeiten dokumentiert |
| **Anforderungsverifikation** | Traceability Matrix | 100% Muss-Anforderungen |

### 5.3 Besondere Testanforderungen

**Event-basierte Tests (Pflicht):**

| Test-Kategorie | Beschreibung | Beispiel |
|----------------|--------------|----------|
| Event Publishing | Werden Events korrekt publiziert? | Nach Buchung: BookingCreated |
| Event Handling | Reagieren Handler korrekt? | NotificationService auf TicketIssued |
| Idempotenz | Doppelte Events ohne Nebenwirkung | Gleiche Message zweimal senden |
| Ordering | Reihenfolge bei abhängigen Events | Reserved vor Issued |
| Dead Letter | Fehlerhafte Events in DLQ | Ungültiges Event-Format |
| Recovery | System nach Broker-Ausfall | Broker neu starten |

---

## 6. Spezielle Projektanforderungen

### 6.1 Event Storming Workshop (Pflicht)

Das Team MUSS einen **Event Storming Workshop** durchführen und dokumentieren:

1. **Big Picture Event Storming** (2-3 Stunden)
   - Alle Domain Events identifizieren
   - Aggregates definieren
   - Bounded Contexts abgrenzen

2. **Design Level Event Storming** (2-3 Stunden)
   - Commands und Events verfeinern
   - Read Models identifizieren
   - Policies definieren

**Deliverable:** Event Storming Dokumentation mit Fotos/Screenshots des Boards und textueller Erklärung

### 6.2 Saga Pattern Implementation (Research-Komponente)

Das Team MUSS das **Saga Pattern** für verteilte Transaktionen implementieren und dokumentieren:

1. **Buchungs-Saga:** Reservierung → Zahlung → Ticketausstellung
2. **Kompensation:** Was passiert bei Zahlungsfehler?
3. **Timeout-Handling:** Wie werden abgelaufene Reservierungen behandelt?

**Deliverable:** Saga-Dokumentation mit Zustandsdiagramm und Fehlerszenarien

### 6.3 Prozess-Anforderungen

| Anforderung | Beschreibung |
|-------------|--------------|
| Code-Reviews | Jeder PR benötigt 1 Approval |
| Event-Schema-Reviews | Neue Events benötigen Team-Diskussion |
| Sprint-Reviews | Alle 2 Wochen |
| Pair Programming | Für komplexe Event Handler empfohlen |
| KI-Dokumentation | Event-Handler-Logik muss verstanden sein |

---

## 7. Abnahmekriterien

### 7.1 Muss-Kriterien für Projektabnahme

1. [ ] Alle Muss-Anforderungen erfüllt
2. [ ] Event Storming Dokumentation liegt vor
3. [ ] Mindestens 10 Domain Events implementiert
4. [ ] Saga Pattern für Buchungen funktioniert
5. [ ] Lasttest: 500 gleichzeitige Buchungen erfolgreich
6. [ ] Chaos-Test: System recovered nach Broker-Restart
7. [ ] Alle Testdokumente und Reports vorhanden
8. [ ] Code-Coverage >80%
9. [ ] Docker-Deployment funktioniert

### 7.2 Bewertungsschema

| Kategorie | Gewicht | Kriterien |
|-----------|---------|-----------|
| Funktionalität | 20% | Erfüllung der Anforderungen |
| EDA-Architektur | 25% | Event Design, Saga, Idempotenz |
| Testqualität | 20% | Coverage, Event-Tests, Lasttests |
| Event Storming | 15% | Workshop-Durchführung und Doku |
| Prozessqualität | 10% | Reviews, Teamarbeit |
| KI-Reflexion | 10% | Verständnis der Event-Handler |

---

## 8. Warum dieses Projekt für KI-Zeitalter geeignet ist

| Aspekt | Begründung |
|--------|------------|
| **Event-Driven Architecture** | Konzeptionelle Arbeit, nicht nur Code |
| **Event Storming** | Workshop-basiert, nicht automatisierbar |
| **Saga Pattern** | Komplexe Zustandsmaschine, Fehlerszenarien |
| **Lasttests** | Echte Performance-Analyse nötig |
| **Chaos Engineering** | Manuelle Fehlerinjektion |
| **Verteilte Systeme** | Debugging über Services hinweg |
| **Payment Integration** | Externe API mit Testmodus |

---

## Projekt genehmigt

Offenburg, den 13.01.2026

_____Lisa Hartmann_____

CultureConnect GmbH
Lisa Hartmann
Geschäftsführerin CultureConnect GmbH
