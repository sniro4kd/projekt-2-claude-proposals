# Project Proposal: SignalScope - Echtzeit-Signalanalyse-Plattform

---

| Eigenschaft | Wert |
|-------------|------|
| **Firma** | SensorTech Analytics GmbH |
| **Projekt** | SignalScope |
| **Product Owner** | Dr. Ing. Markus Reichert |
| **Projektlaufzeit** | März - Juli 2026 |
| **Budget** | 35.000 Euro |
| **Version** | 1.0 |
| **Datum** | 14.01.2026 |
| **Zielgruppe** | 6-7 Studierende, 4.-6. Semester Angewandte Informatik / Elektrotechnik |
| **Aufwand pro Person** | 30-40 Stunden (mit KI-Assistenten) |

---

## 1. Projektbeschreibung

### 1.1 Hintergrund

Die SensorTech Analytics GmbH entwickelt Lösungen für **industrielle Zustandsüberwachung (Condition Monitoring)**. In modernen Fertigungsanlagen ist die frühzeitige Erkennung von Maschinenverschleiß durch Vibrationsanalyse ein Schlüsselfaktor für Predictive Maintenance.

Es soll eine **Echtzeit-Signalanalyse-Plattform** entwickelt werden, die:
- Vibrations- und Audiosignale erfasst und analysiert
- Digitale Signalverarbeitung (FFT, Filter, Spektralanalyse) durchführt
- Anomalien in Signalen automatisch erkennt
- Ein Dashboard für Ingenieure und Techniker bereitstellt

### 1.2 Besondere Herausforderung: DSP meets Software Engineering

Dieses Projekt verbindet **Elektrotechnik/DSP-Theorie** mit **moderner Softwareentwicklung**:
- Implementierung klassischer DSP-Algorithmen (FFT, Filterdesign, Spektralanalyse)
- Echtzeit-Datenverarbeitung mit Streaming-Architektur
- Machine Learning für Anomalieerkennung
- Vergleich von Algorithmen-Performance (Research-Komponente)

### 1.3 Projektziele

1. Entwicklung einer skalierbaren Signalanalyse-Backend-Plattform
2. Implementierung von DSP-Algorithmen für Vibrations-/Audioanalyse
3. Echtzeit-Dashboard mit Spektrogrammen und Zeitreihenvisualisierung
4. Automatische Anomalieerkennung mit konfigurierbaren Schwellwerten
5. Research: Vergleich verschiedener Analyse-Algorithmen

---

## 2. Funktionale Anforderungen

### 2.1 Signalerfassung und -eingabe

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-101 | Das System MUSS Signaldaten via REST-API empfangen können | Muss |
| FA-102 | Das System MUSS WAV/CSV-Dateien für Batch-Analyse importieren können | Muss |
| FA-103 | Das System MUSS einen Signalgenerator für Testsignale bereitstellen | Muss |
| FA-104 | Das System MUSS verschiedene Abtastraten unterstützen (1kHz - 48kHz) | Muss |
| FA-105 | Das System SOLL Echtzeit-Streaming via WebSocket unterstützen | Soll |
| FA-106 | Das System SOLL Mikrofonaudio via Browser-API erfassen können | Soll |
| FA-107 | Das System KANN MQTT für Sensor-Integration unterstützen | Kann |

### 2.2 Digitale Signalverarbeitung (Kernmodul)

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-201 | Das System MUSS FFT (Fast Fourier Transform) implementieren | Muss |
| FA-202 | Das System MUSS Leistungsdichtespektrum (PSD) berechnen können | Muss |
| FA-203 | Das System MUSS Spektrogramme (STFT) generieren können | Muss |
| FA-204 | Das System MUSS FIR-Filter (Tiefpass, Hochpass, Bandpass) implementieren | Muss |
| FA-205 | Das System MUSS Fensterfunktionen unterstützen (Hanning, Hamming, Blackman) | Muss |
| FA-206 | Das System MUSS RMS, Peak, Crest-Faktor berechnen können | Muss |
| FA-207 | Das System SOLL IIR-Filter (Butterworth, Chebyshev) implementieren | Soll |
| FA-208 | Das System SOLL Hüllkurvenanalyse (Envelope) durchführen können | Soll |
| FA-209 | Das System SOLL Cepstrum-Analyse für Maschinendiagnose implementieren | Soll |
| FA-210 | Das System KANN Ordnungsanalyse für rotierende Maschinen implementieren | Kann |

### 2.3 Anomalieerkennung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-301 | Das System MUSS Schwellwertüberwachung für Frequenzbänder implementieren | Muss |
| FA-302 | Das System MUSS Alarme bei Grenzwertüberschreitung generieren | Muss |
| FA-303 | Das System MUSS historische Baselines für Normalzustand speichern | Muss |
| FA-304 | Das System SOLL statistische Anomalieerkennung (Z-Score, IQR) implementieren | Soll |
| FA-305 | Das System SOLL Trendanalyse für langsame Verschlechterung durchführen | Soll |
| FA-306 | Das System KANN ML-basierte Anomalieerkennung (Isolation Forest) implementieren | Kann |
| FA-307 | Das System KANN typische Fehlermuster klassifizieren (Unwucht, Lagerschaden) | Kann |

### 2.4 Visualisierung und Dashboard

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-401 | Das Dashboard MUSS Zeitsignale als Liniendiagramm anzeigen | Muss |
| FA-402 | Das Dashboard MUSS Frequenzspektren anzeigen (linear/logarithmisch) | Muss |
| FA-403 | Das Dashboard MUSS Spektrogramme als Heatmap anzeigen | Muss |
| FA-404 | Das Dashboard MUSS Echtzeit-Updates unterstützen (WebSocket) | Muss |
| FA-405 | Das Dashboard MUSS Zoom und Pan für alle Diagramme unterstützen | Muss |
| FA-406 | Das Dashboard MUSS Alarme visuell hervorheben | Muss |
| FA-407 | Das Dashboard SOLL Vergleich mehrerer Signale ermöglichen | Soll |
| FA-408 | Das Dashboard SOLL Cursor-Readout (Frequenz, Amplitude) bieten | Soll |
| FA-409 | Das Dashboard SOLL Export als PNG/CSV ermöglichen | Soll |
| FA-410 | Das Dashboard KANN 3D-Wasserfall-Diagramme darstellen | Kann |

### 2.5 Datenverwaltung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-501 | Das System MUSS Messdaten mit Metadaten speichern können | Muss |
| FA-502 | Das System MUSS Messungen nach Maschine/Messpunkt organisieren | Muss |
| FA-503 | Das System MUSS historische Daten für Trendanalyse vorhalten | Muss |
| FA-504 | Das System SOLL Daten-Annotations (Kommentare, Tags) ermöglichen | Soll |
| FA-505 | Das System SOLL Batch-Export historischer Daten ermöglichen | Soll |

---

## 3. Nicht-funktionale Anforderungen

### 3.1 Performance

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-601 | FFT mit 8192 Punkten MUSS unter 50ms berechnet werden | Muss |
| NFA-602 | Das Dashboard MUSS Echtzeit-Updates mit 10 Hz unterstützen | Muss |
| NFA-603 | Das System MUSS 20 gleichzeitige Signalstreams verarbeiten | Muss |
| NFA-604 | Spektrogramm-Berechnung (1s Audio) MUSS unter 200ms dauern | Muss |
| NFA-605 | Das System SOLL 100 historische Messungen pro Sekunde abfragen können | Soll |

### 3.2 Skalierbarkeit

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-701 | Das System MUSS horizontal skalierbar sein (Worker-Architektur) | Muss |
| NFA-702 | Das System MUSS Analysen in einer Job-Queue verarbeiten | Muss |
| NFA-703 | Das System SOLL mindestens 1 Jahr Messdaten vorhalten können | Soll |
| NFA-704 | Das System SOLL Daten-Downsampling für lange Zeiträume unterstützen | Soll |

### 3.3 Genauigkeit

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-801 | FFT-Ergebnisse MÜSSEN mit Referenzimplementierung (NumPy) übereinstimmen | Muss |
| NFA-802 | Filterkoeffizienten MÜSSEN mathematisch korrekt berechnet werden | Muss |
| NFA-803 | Das System MUSS mit Referenz-Testsignalen validiert werden | Muss |

---

## 4. Technische Vorgaben

### 4.1 Tech-Stack

| Komponente | Technologie | Begründung |
|------------|-------------|------------|
| Backend | C# / ASP.NET Core 9 | Firmenstandard |
| DSP-Bibliothek | MathNet.Numerics / Eigen-Implementierung | Numerische Berechnungen |
| Job Queue | RabbitMQ oder Hangfire | Asynchrone Analyse |
| Zeitreihendatenbank | InfluxDB oder TimescaleDB | Messdaten |
| Relationale Daten | PostgreSQL | Konfiguration, Metadaten |
| Cache | Redis | Berechnungsergebnisse |
| Frontend | Vue.js 3 mit Chart.js / D3.js | Visualisierung |
| WebSocket | SignalR | Echtzeit-Updates |
| Container | Docker, Docker Compose | Deployment |

### 4.2 Architektur

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         Signal Sources                                   │
├─────────────────┬─────────────────┬─────────────────┬───────────────────┤
│  File Upload    │  REST API       │  WebSocket      │  MQTT (Optional)  │
│  (WAV/CSV)      │  (Batch)        │  (Realtime)     │  (Sensors)        │
└────────┬────────┴────────┬────────┴────────┬────────┴─────────┬─────────┘
         │                 │                 │                   │
         ▼                 ▼                 ▼                   ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                          API Gateway (ASP.NET Core)                      │
└─────────────────────────────────┬───────────────────────────────────────┘
                                  │
          ┌───────────────────────┼───────────────────────┐
          │                       │                       │
          ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Ingest Service │    │  Query Service  │    │  Alert Service  │
│  (Daten→Queue)  │    │  (REST API)     │    │  (Monitoring)   │
└────────┬────────┘    └────────┬────────┘    └────────┬────────┘
         │                      │                      │
         ▼                      ▼                      ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                       Message Queue (RabbitMQ)                           │
└─────────────────────────────────┬───────────────────────────────────────┘
                                  │
          ┌───────────────────────┼───────────────────────┐
          ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  DSP Worker     │    │  Anomaly Worker │    │  Export Worker  │
│  (FFT, Filter)  │    │  (Detection)    │    │  (Reports)      │
└────────┬────────┘    └────────┬────────┘    └────────┬────────┘
         │                      │                      │
         └──────────────────────┼──────────────────────┘
                                │
          ┌─────────────────────┼─────────────────────┐
          ▼                     ▼                     ▼
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│   InfluxDB      │  │   PostgreSQL    │  │   Redis Cache   │
│   (Timeseries)  │  │   (Config)      │  │   (Results)     │
└─────────────────┘  └─────────────────┘  └─────────────────┘
                                │
                                ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                    Web Dashboard (Vue.js + SignalR)                      │
├─────────────────┬─────────────────┬─────────────────┬───────────────────┤
│  Time Domain    │  Frequency View │  Spectrogram    │  Alarm Panel      │
│  (Waveform)     │  (Spectrum)     │  (Heatmap)      │  (Alerts)         │
└─────────────────┴─────────────────┴─────────────────┴───────────────────┘
```

---

## 5. Pflichtdokumentation nach V-Modell

### 5.1 Erforderliche Dokumente

| Phase | Dokument | Besonderheit |
|-------|----------|--------------|
| Anforderungen | Lastenheft | Frequenzbänder und Grenzwerte definieren |
| Spezifikation | Pflichtenheft | DSP-Algorithmen mathematisch spezifizieren |
| Entwurf | High-Level-Design | Worker-Architektur, Datenfluss |
| Entwurf | Low-Level-Design | DSP-Algorithmen Pseudocode |
| Entwurf | **DSP-Spezifikation** | **PFLICHT** - Mathematische Grundlagen |
| Projektmanagement | ADRs | Mind. 5, davon 2 zu DSP-Implementierung |
| Projektmanagement | Algorithmen-Vergleich | **PFLICHT** |

### 5.2 Pflicht-Testdokumentation

| Dokument | Inhalt | Spezielle Anforderungen |
|----------|--------|-------------------------|
| **Mastertestplan** | Teststrategie inkl. DSP-Validierung | DSP-Teststrategie beschreiben |
| **Komponententest-Spezifikation** | Unit-Tests für DSP-Module | Mind. 60 Testfälle |
| **Referenz-Signal-Tests** | Testsignale mit bekannten Eigenschaften | **PFLICHT** - Mind. 20 Signale |
| **Integrationstest-Spezifikation** | Service-Kommunikation | Mind. 20 Testfälle |
| **Systemtest-Spezifikation** | End-to-End Szenarien | Mind. 10 Szenarien |
| **Performance-Test-Spezifikation** | Latenz und Durchsatz | Mind. 5 Szenarien |
| **Komponententest-Report** | Ergebnisse Unit-Tests | Coverage >80% |
| **Referenz-Signal-Report** | Validierung gegen NumPy/MATLAB | **PFLICHT** - Mit Plots |
| **Integrationstest-Report** | API-Tests | Alle Services |
| **Systemtest-Report** | E2E-Ergebnisse | Screenshots |
| **Performance-Report** | Latenz-Messungen | Mit Grafiken |
| **Anforderungsverifikation** | Traceability Matrix | 100% Muss-Anforderungen |

### 5.3 Referenz-Signal-Tests (Pflicht)

Das Team MUSS eine **Test-Suite mit definierten Testsignalen** erstellen:

| Signal-Typ | Parameter | Erwartetes Ergebnis |
|------------|-----------|---------------------|
| Sinuston | 1000 Hz, 1V | Peak bei 1000 Hz im Spektrum |
| Chirp | 100-5000 Hz, 1s | Linearer Anstieg im Spektrogramm |
| Weißes Rauschen | Normalverteilt | Flaches Spektrum |
| Impulse | Delta-Funktion | Flaches Spektrum |
| AM-Signal | 1kHz Träger, 100Hz Modulation | Seitenbänder bei 900/1100 Hz |
| Superposition | 440 Hz + 880 Hz | Zwei Peaks |
| Maschinenfehlersimulation | Unwucht bei 25 Hz | Peak bei Drehfrequenz |

**Validierung:** Alle Ergebnisse MÜSSEN mit NumPy/SciPy-Referenzimplementierung verglichen werden.

---

## 6. Spezielle Projektanforderungen

### 6.1 Research-Komponente: Algorithmen-Vergleich (Pflicht)

Das Team MUSS einen systematischen **Vergleich von DSP-Algorithmen** durchführen:

1. **FFT-Implementierungen:**
   - Radix-2 Cooley-Tukey
   - Bluestein (beliebige Längen)
   - Vergleich mit MathNet.Numerics

2. **Fensterfunktionen:**
   - Vergleich von Hanning, Hamming, Blackman, Kaiser
   - Analyse von Frequenzauflösung vs. Leckage

3. **Anomalieerkennung:**
   - Schwellwert-basiert vs. statistisch vs. ML
   - Precision/Recall für verschiedene Fehlerfälle

**Deliverables:**
- Research-Report (mind. 12 Seiten)
- Benchmark-Ergebnisse mit Grafiken
- Empfehlungen für Produktiveinsatz

### 6.2 DSP-Dokumentation (Pflicht)

Das Team MUSS die **mathematischen Grundlagen** dokumentieren:

| Algorithmus | Dokumentation |
|-------------|---------------|
| DFT/FFT | Formel, Komplexität, Implementierung |
| Fensterfunktionen | Formeln, Frequenzantwort, Trade-offs |
| FIR-Filter | Filterdesign-Verfahren, Koeffizientenberechnung |
| IIR-Filter | Bilineare Transformation, Stabilität |
| Spektrogramm | STFT-Parameter (Overlap, Window Size) |

**Deliverable:** DSP-Dokumentation (mind. 8 Seiten mit Formeln und Diagrammen)

### 6.3 Hardware-Integration (Optional für Bonus)

Teams können für Bonuspunkte echte Sensoren integrieren:
- MEMS-Beschleunigungssensor (ADXL345, MPU6050)
- USB-Mikrofon für Audioanalyse
- ESP32 als Datenerfassungseinheit

Hardware wird bei Bedarf gestellt.

### 6.4 Prozess-Anforderungen

| Anforderung | Beschreibung |
|-------------|--------------|
| Code-Reviews | Jeder PR benötigt 1 Approval |
| DSP-Code-Reviews | DSP-Algorithmen benötigen Review durch 2 Personen |
| Sprint-Reviews | Alle 2 Wochen mit Demo |
| Pair Programming | Empfohlen für komplexe DSP-Implementierung |

---

## 7. Abnahmekriterien

### 7.1 Muss-Kriterien für Projektabnahme

1. [ ] Alle Muss-Anforderungen erfüllt
2. [ ] FFT korrekt implementiert (validiert gegen NumPy)
3. [ ] Mindestens 3 Filtertypen implementiert und validiert
4. [ ] Spektrogramm-Visualisierung funktioniert
5. [ ] Anomalieerkennung mit konfigurierbaren Schwellwerten
6. [ ] Referenz-Signal-Tests bestanden
7. [ ] Algorithmen-Vergleich durchgeführt und dokumentiert
8. [ ] DSP-Dokumentation liegt vor
9. [ ] Code-Coverage >80%
10. [ ] Docker-Deployment funktioniert

### 7.2 Bewertungsschema

| Kategorie | Gewicht | Kriterien |
|-----------|---------|-----------|
| DSP-Korrektheit | 25% | Validierung gegen Referenz |
| Funktionalität | 20% | Erfüllung der Anforderungen |
| Visualisierung | 15% | Dashboard-Qualität, Echtzeit |
| Research-Komponente | 15% | Algorithmen-Vergleich |
| Testqualität | 15% | Coverage, Referenz-Tests |
| Prozessqualität | 10% | Reviews, Dokumentation |

---

## 8. Warum dieses Projekt für KI-Zeitalter geeignet ist

| Aspekt | Begründung |
|--------|------------|
| **Mathematische Tiefe** | DSP erfordert echtes Verständnis, nicht nur API-Calls |
| **Algorithmen-Implementierung** | Eigene Implementierung vs. Bibliothek |
| **Validierung** | Numerische Korrektheit muss bewiesen werden |
| **Domänenwissen** | Elektrotechnik-Grundlagen notwendig |
| **Research-Pflicht** | Vergleich erfordert eigenständige Analyse |
| **Echtzeit-Anforderungen** | Performance-Optimierung nötig |
| **Interdisziplinär** | Software Engineering + Signalverarbeitung |

---

## Projekt genehmigt

Offenburg, den 14.01.2026

_____Dr. Ing. Klaus Brenner_____

SensorTech Analytics GmbH
Dr. Ing. Klaus Brenner
CTO SensorTech Analytics GmbH
