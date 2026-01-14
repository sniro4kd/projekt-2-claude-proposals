# Project Proposal: WaveForge - Interaktive DSP-Lern- und Simulationsplattform

---

| Eigenschaft | Wert |
|-------------|------|
| **Firma** | EduSignal Technologies GmbH |
| **Projekt** | WaveForge |
| **Product Owner** | Prof. Dr. Ing. Andreas Körner |
| **Projektlaufzeit** | März - Juli 2026 |
| **Budget** | 35.000 Euro |
| **Version** | 1.0 |
| **Datum** | 14.01.2026 |
| **Zielgruppe** | 6-7 Studierende, 4.-6. Semester Angewandte Informatik / Elektrotechnik |
| **Aufwand pro Person** | 30-40 Stunden (mit KI-Assistenten) |

---

## 1. Projektbeschreibung

### 1.1 Hintergrund

Die EduSignal Technologies GmbH entwickelt **Lernsoftware für technische Hochschulen**. In der Lehre der digitalen Signalverarbeitung fehlen oft interaktive Tools, die Studierenden ermöglichen, DSP-Konzepte praktisch zu erleben.

Es soll eine **webbasierte DSP-Simulationsplattform** entwickelt werden, die:
- Interaktives Filterdesign mit Echtzeit-Visualisierung bietet
- Modulationsverfahren simuliert und visualisiert
- Signale generieren, transformieren und analysieren kann
- C-Code für Embedded-Targets exportieren kann

### 1.2 Besondere Herausforderung: Theorie erlebbar machen

Dieses Projekt verbindet **DSP-Theorie** mit **interaktiver Visualisierung**:
- Mathematische Konzepte werden durch Echtzeit-Interaktion verständlich
- Parameter-Änderungen zeigen sofort Auswirkungen
- Export-Funktion schlägt Brücke zu Embedded-Systemen
- Vergleich verschiedener Verfahren ermöglicht tiefes Verständnis

### 1.3 Projektziele

1. Entwicklung einer interaktiven Web-Plattform für DSP-Simulation
2. Implementierung von Filterdesign-Tools (FIR, IIR)
3. Simulation von Modulationsverfahren (AM, FM, ASK, FSK, PSK, QAM)
4. Echtzeit-Visualisierung aller Signale im Zeit- und Frequenzbereich
5. Code-Generator für C/C++ Embedded-Implementierungen

---

## 2. Funktionale Anforderungen

### 2.1 Signalgenerator

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-101 | Das System MUSS Sinussignale mit konfigurierbarer Frequenz/Amplitude generieren | Muss |
| FA-102 | Das System MUSS Rechteck-, Dreieck- und Sägezahnsignale generieren | Muss |
| FA-103 | Das System MUSS weißes und rosa Rauschen generieren | Muss |
| FA-104 | Das System MUSS Chirp-Signale (Frequenzsweep) generieren | Muss |
| FA-105 | Das System MUSS Signale addieren/multiplizieren können | Muss |
| FA-106 | Das System SOLL Impulse und Sprungfunktionen generieren | Soll |
| FA-107 | Das System SOLL Audio-Upload für Analyse ermöglichen | Soll |
| FA-108 | Das System KANN Mikrofon-Eingang nutzen | Kann |

### 2.2 Filterdesign-Modul

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-201 | Das System MUSS FIR-Filter mit Window-Methode designen | Muss |
| FA-202 | Das System MUSS Tiefpass, Hochpass, Bandpass, Bandsperre unterstützen | Muss |
| FA-203 | Das System MUSS Frequenzgang (Magnitude + Phase) visualisieren | Muss |
| FA-204 | Das System MUSS Impulsantwort und Sprungantwort anzeigen | Muss |
| FA-205 | Das System MUSS Pol-Nullstellen-Diagramm anzeigen | Muss |
| FA-206 | Das System MUSS Filterkoeffizienten anzeigen und exportieren | Muss |
| FA-207 | Das System SOLL IIR-Filter (Butterworth) designen | Soll |
| FA-208 | Das System SOLL IIR-Filter (Chebyshev Typ I/II) designen | Soll |
| FA-209 | Das System SOLL Parks-McClellan Algorithmus für FIR implementieren | Soll |
| FA-210 | Das System SOLL interaktive Pol-Nullstellen-Platzierung ermöglichen | Soll |
| FA-211 | Das System KANN elliptische Filter (Cauer) designen | Kann |

### 2.3 Modulationsverfahren

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-301 | Das System MUSS Amplitudenmodulation (AM) simulieren | Muss |
| FA-302 | Das System MUSS Frequenzmodulation (FM) simulieren | Muss |
| FA-303 | Das System MUSS ASK (Amplitude Shift Keying) simulieren | Muss |
| FA-304 | Das System MUSS FSK (Frequency Shift Keying) simulieren | Muss |
| FA-305 | Das System MUSS PSK (Phase Shift Keying) simulieren | Muss |
| FA-306 | Das System MUSS Modulator UND Demodulator implementieren | Muss |
| FA-307 | Das System SOLL QAM (Quadrature Amplitude Modulation) simulieren | Soll |
| FA-308 | Das System SOLL Konstellationsdiagramme für digitale Modulation anzeigen | Soll |
| FA-309 | Das System SOLL Augendiagramme für ISI-Analyse anzeigen | Soll |
| FA-310 | Das System KANN OFDM-Grundlagen demonstrieren | Kann |
| FA-311 | Das System KANN Rauscheinfluss auf BER simulieren | Kann |

### 2.4 Visualisierung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-401 | Das System MUSS Zeitsignal (Oszilloskop-Ansicht) anzeigen | Muss |
| FA-402 | Das System MUSS Frequenzspektrum (FFT) anzeigen | Muss |
| FA-403 | Das System MUSS Spektrogramm anzeigen | Muss |
| FA-404 | Das System MUSS Echtzeit-Updates bei Parameter-Änderung zeigen | Muss |
| FA-405 | Das System MUSS Zoom, Pan und Cursor-Readout unterstützen | Muss |
| FA-406 | Das System SOLL mehrere Signale überlagert darstellen | Soll |
| FA-407 | Das System SOLL Split-View (Zeit + Frequenz) bieten | Soll |
| FA-408 | Das System SOLL Export als PNG/SVG ermöglichen | Soll |
| FA-409 | Das System KANN Audio-Wiedergabe von Signalen ermöglichen | Kann |

### 2.5 Code-Generator (Embedded-Export)

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-501 | Das System MUSS Filterkoeffizienten als C-Array exportieren | Muss |
| FA-502 | Das System MUSS C-Funktion für FIR-Filterung generieren | Muss |
| FA-503 | Das System MUSS Header-Dateien mit Konfiguration generieren | Muss |
| FA-504 | Das System SOLL C-Code für IIR-Filterung (Direct Form II) generieren | Soll |
| FA-505 | Das System SOLL Fixed-Point-Implementierung (Q15, Q31) generieren | Soll |
| FA-506 | Das System SOLL CMSIS-DSP kompatiblen Code generieren | Soll |
| FA-507 | Das System KANN Python/NumPy-Code exportieren | Kann |
| FA-508 | Das System KANN MATLAB-Code exportieren | Kann |

### 2.6 Lern-Modus

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-601 | Das System MUSS erklärende Texte zu jedem Modul anzeigen | Muss |
| FA-602 | Das System MUSS mathematische Formeln (LaTeX) darstellen | Muss |
| FA-603 | Das System SOLL vordefinierte Beispiel-Szenarien bieten | Soll |
| FA-604 | Das System SOLL interaktive Tutorials anbieten | Soll |
| FA-605 | Das System KANN Quiz-Funktionen für Selbsttest bieten | Kann |

---

## 3. Nicht-funktionale Anforderungen

### 3.1 Performance

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-701 | Visualisierung MUSS mit 30 FPS aktualisieren | Muss |
| NFA-702 | Filterdesign-Berechnung MUSS unter 100ms dauern | Muss |
| NFA-703 | FFT (4096 Punkte) MUSS unter 20ms im Browser laufen | Muss |
| NFA-704 | Das System MUSS auf durchschnittlicher Hardware flüssig laufen | Muss |

### 3.2 Usability

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-801 | Das System MUSS ohne Installation im Browser laufen | Muss |
| NFA-802 | Das System MUSS auf Desktop und Tablet funktionieren | Muss |
| NFA-803 | Das System MUSS intuitive Slider für Parameter bieten | Muss |
| NFA-804 | Das System SOLL Keyboard-Shortcuts unterstützen | Soll |
| NFA-805 | Das System SOLL Undo/Redo für Änderungen bieten | Soll |

### 3.3 Genauigkeit

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-901 | Filterkoeffizienten MÜSSEN numerisch stabil berechnet werden | Muss |
| NFA-902 | Visualisierungen MÜSSEN mathematisch korrekt sein | Muss |
| NFA-903 | Generierter C-Code MUSS kompilierbar und korrekt sein | Muss |

---

## 4. Technische Vorgaben

### 4.1 Tech-Stack

| Komponente | Technologie | Begründung |
|------------|-------------|------------|
| Backend | C# / ASP.NET Core 9 | Firmenstandard, Code-Generierung |
| DSP-Backend | MathNet.Numerics | Filterdesign-Algorithmen |
| Frontend | Vue.js 3 + TypeScript | Interaktivität |
| DSP-Frontend | Web Audio API + eigene Implementierung | Echtzeit-Audio |
| Visualisierung | D3.js + Canvas API | Performance |
| Formeldarstellung | KaTeX oder MathJax | LaTeX-Rendering |
| Datenbank | PostgreSQL | User-Projekte, Presets |
| Container | Docker, Docker Compose | Deployment |

### 4.2 Architektur

```
┌─────────────────────────────────────────────────────────────────────────┐
│                         Web Browser (Client)                             │
├─────────────────────────────────────────────────────────────────────────┤
│                                                                          │
│  ┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐          │
│  │  Signal         │  │  Filter         │  │  Modulation     │          │
│  │  Generator      │  │  Designer       │  │  Simulator      │          │
│  │  (Vue Component)│  │  (Vue Component)│  │  (Vue Component)│          │
│  └────────┬────────┘  └────────┬────────┘  └────────┬────────┘          │
│           │                    │                    │                    │
│           ▼                    ▼                    ▼                    │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │              DSP Engine (TypeScript/WebAssembly)                 │    │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐            │    │
│  │  │   FFT   │  │ Filters │  │  Mod/   │  │  Audio  │            │    │
│  │  │         │  │         │  │  Demod  │  │  I/O    │            │    │
│  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘            │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│           │                    │                    │                    │
│           ▼                    ▼                    ▼                    │
│  ┌─────────────────────────────────────────────────────────────────┐    │
│  │              Visualization Layer (D3.js + Canvas)                │    │
│  │  ┌─────────┐  ┌─────────┐  ┌─────────┐  ┌─────────┐            │    │
│  │  │  Time   │  │  Freq   │  │ Spectro │  │  Pole/  │            │    │
│  │  │  Plot   │  │  Plot   │  │  gram   │  │  Zero   │            │    │
│  │  └─────────┘  └─────────┘  └─────────┘  └─────────┘            │    │
│  └─────────────────────────────────────────────────────────────────┘    │
│                                                                          │
└─────────────────────────────────────────────────────────────────────────┘
                                  │
                                  │ REST API
                                  ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                          Backend (ASP.NET Core)                          │
├─────────────────┬─────────────────┬─────────────────┬───────────────────┤
│  Advanced       │  Code           │  Project        │  Tutorial         │
│  Filter Design  │  Generator      │  Storage        │  Content          │
│  (MathNet)      │  (C/Python)     │  (CRUD)         │  (Markdown)       │
└────────┬────────┴────────┬────────┴────────┬────────┴─────────┬─────────┘
         │                 │                 │                   │
         └─────────────────┴────────┬────────┴───────────────────┘
                                    │
                                    ▼
                          ┌─────────────────┐
                          │   PostgreSQL    │
                          │   (Projects,    │
                          │    Presets)     │
                          └─────────────────┘
```

---

## 5. Pflichtdokumentation nach V-Modell

### 5.1 Erforderliche Dokumente

| Phase | Dokument | Besonderheit |
|-------|----------|--------------|
| Anforderungen | Lastenheft | Lernziele definieren |
| Spezifikation | Pflichtenheft | DSP-Algorithmen mathematisch spezifizieren |
| Entwurf | High-Level-Design | Client/Server-Architektur |
| Entwurf | Low-Level-Design | DSP-Engine Design |
| Entwurf | **Filterdesign-Dokumentation** | **PFLICHT** - Alle Algorithmen |
| Entwurf | **Modulations-Dokumentation** | **PFLICHT** - Alle Verfahren |
| Projektmanagement | ADRs | Mind. 5, davon 2 zu DSP im Browser |
| Projektmanagement | Lernkonzept | **PFLICHT** - Didaktisches Konzept |

### 5.2 Pflicht-Testdokumentation

| Dokument | Inhalt | Spezielle Anforderungen |
|----------|--------|-------------------------|
| **Mastertestplan** | Teststrategie inkl. numerischer Validierung | DSP-Validierungsstrategie |
| **Komponententest-Spezifikation** | Unit-Tests für DSP-Module | Mind. 80 Testfälle |
| **Filterdesign-Tests** | Tests für alle Filtertypen | **PFLICHT** - Mind. 30 Tests |
| **Modulations-Tests** | Tests für alle Modulationsverfahren | **PFLICHT** - Mind. 20 Tests |
| **Code-Generator-Tests** | Validierung generierter Code | **PFLICHT** - Kompiliert und korrekt |
| **Integrationstest-Spezifikation** | Frontend-Backend Integration | Mind. 15 Testfälle |
| **Usability-Test-Spezifikation** | User-Tests mit Studierenden | Mind. 5 Testpersonen |
| **Komponententest-Report** | Ergebnisse Unit-Tests | Coverage >80% |
| **Filterdesign-Report** | Validierung gegen MATLAB/SciPy | **PFLICHT** - Mit Plots |
| **Modulations-Report** | BER-Kurven, Spektren | **PFLICHT** |
| **Code-Generator-Report** | Test auf Embedded-Target | Mind. 1 Target |
| **Usability-Report** | Feedback von Testpersonen | Mit Verbesserungsvorschlägen |
| **Anforderungsverifikation** | Traceability Matrix | 100% Muss-Anforderungen |

### 5.3 Filterdesign-Validierung (Pflicht)

Das Team MUSS **alle implementierten Filter** gegen Referenzimplementierungen validieren:

| Filtertyp | Referenz | Validierungskriterien |
|-----------|----------|----------------------|
| FIR Tiefpass | SciPy firwin | Koeffizienten ±0.001% |
| FIR Bandpass | SciPy firwin | Frequenzgang-Match |
| IIR Butterworth | SciPy butter | Pol/Nullstellen-Match |
| IIR Chebyshev | SciPy cheby1/cheby2 | Ripple-Spezifikation |

### 5.4 Code-Generator-Validierung (Pflicht)

Der generierte Code MUSS auf mindestens einem Embedded-Target validiert werden:

| Test | Beschreibung |
|------|--------------|
| Kompilierung | Code kompiliert ohne Fehler (GCC ARM) |
| Numerische Korrektheit | Ausgabe identisch zu Simulation |
| Performance | Echtzeitfähig auf Cortex-M4 |

---

## 6. Spezielle Projektanforderungen

### 6.1 Research-Komponente: Filterdesign-Vergleich (Pflicht)

Das Team MUSS einen systematischen **Vergleich von Filterdesign-Methoden** durchführen:

1. **FIR-Design-Methoden:**
   - Window-Methode (verschiedene Fenster)
   - Frequenz-Sampling
   - Parks-McClellan (Optimal)

2. **IIR-Design-Methoden:**
   - Butterworth (Maximal flach)
   - Chebyshev (Ripple-Optimiert)
   - Elliptisch (Schärfste Transition)

3. **Vergleichskriterien:**
   - Ordnung für gleiche Spezifikation
   - Gruppenaufzeit
   - Implementierungsaufwand
   - Numerische Stabilität

**Deliverables:**
- Research-Report (mind. 12 Seiten)
- Interaktiver Vergleich im Tool
- Empfehlungs-Guide für Anwender

### 6.2 Didaktisches Konzept (Pflicht)

Das Team MUSS ein **Lernkonzept** erstellen:

| Element | Beschreibung |
|---------|--------------|
| Lernziele | Pro Modul definierte Lernziele |
| Progression | Einfach → Komplex Struktur |
| Beispiele | Mind. 10 vordefinierte Szenarien |
| Erklärungen | Mathematische Hintergründe |
| Visualisierung | Welche Darstellung für welches Konzept |

**Deliverable:** Didaktisches Konzept (mind. 6 Seiten)

### 6.3 Embedded-Integration (Optional für Bonus)

Teams können für Bonuspunkte:
- Generierter Code auf STM32/ESP32 validieren
- Live-Verbindung zum Mikrocontroller (USB)
- Vergleich Simulation vs. reale Hardware

Hardware wird bei Bedarf gestellt.

### 6.4 Prozess-Anforderungen

| Anforderung | Beschreibung |
|-------------|--------------|
| Code-Reviews | Jeder PR benötigt 1 Approval |
| Mathe-Reviews | DSP-Algorithmen: Review durch 2 Personen |
| User-Tests | Mind. 2 Iterationen mit Feedback |
| Sprint-Reviews | Alle 2 Wochen mit Demo |

---

## 7. Abnahmekriterien

### 7.1 Muss-Kriterien für Projektabnahme

1. [ ] Alle Muss-Anforderungen erfüllt
2. [ ] Signalgenerator mit mind. 5 Signaltypen
3. [ ] FIR-Filterdesign (Window-Methode) funktioniert
4. [ ] Mind. 1 IIR-Filtertyp implementiert
5. [ ] AM und FM Modulation/Demodulation funktioniert
6. [ ] Mind. 2 digitale Modulationsverfahren implementiert
7. [ ] Alle Visualisierungen funktionieren in Echtzeit
8. [ ] C-Code-Export funktioniert und kompiliert
9. [ ] Filterdesign-Vergleich durchgeführt
10. [ ] Didaktisches Konzept liegt vor
11. [ ] Code-Coverage >80%
12. [ ] Docker-Deployment funktioniert

### 7.2 Bewertungsschema

| Kategorie | Gewicht | Kriterien |
|-----------|---------|-----------|
| DSP-Korrektheit | 25% | Validierung gegen Referenz |
| Interaktivität | 20% | Echtzeit, Usability |
| Funktionsumfang | 15% | Filter, Modulation, Visualisierung |
| Code-Generator | 15% | Qualität, Korrektheit |
| Research-Komponente | 15% | Filterdesign-Vergleich |
| Didaktik | 10% | Lernkonzept, Tutorials |

---

## 8. Warum dieses Projekt für KI-Zeitalter geeignet ist

| Aspekt | Begründung |
|--------|------------|
| **Mathematische Tiefe** | Filterdesign erfordert DSP-Verständnis |
| **Algorithmen-Vielfalt** | Viele verschiedene Verfahren implementieren |
| **Validierung** | Numerische Korrektheit beweisen |
| **Cross-Domain** | Web-Entwicklung + DSP + Embedded |
| **Code-Generierung** | Nicht trivial, erfordert Verständnis |
| **User-Experience** | Interaktivität erfordert Design-Entscheidungen |
| **Didaktik** | Erklärungen verfassen erfordert Verständnis |

---

## Projekt genehmigt

Offenburg, den 14.01.2026

_____Prof. Dr. Ing. Heinrich Wagner_____

EduSignal Technologies GmbH
Prof. Dr. Ing. Heinrich Wagner
Geschäftsführer EduSignal Technologies GmbH
