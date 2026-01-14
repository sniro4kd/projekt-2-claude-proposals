# Project Proposal: PowerGrid Analyzer - Netzqualitäts-Monitoring-System

---

| Eigenschaft | Wert |
|-------------|------|
| **Firma** | GridWatch Energy Solutions GmbH |
| **Projekt** | PowerGrid Analyzer |
| **Product Owner** | Dipl.-Ing. Frank Neumann |
| **Projektlaufzeit** | März - Juli 2026 |
| **Budget** | 35.000 Euro |
| **Version** | 1.0 |
| **Datum** | 14.01.2026 |
| **Zielgruppe** | 6-7 Studierende, 4.-6. Semester Angewandte Informatik / Elektrotechnik |
| **Aufwand pro Person** | 30-40 Stunden (mit KI-Assistenten) |

---

## 1. Projektbeschreibung

### 1.1 Hintergrund

Die GridWatch Energy Solutions GmbH entwickelt **Monitoring-Systeme für Stromnetze**. Mit der zunehmenden Integration von erneuerbaren Energien und Elektrofahrzeugen wird die **Netzqualität (Power Quality)** zu einem kritischen Faktor.

Probleme wie Oberschwingungen, Spannungseinbrüche, Flicker und Unsymmetrien können empfindliche Geräte beschädigen und müssen erkannt und dokumentiert werden.

Es soll ein **Netzqualitäts-Analyse-System** entwickelt werden, das:
- Spannungs- und Stromsignale analysiert (simuliert oder real)
- Netzqualitätsparameter nach EN 50160 berechnet
- Oberschwingungsanalyse (THD, Einzelharmonische) durchführt
- Events (Einbrüche, Überspannungen) erkennt und protokolliert

### 1.2 Besondere Herausforderung: Normen und DSP

Dieses Projekt verbindet **Elektrotechnik-Normen** mit **Signalverarbeitung**:
- Implementierung normkonformer Messalgorithmen (IEC 61000-4-30)
- Echtzeit-Analyse von Dreiphasensystemen
- Ereigniserkennung mit präzisen Zeitstempeln
- Berichterstattung nach Industriestandards

### 1.3 Projektziele

1. Entwicklung einer Plattform für Netzqualitätsanalyse
2. Implementierung von Oberschwingungsanalyse (FFT-basiert)
3. Berechnung von Power-Quality-Parametern (THD, Flicker, Unsymmetrie)
4. Event-Erkennung (Sags, Swells, Interruptions)
5. Dashboard und Report-Generator nach EN 50160

---

## 2. Funktionale Anforderungen

### 2.1 Signalerfassung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-101 | Das System MUSS dreiphasige Spannungssignale (L1, L2, L3) verarbeiten | Muss |
| FA-102 | Das System MUSS Stromsignale (I1, I2, I3) verarbeiten | Muss |
| FA-103 | Das System MUSS einen Netz-Simulator für Testsignale bereitstellen | Muss |
| FA-104 | Das System MUSS CSV/COMTRADE-Import für Messdaten unterstützen | Muss |
| FA-105 | Das System MUSS mit 10kHz Abtastrate arbeiten können | Muss |
| FA-106 | Das System SOLL Echtzeit-Streaming via WebSocket unterstützen | Soll |
| FA-107 | Das System KANN MQTT für externe Messgeräte unterstützen | Kann |

### 2.2 Oberschwingungsanalyse

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-201 | Das System MUSS FFT-basierte Oberschwingungsanalyse durchführen | Muss |
| FA-202 | Das System MUSS THD (Total Harmonic Distortion) berechnen | Muss |
| FA-203 | Das System MUSS Einzelharmonische bis zur 50. Ordnung anzeigen | Muss |
| FA-204 | Das System MUSS Interharmonische erkennen können | Muss |
| FA-205 | Das System MUSS synchronisierte FFT (PLL-basiert) implementieren | Muss |
| FA-206 | Das System SOLL THD nach IEC 61000-4-7 berechnen | Soll |
| FA-207 | Das System SOLL Trend-Analyse für THD über Zeit bieten | Soll |
| FA-208 | Das System KANN Supraharmonische (2-150 kHz) analysieren | Kann |

### 2.3 Netzqualitätsparameter

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-301 | Das System MUSS RMS-Spannung (True RMS) berechnen | Muss |
| FA-302 | Das System MUSS Frequenzabweichung messen | Muss |
| FA-303 | Das System MUSS Spannungsunsymmetrie berechnen | Muss |
| FA-304 | Das System MUSS Leistungsberechnung durchführen (P, Q, S, PF) | Muss |
| FA-305 | Das System MUSS Grenzwerte nach EN 50160 prüfen | Muss |
| FA-306 | Das System SOLL Flicker (Pst, Plt) nach IEC 61000-4-15 berechnen | Soll |
| FA-307 | Das System SOLL Spannungs-Events klassifizieren (ITIC/CBEMA-Kurve) | Soll |
| FA-308 | Das System KANN Netzimpedanz-Schätzung durchführen | Kann |

### 2.4 Event-Erkennung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-401 | Das System MUSS Spannungseinbrüche (Sags) erkennen | Muss |
| FA-402 | Das System MUSS Überspannungen (Swells) erkennen | Muss |
| FA-403 | Das System MUSS Unterbrechungen (Interruptions) erkennen | Muss |
| FA-404 | Das System MUSS Events mit Zeitstempel und Dauer protokollieren | Muss |
| FA-405 | Das System MUSS Events nach Schwere klassifizieren | Muss |
| FA-406 | Das System SOLL Transienten erkennen | Soll |
| FA-407 | Das System SOLL Event-Wellenformen speichern (Pre/Post-Trigger) | Soll |
| FA-408 | Das System KANN Rapid Voltage Changes (RVC) erkennen | Kann |

### 2.5 Dashboard und Visualisierung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-501 | Das Dashboard MUSS Echtzeit-Spannungs-/Stromverläufe anzeigen | Muss |
| FA-502 | Das Dashboard MUSS Oberschwingungsspektrum als Balkendiagramm zeigen | Muss |
| FA-503 | Das Dashboard MUSS Phasordiagramm (Zeigerdiagramm) anzeigen | Muss |
| FA-504 | Das Dashboard MUSS aktuelle PQ-Parameter übersichtlich darstellen | Muss |
| FA-505 | Das Dashboard MUSS Event-Liste mit Filterung anzeigen | Muss |
| FA-506 | Das Dashboard SOLL ITIC/CBEMA-Kurve mit Events visualisieren | Soll |
| FA-507 | Das Dashboard SOLL historische Trends darstellen | Soll |
| FA-508 | Das Dashboard SOLL Alarmierung bei Grenzwertüberschreitung | Soll |

### 2.6 Berichterstattung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-601 | Das System MUSS EN 50160-konforme Reports generieren | Muss |
| FA-602 | Das System MUSS wöchentliche/monatliche Zusammenfassungen erstellen | Muss |
| FA-603 | Das System MUSS Reports als PDF exportieren | Muss |
| FA-604 | Das System SOLL Compliance-Statistik (% innerhalb Grenzwerte) zeigen | Soll |
| FA-605 | Das System SOLL Event-Reports mit Wellenformen generieren | Soll |
| FA-606 | Das System KANN Reports per E-Mail versenden | Kann |

---

## 3. Nicht-funktionale Anforderungen

### 3.1 Performance

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-701 | FFT-Analyse MUSS synchron zur Netzfrequenz erfolgen | Muss |
| NFA-702 | Event-Erkennung MUSS mit Latenz <100ms erfolgen | Muss |
| NFA-703 | Dashboard MUSS Echtzeit-Updates mit 1 Hz unterstützen | Muss |
| NFA-704 | Das System MUSS 3-Phasen-Analyse simultan durchführen | Muss |

### 3.2 Genauigkeit

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-801 | RMS-Berechnung MUSS Genauigkeit von ±0.1% erreichen | Muss |
| NFA-802 | THD-Berechnung MUSS nach IEC-Standard korrekt sein | Muss |
| NFA-803 | Frequenzmessung MUSS Genauigkeit von ±10mHz erreichen | Muss |
| NFA-804 | Event-Zeitstempel MÜSSEN Genauigkeit von ±1ms haben | Muss |

### 3.3 Skalierbarkeit

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-901 | Das System MUSS mindestens 10 Messpunkte verwalten | Muss |
| NFA-902 | Das System MUSS 1 Jahr historische Daten speichern | Muss |
| NFA-903 | Das System SOLL mehrere Benutzer gleichzeitig unterstützen | Soll |

---

## 4. Technische Vorgaben

### 4.1 Tech-Stack

| Komponente | Technologie | Begründung |
|------------|-------------|------------|
| Backend | C# / ASP.NET Core 9 | Firmenstandard |
| DSP-Bibliothek | MathNet.Numerics | FFT, Filterung |
| Zeitreihendatenbank | InfluxDB oder TimescaleDB | PQ-Messdaten |
| Relationale Daten | PostgreSQL | Konfiguration, Events |
| Job Queue | Hangfire | Report-Generierung |
| Frontend | Vue.js 3 | Dashboard |
| Visualisierung | Chart.js + D3.js | Diagramme |
| PDF-Generierung | QuestPDF oder iText | Reports |
| Container | Docker, Docker Compose | Deployment |

### 4.2 Architektur

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         Signal Sources                                   │
├─────────────────┬─────────────────┬─────────────────────────────────────┤
│  Grid Simulator │  COMTRADE Import│  External Meters (MQTT)             │
│  (Testsignale)  │  (Offline)      │  (Optional)                         │
└────────┬────────┴────────┬────────┴─────────────────┬───────────────────┘
         │                 │                           │
         ▼                 ▼                           ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                          Ingest Service                                  │
│  (Synchronisation, Resampling, Pufferung)                               │
└─────────────────────────────────┬───────────────────────────────────────┘
                                  │
                                  ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                       Analysis Pipeline                                  │
├─────────────────┬─────────────────┬─────────────────┬───────────────────┤
│  FFT Engine     │  RMS/Power      │  Event          │  PQ Parameter     │
│  (Harmonics)    │  Calculator     │  Detector       │  Calculator       │
└────────┬────────┴────────┬────────┴────────┬────────┴─────────┬─────────┘
         │                 │                 │                   │
         └─────────────────┴────────┬────────┴───────────────────┘
                                    │
          ┌─────────────────────────┼─────────────────────────┐
          ▼                         ▼                         ▼
┌─────────────────┐      ┌─────────────────┐      ┌─────────────────┐
│   InfluxDB      │      │   PostgreSQL    │      │   Redis         │
│   (Timeseries)  │      │   (Events,      │      │   (Realtime)    │
│                 │      │    Config)      │      │                 │
└─────────────────┘      └─────────────────┘      └─────────────────┘
                                    │
                                    ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                          API Layer (REST + SignalR)                      │
└─────────────────────────────────┬───────────────────────────────────────┘
                                  │
          ┌───────────────────────┼───────────────────────┐
          ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Dashboard      │    │  Report         │    │  Alert          │
│  (Vue.js)       │    │  Generator      │    │  Service        │
└─────────────────┘    └─────────────────┘    └─────────────────┘
```

---

## 5. Pflichtdokumentation nach V-Modell

### 5.1 Erforderliche Dokumente

| Phase | Dokument | Besonderheit |
|-------|----------|--------------|
| Anforderungen | Lastenheft | EN 50160 Anforderungen dokumentieren |
| Spezifikation | Pflichtenheft | PQ-Algorithmen spezifizieren |
| Entwurf | High-Level-Design | Pipeline-Architektur |
| Entwurf | Low-Level-Design | Algorithmen-Design |
| Entwurf | **Normen-Dokumentation** | **PFLICHT** - EN 50160, IEC 61000-4-30 |
| Entwurf | **Algorithmen-Dokumentation** | **PFLICHT** - FFT-Sync, RMS, THD |
| Projektmanagement | ADRs | Mind. 5, davon 2 zu Norm-Konformität |

### 5.2 Pflicht-Testdokumentation

| Dokument | Inhalt | Spezielle Anforderungen |
|----------|--------|-------------------------|
| **Mastertestplan** | Teststrategie inkl. Norm-Validierung | PQ-Teststrategie |
| **Komponententest-Spezifikation** | Unit-Tests für alle Module | Mind. 70 Testfälle |
| **Referenz-Signal-Tests** | Definierte PQ-Testszenarien | **PFLICHT** - Mind. 25 Szenarien |
| **Norm-Konformitäts-Tests** | EN 50160 Grenzwertprüfung | **PFLICHT** |
| **Event-Erkennungs-Tests** | Sag/Swell/Interruption Detection | **PFLICHT** - Mind. 15 Szenarien |
| **Integrationstest-Spezifikation** | Pipeline-Integration | Mind. 15 Testfälle |
| **Systemtest-Spezifikation** | End-to-End Szenarien | Mind. 10 Szenarien |
| **Komponententest-Report** | Ergebnisse Unit-Tests | Coverage >80% |
| **Referenz-Signal-Report** | Validierung aller Algorithmen | **PFLICHT** |
| **Norm-Konformitäts-Report** | EN 50160 Compliance | **PFLICHT** |
| **Event-Erkennungs-Report** | Detection Rate, False Positives | **PFLICHT** |
| **Systemtest-Report** | E2E-Ergebnisse | Screenshots |
| **Anforderungsverifikation** | Traceability Matrix | 100% Muss-Anforderungen |

### 5.3 Referenz-Testszenarien (Pflicht)

Das Team MUSS **definierte PQ-Testszenarien** implementieren:

| Szenario | Parameter | Erwartetes Ergebnis |
|----------|-----------|---------------------|
| Ideales Netz | 230V, 50Hz, rein sinusförmig | THD<1%, keine Events |
| 5% THD | Grundwelle + 5./7./11. Harmonische | THD = 5.0% ±0.1% |
| Spannungseinbruch | 70% für 200ms | Sag Event erkannt |
| Überspannung | 115% für 500ms | Swell Event erkannt |
| Unterbrechung | <1% für 2s | Interruption erkannt |
| Unsymmetrie | L1=230V, L2=220V, L3=240V | Unsymmetrie korrekt |
| Frequenzabweichung | 49.5 Hz, 50.5 Hz | Abweichung erkannt |
| Flicker | 10 Hz Modulation | Pst berechnet |

### 5.4 Netz-Simulator-Anforderungen

Der Simulator MUSS generieren können:
- Reine Sinussignale (50 Hz, einstellbare Amplitude)
- Oberschwingungen (bis 50. Ordnung, einstellbare Amplitude)
- Spannungseinbrüche/Überspannungen (Dauer, Tiefe einstellbar)
- Frequenzabweichungen
- Unsymmetrische Dreiphasensysteme

---

## 6. Spezielle Projektanforderungen

### 6.1 Research-Komponente: Algorithmen-Vergleich (Pflicht)

Das Team MUSS einen **Vergleich von PQ-Analysealgorithmen** durchführen:

1. **FFT-Synchronisation:**
   - Zero-Crossing Detection
   - PLL (Phase-Locked Loop)
   - Interpolierte FFT

2. **RMS-Berechnung:**
   - Standard RMS über Fenster
   - Sliding Window RMS
   - DFT-basiertes RMS

3. **Event-Erkennung:**
   - Schwellwert-basiert
   - RMS-Verlauf
   - Wavelet-basiert

**Deliverables:**
- Research-Report (mind. 12 Seiten)
- Vergleichsmetriken (Genauigkeit, Latenz)
- Empfehlungen für verschiedene Anwendungsfälle

### 6.2 Normen-Dokumentation (Pflicht)

Das Team MUSS die **relevanten Normen** dokumentieren und umsetzen:

| Norm | Inhalt | Implementierung |
|------|--------|-----------------|
| EN 50160 | Spannungsqualität | Grenzwerte, Reporting |
| IEC 61000-4-30 | Messmethoden | Algorithmen |
| IEC 61000-4-7 | Oberschwingungsmessung | FFT-Fensterung |
| IEC 61000-4-15 | Flickermessung | Optional |

**Deliverable:** Normen-Zusammenfassung (mind. 8 Seiten)

### 6.3 Hardware-Integration (Optional für Bonus)

Teams können für Bonuspunkte echte Messgeräte integrieren:
- Raspberry Pi mit ADC für Niederspannungsmessung
- USB-Oszilloskop mit Spannungsteiler
- Industrielle PQ-Meter via Modbus

Hardware wird bei Bedarf gestellt.

### 6.4 Prozess-Anforderungen

| Anforderung | Beschreibung |
|-------------|--------------|
| Code-Reviews | Jeder PR benötigt 1 Approval |
| Algorithmen-Reviews | PQ-Algorithmen: Review durch 2 Personen |
| Norm-Validierung | Grenzwerte gegen Norm prüfen |
| Sprint-Reviews | Alle 2 Wochen mit Demo |

---

## 7. Abnahmekriterien

### 7.1 Muss-Kriterien für Projektabnahme

1. [ ] Alle Muss-Anforderungen erfüllt
2. [ ] Netz-Simulator generiert alle geforderten Szenarien
3. [ ] FFT-basierte Oberschwingungsanalyse korrekt (validiert)
4. [ ] THD-Berechnung nach IEC korrekt
5. [ ] RMS, Power, PF korrekt berechnet
6. [ ] Event-Erkennung (Sag, Swell, Interruption) funktioniert
7. [ ] EN 50160 Report-Generator funktioniert
8. [ ] Referenz-Signal-Tests bestanden
9. [ ] Algorithmen-Vergleich durchgeführt
10. [ ] Normen-Dokumentation liegt vor
11. [ ] Code-Coverage >80%
12. [ ] Docker-Deployment funktioniert

### 7.2 Bewertungsschema

| Kategorie | Gewicht | Kriterien |
|-----------|---------|-----------|
| Messgenauigkeit | 25% | Validierung gegen Referenz |
| Norm-Konformität | 20% | EN 50160, IEC 61000 |
| Funktionalität | 15% | Erfüllung der Anforderungen |
| Event-Erkennung | 15% | Detection Rate, False Positives |
| Research-Komponente | 15% | Algorithmen-Vergleich |
| Prozessqualität | 10% | Reviews, Dokumentation |

---

## 8. Warum dieses Projekt für KI-Zeitalter geeignet ist

| Aspekt | Begründung |
|--------|------------|
| **Normenwissen** | EN 50160, IEC 61000 müssen verstanden werden |
| **Präzisions-Algorithmen** | Genauigkeit ist kritisch, nicht trivial |
| **Domänenwissen** | Elektrotechnik-Grundlagen (Dreiphasensystem) |
| **Validierung** | Korrektheit muss bewiesen werden |
| **Mehrere Analyseebenen** | FFT, RMS, Events - verschiedene Zeitskalen |
| **Industrierelevanz** | Echtes Problem, echte Standards |
| **Reporting** | Nicht triviale Report-Generierung |

---

## Projekt genehmigt

Offenburg, den 14.01.2026

_____Dipl.-Ing. Martin Schuster_____

GridWatch Energy Solutions GmbH
Dipl.-Ing. Martin Schuster
Technischer Leiter GridWatch Energy Solutions GmbH
