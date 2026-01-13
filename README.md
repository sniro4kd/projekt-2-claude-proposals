# Projektproposals im KI-Zeitalter

## Übersicht

Dieses Repository enthält Materialien zur Anpassung von Software-Projektaufgaben für Studierende im Zeitalter von KI-Assistenten wie Claude Code.

---

## Inhalt

| Datei | Beschreibung |
|-------|--------------|
| [00_Theoretische_Analyse.md](00_Theoretische_Analyse.md) | Analyse und Strategien zur Projektanpassung |
| [01_Proposal_SmartCampus.md](01_Proposal_SmartCampus.md) | IoT-Plattform für Gebäudemanagement |
| [02_Proposal_MediTrack.md](02_Proposal_MediTrack.md) | Medikamenten-Management mit Security-Fokus |
| [03_Proposal_EventHub.md](03_Proposal_EventHub.md) | Event-Management mit Event-Driven Architecture |
| [04_Proposal_CodeReview_AI.md](04_Proposal_CodeReview_AI.md) | KI-gestütztes Code-Review-System |
| [05_Proposal_GreenFleet.md](05_Proposal_GreenFleet.md) | Nachhaltiges Flottenmanagement |

---

## Vergleich der Proposals

### Technische Schwerpunkte

| Proposal | Architektur | Datenbanken | Externe APIs | Besonderheit |
|----------|-------------|-------------|--------------|--------------|
| **SmartCampus** | Microservices | TimescaleDB + PostgreSQL + Redis | MQTT, Kalender | IoT, Sensoren |
| **MediTrack** | Layered + PWA | PostgreSQL (encrypted) | - | Security, DSGVO |
| **EventHub** | Event-Driven (CQRS/ES) | EventStoreDB + PostgreSQL + Redis | Stripe, Mail | Saga Pattern |
| **CodeGuardian** | Worker-basiert | PostgreSQL + Redis | GitHub, LLM APIs | Prompt Engineering |
| **GreenFleet** | Stream Processing | PostgreSQL + PostGIS + InfluxDB | Maps, Weather, Traffic | Optimierungsalgorithmen |

### Research-Komponenten

| Proposal | Research-Thema | Deliverable |
|----------|----------------|-------------|
| **SmartCampus** | Belegungsvorhersage (ML-Vergleich) | Research-Report (10+ Seiten) |
| **MediTrack** | Wechselwirkungsdatenbank aufbauen | DSFA + Wechselwirkungs-Doku |
| **EventHub** | Event Storming + Saga Pattern | Workshop-Dokumentation |
| **CodeGuardian** | Prompt Engineering + LLM-Evaluation | Prompt-Doku + Kosten-Analyse |
| **GreenFleet** | VRP-Algorithmen-Vergleich | Benchmark-Report (8+ Seiten) |

### Test-Schwerpunkte

| Proposal | Spezielle Tests | Testdokumente |
|----------|-----------------|---------------|
| **SmartCampus** | Lasttests (100 Sensoren), Simulation | Standard + Lasttest-Report |
| **MediTrack** | Security-Tests (OWASP), Pentest | Security-Test-Report (Pflicht) |
| **EventHub** | Contract-Tests, Chaos-Tests | Event-Tests, Saga-Tests |
| **CodeGuardian** | Golden Tests, LLM-Evaluation | LLM-Evaluation-Report |
| **GreenFleet** | Algorithmus-Tests, Simulations-Tests | CO2-Validierungs-Report |

---

## Aufwandsverteilung (geschätzt)

Für ein Team von 6-7 Studierenden mit 30-40h pro Person (180-280 Personenstunden total):

| Aktivität | Traditionell (ohne KI) | Mit KI-Assistenten |
|-----------|------------------------|-------------------|
| **Implementierung** | 60% | 15% |
| **Testing & Dokumentation** | 20% | 25% |
| **Research/Analyse** | 5% | 20% |
| **Architektur & Design** | 10% | 20% |
| **Prozess (Reviews, Retros)** | 5% | 20% |

---

## Gemeinsame Anforderungen aller Proposals

### V-Modell Dokumentation (Pflicht)

Alle Projekte erfordern:

1. **Lastenheft** - Kundenanforderungen dokumentiert
2. **Pflichtenheft** - Technische Spezifikation
3. **High-Level-Design** - Architekturübersicht
4. **Low-Level-Design** - Detailliertes Design
5. **ADRs** - Mindestens 5 Architecture Decision Records
6. **Projektprotokoll** - Sprint-Protokolle, Retrospektiven

### Test-Dokumentation (Pflicht)

| Stufe | Spezifikation | Report |
|-------|---------------|--------|
| **Unit-Tests** | Komponententest-Spezifikation (50+ Testfälle) | Komponententest-Report |
| **Integration** | Integrationstest-Spezifikation (20+ Testfälle) | Integrationstest-Report |
| **System/E2E** | Systemtest-Spezifikation (10-15 Szenarien) | Systemtest-Report |
| **Spezial** | Projekt-spezifische Tests | Projekt-spezifische Reports |
| **Coverage** | - | Code-Coverage-Report (Ziel >80%) |
| **Traceability** | - | Anforderungsverifikation (100%) |

### Mastertestplan

Jedes Projekt erfordert einen **Mastertestplan** der folgendes enthält:

- Teststrategie und -ansatz
- Testumgebungen (lokal, CI/CD, Staging)
- Testdaten-Management
- Verantwortlichkeiten im Team
- Zeitplan für Testaktivitäten
- Entry/Exit-Kriterien pro Teststufe
- Risiken und Mitigationsstrategien

---

## Bewertungsschema (Empfehlung)

| Kategorie | Gewicht | Beschreibung |
|-----------|---------|--------------|
| **Funktionalität** | 20% | Erfüllung der Muss-/Soll-Anforderungen |
| **Architektur** | 20% | ADRs, Clean Architecture, Entscheidungsqualität |
| **Testqualität** | 20% | Coverage, Dokumentation, Teststrategie |
| **Research** | 15% | Projekt-spezifische Forschungskomponente |
| **Prozess** | 15% | Reviews, Retrospektiven, Teamarbeit |
| **KI-Reflexion** | 10% | Dokumentation und Reflexion des KI-Einsatzes |

---

## Regeln für KI-Nutzung

### Erlaubt und erwünscht

- Boilerplate-Code generieren lassen
- Tests schreiben lassen
- Dokumentationsvorlagen erstellen
- Debugging-Unterstützung
- Code-Erklärungen einholen

### Eingeschränkt (mit Dokumentationspflicht)

- Architektur-Code (muss verstanden und reviewed werden)
- Algorithmus-Implementierungen (muss erklärt werden können)
- Security-relevanter Code (muss geprüft werden)

### Nicht erlaubt / wenig sinnvoll

- Retrospektiven schreiben lassen
- Stakeholder-Kommunikation delegieren
- Code-Reviews automatisieren
- Research ohne eigene Analyse

### Dokumentationspflicht

- Wesentliche KI-Interaktionen werden im Projektprotokoll festgehalten
- KI-generierter Code wird als solcher markiert
- Studierende müssen KI-Code in mündlicher Prüfung erklären können

---

## Referenz: Original-Projekt

Das Original-Projekt **CatchTheRabbit** diente als Baseline:

| Metrik | Original (ohne KI) | Mit Claude Code |
|--------|-------------------|-----------------|
| Personenstunden | 180-280h (6-7 Personen) | ~5h (1 Person) |
| LOC | ~5.100 | ~5.100 |
| Testabdeckung | variabel | 83.8% |
| V-Modell Doku | komplett | komplett |

**Produktivitätsfaktor: 36-56x**

Die neuen Proposals sind so gestaltet, dass sie mit KI-Unterstützung einen ähnlichen Aufwand wie das Original-Projekt ohne KI erfordern.

---

## Empfehlungen für Lehrende

1. **Kick-off Workshop:** Erwartungen an KI-Nutzung klären
2. **Zwischenpräsentationen:** Architektur-Reviews einbauen
3. **Code-Walkthrough:** Studierende erklären ihren Code
4. **Retrospektiven:** Team-Reflexion über KI-Einsatz
5. **Mündliche Prüfung:** Verständnis des Codes prüfen

---

## Kontakt

Bei Fragen zu den Proposals oder der Methodik wenden Sie sich an die Modulverantwortlichen.

*Erstellt: Januar 2026*
