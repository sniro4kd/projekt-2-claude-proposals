# Project Proposal: GreenFleet - Nachhaltiges Flottenmanagement

---

| Eigenschaft | Wert |
|-------------|------|
| **Firma** | EcoLogistics AG |
| **Projekt** | GreenFleet |
| **Product Owner** | Sarah Klein |
| **Projektlaufzeit** | März - Juli 2026 |
| **Budget** | 38.000 Euro |
| **Version** | 1.0 |
| **Datum** | 13.01.2026 |
| **Zielgruppe** | 6-7 Studierende, 4.-6. Semester Angewandte Informatik |
| **Aufwand pro Person** | 30-40 Stunden (mit KI-Assistenten) |

---

## 1. Projektbeschreibung

### 1.1 Hintergrund

Die EcoLogistics AG betreibt einen Lieferdienst mit 50 Fahrzeugen (Mix aus Verbrenner, Hybrid, Elektro). Das Unternehmen möchte seinen CO2-Fußabdruck reduzieren und gleichzeitig die Flottenkosten optimieren.

Es soll ein **Flottenmanagement-System** entwickelt werden, das:
- Echtzeitdaten von Fahrzeugen erfasst (GPS, Verbrauch, Ladezustand)
- Routen CO2-optimiert plant
- Wartungsintervalle vorhersagt
- Nachhaltigkeits-Reports für Stakeholder generiert

### 1.2 Besondere Herausforderung: Echte Daten und Optimierung

Dieses Projekt kombiniert:
- **IoT-Datenverarbeitung** (GPS-Tracker, OBD-II Simulatoren)
- **Optimierungsalgorithmen** (Routenplanung, Fahrzeugzuweisung)
- **Datenanalyse und ML** (Verbrauchsprognose, Wartungsvorhersage)
- **Externe APIs** (Kartendienste, Wetter, Verkehr)

---

## 2. Funktionale Anforderungen

### 2.1 Fahrzeugverwaltung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-101 | Das System MUSS Fahrzeuge mit Typ (Verbrenner/Hybrid/Elektro), Kennzeichen, Kapazität verwalten | Muss |
| FA-102 | Das System MUSS technische Daten (Verbrauch, Reichweite, CO2/km) pro Fahrzeugtyp speichern | Muss |
| FA-103 | Das System MUSS Fahrzeugstatus (verfügbar, unterwegs, Wartung) tracken | Muss |
| FA-104 | Das System MUSS Wartungshistorie führen | Muss |
| FA-105 | Das System SOLL Fahrer-Fahrzeug-Zuordnung verwalten | Soll |
| FA-106 | Das System SOLL Versicherungs- und TÜV-Termine tracken | Soll |

### 2.2 Echtzeit-Tracking

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-201 | Das System MUSS GPS-Positionen aller Fahrzeuge in Echtzeit anzeigen | Muss |
| FA-202 | Das System MUSS Position via GPS-Tracker oder Simulator empfangen | Muss |
| FA-203 | Das System MUSS aktuelle Route pro Fahrzeug visualisieren | Muss |
| FA-204 | Das System MUSS Geschwindigkeit und Fahrtrichtung anzeigen | Muss |
| FA-205 | Das System SOLL Geofencing mit Alerts unterstützen | Soll |
| FA-206 | Das System SOLL historische Fahrten speichern und abspielen | Soll |
| FA-207 | Das System KANN OBD-II Daten (Verbrauch, Motortemperatur) empfangen | Kann |

### 2.3 Routenplanung und Optimierung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-301 | Das System MUSS Touren mit mehreren Stopps planen können | Muss |
| FA-302 | Das System MUSS Routen nach verschiedenen Kriterien optimieren (Zeit, Distanz, CO2) | Muss |
| FA-303 | Das System MUSS bei E-Fahrzeugen Ladestopps einplanen wenn nötig | Muss |
| FA-304 | Das System MUSS Lieferzeitfenster berücksichtigen | Muss |
| FA-305 | Das System MUSS Fahrzeugkapazität bei Zuweisung berücksichtigen | Muss |
| FA-306 | Das System SOLL Verkehrslage in Planung einbeziehen | Soll |
| FA-307 | Das System SOLL Wetterdaten für E-Fahrzeug-Reichweite berücksichtigen | Soll |
| FA-308 | Das System KANN Echtzeit-Umplanung bei Verzögerungen bieten | Kann |

### 2.4 CO2-Tracking und Reporting

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-401 | Das System MUSS CO2-Emissionen pro Fahrt berechnen | Muss |
| FA-402 | Das System MUSS CO2-Emissionen pro Fahrzeug, Tag, Monat aggregieren | Muss |
| FA-403 | Das System MUSS Vergleich tatsächlich vs. optimale Route zeigen | Muss |
| FA-404 | Das System MUSS Nachhaltigkeits-Dashboard bieten | Muss |
| FA-405 | Das System MUSS PDF-Reports für Stakeholder generieren | Muss |
| FA-406 | Das System SOLL CO2-Einsparung durch Optimierung quantifizieren | Soll |
| FA-407 | Das System SOLL Benchmarks gegen Branchendurchschnitt zeigen | Soll |

### 2.5 Wartungsvorhersage (Predictive Maintenance)

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-501 | Das System MUSS Wartungsintervalle basierend auf km-Stand tracken | Muss |
| FA-502 | Das System MUSS anstehende Wartungen anzeigen und erinnern | Muss |
| FA-503 | Das System SOLL basierend auf Fahrverhalten optimale Wartungszeitpunkte vorhersagen | Soll |
| FA-504 | Das System SOLL ungewöhnliche Verbräuche als Warnung melden | Soll |
| FA-505 | Das System KANN Anomalien in OBD-II Daten erkennen | Kann |

### 2.6 Auftragsmanagement

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-601 | Das System MUSS Lieferaufträge mit Abholung, Ziel, Zeitfenster verwalten | Muss |
| FA-602 | Das System MUSS Aufträge automatisch Touren zuordnen können | Muss |
| FA-603 | Das System MUSS Auftragsstatus (offen, unterwegs, geliefert) tracken | Muss |
| FA-604 | Das System SOLL Kunden-Benachrichtigungen bei Annäherung senden | Soll |
| FA-605 | Das System SOLL Lieferbestätigungen mit Foto/Unterschrift erfassen | Soll |

---

## 3. Nicht-funktionale Anforderungen

### 3.1 Optimierungsanforderungen (KRITISCH)

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-701 | Das System MUSS Vehicle Routing Problem (VRP) Algorithmus implementieren | Muss |
| NFA-702 | Optimierung für 20 Stopps MUSS unter 5 Sekunden dauern | Muss |
| NFA-703 | Das System MUSS mindestens 2 Optimierungsalgorithmen vergleichen | Muss |
| NFA-704 | Das System SOLL Optimierungsergebnisse cachen | Soll |

### 3.2 Datenverarbeitung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-801 | Das System MUSS GPS-Daten von 50 Fahrzeugen alle 10 Sekunden verarbeiten | Muss |
| NFA-802 | Das System MUSS GPS-Historie für 90 Tage speichern | Muss |
| NFA-803 | Das System MUSS Datenimport (CSV, API) für Aufträge unterstützen | Muss |

### 3.3 Externe Integrationen

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-901 | Das System MUSS Kartenvisualisierung (OpenStreetMap oder ähnlich) nutzen | Muss |
| NFA-902 | Das System MUSS Routing-API (OSRM, GraphHopper oder Google) nutzen | Muss |
| NFA-903 | Das System SOLL Wetter-API integrieren | Soll |
| NFA-904 | Das System SOLL Verkehrsdaten-API integrieren | Soll |
| NFA-905 | Das System KANN Ladesäulen-API (z.B. OpenChargeMap) nutzen | Kann |

---

## 4. Technische Vorgaben

### 4.1 Tech-Stack

| Komponente | Technologie | Begründung |
|------------|-------------|------------|
| Backend | C# / ASP.NET Core 9 | Firmenstandard |
| Datenbank | PostgreSQL + PostGIS | Geodaten-Support |
| Zeitreihen | InfluxDB oder TimescaleDB | GPS-Historie |
| Message Queue | RabbitMQ | GPS-Datenverarbeitung |
| Frontend | Vue.js 3 | Dashboard |
| Karten | Leaflet + OpenStreetMap | Open Source |
| Routing | OSRM (self-hosted) oder GraphHopper | Routing-Engine |
| Optimierung | OR-Tools (Google) oder OptaPlanner | VRP-Solver |
| Mobile | Vue.js PWA | Fahrer-App |
| Container | Docker, Docker Compose | Deployment |

### 4.2 Architektur

```
┌─────────────────────────────────────────────────────────────────────────┐
│                            Datenquellen                                  │
├─────────────────┬─────────────────┬─────────────────┬───────────────────┤
│  GPS Tracker    │  OBD-II         │  Wetter-API     │  Traffic-API      │
│  (oder Sim.)    │  (Simulator)    │                 │                   │
└────────┬────────┴────────┬────────┴────────┬────────┴─────────┬─────────┘
         │                 │                  │                  │
         │              MQTT/HTTP             │               HTTP
         │                 │                  │                  │
         ▼                 ▼                  ▼                  ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                         Data Ingestion Layer                             │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐         │
│  │ GPS Receiver    │  │ OBD Receiver    │  │ External API    │         │
│  │ Service         │  │ Service         │  │ Connector       │         │
│  └────────┬────────┘  └────────┬────────┘  └────────┬────────┘         │
│           │                    │                    │                   │
│           ▼                    ▼                    ▼                   │
│  ┌─────────────────────────────────────────────────────────────────┐   │
│  │                    RabbitMQ (Message Queue)                     │   │
│  └─────────────────────────────────────────────────────────────────┘   │
└─────────────────────────────────┬───────────────────────────────────────┘
                                  │
                                  ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                         Core Services                                    │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐         │
│  │ Vehicle         │  │ Route           │  │ Analytics       │         │
│  │ Service         │  │ Optimizer       │  │ Service         │         │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘         │
│           │                    │                    │                   │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐         │
│  │ Order           │  │ Tracking        │  │ Reporting       │         │
│  │ Service         │  │ Service         │  │ Service         │         │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘         │
└─────────────────────────────────┬───────────────────────────────────────┘
                                  │
         ┌────────────────────────┼────────────────────────┐
         │                        │                        │
         ▼                        ▼                        ▼
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   PostgreSQL    │     │   InfluxDB      │     │   Redis         │
│   + PostGIS     │     │   (GPS-History) │     │   (Cache)       │
└─────────────────┘     └─────────────────┘     └─────────────────┘
         │                        │                        │
         └────────────────────────┼────────────────────────┘
                                  │
                                  ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                         Presentation Layer                               │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐         │
│  │ Fleet Dashboard │  │ Route Planner   │  │ Driver App      │         │
│  │ (Leaflet Map)   │  │ UI              │  │ (PWA)           │         │
│  └─────────────────┘  └─────────────────┘  └─────────────────┘         │
└─────────────────────────────────────────────────────────────────────────┘
```

---

## 5. Pflichtdokumentation nach V-Modell

### 5.1 Erforderliche Dokumente

| Phase | Dokument | Besonderheit |
|-------|----------|--------------|
| Anforderungen | Lastenheft | CO2-Berechnungsmodell definieren |
| Spezifikation | Pflichtenheft | Optimierungskriterien spezifizieren |
| Entwurf | High-Level-Design | Datenfluss-Diagramme |
| Entwurf | Low-Level-Design | VRP-Algorithmus-Design |
| Entwurf | Geodaten-Architektur | PostGIS-Schema |
| Projektmanagement | ADRs | Mind. 5, davon 2 zu Algorithmen |
| Projektmanagement | Algorithmen-Vergleich | **PFLICHT** |

### 5.2 Pflicht-Testdokumentation

| Dokument | Inhalt | Spezielle Anforderungen |
|----------|--------|-------------------------|
| **Mastertestplan** | Teststrategie inkl. Simulation | Simulator-Strategie beschreiben |
| **Komponententest-Spezifikation** | Unit-Tests für Services | Mind. 50 Testfälle |
| **Integrationstest-Spezifikation** | API-Tests, DB-Tests | Mind. 20 Testfälle |
| **Algorithmus-Test-Spezifikation** | VRP-Solver Tests | **PFLICHT** - Mind. 15 Szenarien |
| **Simulations-Test-Spezifikation** | GPS-Simulator Tests | **PFLICHT** - Mind. 10 Szenarien |
| **Systemtest-Spezifikation** | E2E Tourenplanung | Mind. 10 Szenarien |
| **Performance-Test-Spezifikation** | Optimierung unter Last | Mind. 5 Szenarien |
| **Komponententest-Report** | Ergebnisse Unit-Tests | Coverage >80% |
| **Integrationstest-Report** | API-Ergebnisse | Alle Integrationen |
| **Algorithmus-Test-Report** | VRP-Solver Qualität | **PFLICHT** - Vergleichsmatrix |
| **Simulations-Test-Report** | Simulator-Validierung | Mit visualisierten Fahrten |
| **Systemtest-Report** | E2E-Ergebnisse | Screenshots |
| **Performance-Test-Report** | Optimierungs-Zeiten | Mit Grafiken |
| **CO2-Validierungs-Report** | Plausibilität der CO2-Berechnung | **PFLICHT** |
| **Anforderungsverifikation** | Traceability Matrix | 100% Muss-Anforderungen |

### 5.3 Besondere Testanforderungen

**Algorithmus-Tests (Pflicht):**

| Szenario | Beschreibung | Erwartung |
|----------|--------------|-----------|
| Small Instance | 5 Stopps, 1 Fahrzeug | Optimale Lösung |
| Medium Instance | 15 Stopps, 3 Fahrzeuge | Gute Lösung (<10% von optimal) |
| Large Instance | 30 Stopps, 5 Fahrzeuge | Lösung in <5s |
| E-Vehicle | Mit Ladestopp-Constraint | Korrekte Einplanung |
| Time Windows | Zeitfenster-Constraints | Alle Fenster eingehalten |

**Simulations-Tests (Pflicht):**

| Test | Beschreibung |
|------|--------------|
| Route Replay | Bekannte Route wird korrekt simuliert |
| Speed Variation | Geschwindigkeiten realistisch |
| Position Accuracy | GPS-Drift simuliert |
| Concurrent Vehicles | 50 Fahrzeuge parallel |
| Historical Playback | Vergangene Fahrten abspielen |

---

## 6. Spezielle Projektanforderungen

### 6.1 Algorithmen-Vergleich (Research-Komponente)

Das Team MUSS mindestens **2 VRP-Algorithmen** implementieren und vergleichen:

**Option A: Klassische Algorithmen**
- Nearest Neighbor Heuristik (Baseline)
- 2-opt oder 3-opt Verbesserung
- Savings Algorithm (Clarke-Wright)

**Option B: Metaheuristiken**
- Simulated Annealing
- Genetic Algorithm
- Tabu Search

**Option C: OR-Tools / OptaPlanner**
- Verschiedene Solver-Konfigurationen

**Deliverables:**
- Algorithmen-Vergleichs-Report (mind. 8 Seiten)
- Benchmark-Datensätze (klein, mittel, groß)
- Laufzeit- und Qualitätsvergleich
- Empfehlung für Produktiveinsatz

### 6.2 GPS-Simulator (Pflicht)

Das Team MUSS einen **GPS-Simulator** entwickeln:

1. **Route-basiert:** Simuliert Fahrt entlang definierter Route
2. **Realistisch:** Variable Geschwindigkeit, Stopps
3. **Skalierbar:** Mind. 50 parallele Fahrzeuge
4. **Steuerbar:** Start, Stop, Pause, Geschwindigkeit

**Deliverable:** Funktionierender Simulator + Dokumentation

### 6.3 CO2-Berechnungsmodell (Pflicht)

Das Team MUSS ein **plausibles CO2-Berechnungsmodell** entwickeln und validieren:

1. **Basiswerte:** CO2/km für verschiedene Fahrzeugtypen
2. **Faktoren:** Einfluss von Geschwindigkeit, Last, Steigung
3. **E-Fahrzeuge:** Strommix für CO2-Äquivalent
4. **Validierung:** Vergleich mit offiziellen Daten

**Deliverable:** CO2-Modell-Dokumentation + Validierungs-Report

### 6.4 Prozess-Anforderungen

| Anforderung | Beschreibung |
|-------------|--------------|
| Code-Reviews | Jeder PR benötigt 1 Approval |
| Algorithmus-Reviews | Optimierer-Code benötigt Team-Review |
| Sprint-Reviews | Alle 2 Wochen mit Demo auf Karte |
| Pair Programming | Für Algorithmus-Implementierung empfohlen |

---

## 7. Abnahmekriterien

### 7.1 Muss-Kriterien für Projektabnahme

1. [ ] Alle Muss-Anforderungen erfüllt
2. [ ] GPS-Tracking auf Karte funktioniert
3. [ ] Routenoptimierung funktioniert (20 Stopps < 5s)
4. [ ] CO2-Berechnung plausibel validiert
5. [ ] Algorithmen-Vergleich durchgeführt
6. [ ] GPS-Simulator funktioniert (50 Fahrzeuge)
7. [ ] Alle Testdokumente und Reports vorhanden
8. [ ] Code-Coverage >80%
9. [ ] Docker-Deployment funktioniert

### 7.2 Bewertungsschema

| Kategorie | Gewicht | Kriterien |
|-----------|---------|-----------|
| Funktionalität | 20% | Erfüllung der Anforderungen |
| Optimierung | 25% | Algorithmenqualität, Vergleich |
| Datenverarbeitung | 15% | GPS, CO2-Modell, Simulator |
| Testqualität | 20% | Coverage, Algorithmus-Tests, Simulation |
| Research & Doku | 10% | Algorithmen-Report, CO2-Validierung |
| Prozessqualität | 10% | Reviews, Teamarbeit |

---

## 8. Warum dieses Projekt für KI-Zeitalter geeignet ist

| Aspekt | Begründung |
|--------|------------|
| **Optimierungsalgorithmen** | Echte Algorithmus-Arbeit, Vergleich |
| **GPS-Simulation** | Eigene Testdaten generieren |
| **Geodaten** | PostGIS, Karten-APIs |
| **Externe APIs** | Routing, Wetter, Verkehr |
| **CO2-Modell** | Domänenwissen, Validierung |
| **Echtzeitverarbeitung** | Message Queue, Streaming |
| **Nachhaltigkeits-Thema** | Gesellschaftliche Relevanz |

---

## Projekt genehmigt

Offenburg, den 13.01.2026

_____Thomas Grün_____

EcoLogistics AG
Thomas Grün
CSO EcoLogistics AG
