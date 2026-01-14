# Project Proposal: PowerGrid Analyzer - Netzqualitäts-Monitoring-System

## Projekteckdaten

Die GridWatch Energy Solutions GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung eines Netzqualitäts-Analysesystems. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 35.000 Euro. Ansprechpartner ist Dipl.-Ing. Frank Neumann (Technischer Leiter). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von KI-Assistenten.

---

## 1. Ausgangssituation und Projektziel

Die GridWatch Energy Solutions GmbH entwickelt Monitoring-Systeme für elektrische Energieversorgungsnetze. Mit der Energiewende und der zunehmenden Integration von Photovoltaik-Anlagen, Windkraftwerken und Elektrofahrzeugen wird die Netzqualität (Power Quality) zu einem immer wichtigeren Thema.

Oberschwingungen, die von Schaltnetzteilen und Frequenzumrichtern erzeugt werden, können empfindliche Elektronik stören. Spannungseinbrüche durch Laständerungen oder Fehler im Netz können Produktionsanlagen zum Stillstand bringen. Die Dokumentation der Netzqualität nach europäischen Normen ist für Netzbetreiber und Industriekunden gleichermaßen relevant.

Das Ziel dieses Projekts ist die Entwicklung einer Plattform zur Analyse der Netzqualität. Diese soll Spannungs- und Stromsignale erfassen (zunächst simuliert, optional mit echter Hardware), die relevanten Parameter berechnen, Events wie Spannungseinbrüche erkennen und dokumentieren, sowie normkonforme Berichte erstellen.

---

## 2. Fachlicher Hintergrund

Das europäische Niederspannungsnetz arbeitet mit 230V Nennspannung und 50 Hz Nennfrequenz. In Industrieanlagen werden meist Dreiphasensysteme verwendet mit drei um 120° versetzten Spannungen (L1, L2, L3). Im Idealfall sind alle drei Spannungen gleich groß und perfekt sinusförmig - in der Realität gibt es jedoch Abweichungen.

Oberschwingungen sind Vielfache der Grundfrequenz (50 Hz). Die 5. Harmonische hat 250 Hz, die 7. hat 350 Hz. Sie entstehen durch nichtlineare Lasten wie Schaltnetzteile, LED-Lampen oder Frequenzumrichter. Der THD (Total Harmonic Distortion) fasst alle Oberschwingungen in einer Kennzahl zusammen. Die Norm EN 50160 definiert Grenzwerte für den THD und einzelne Harmonische.

Spannungsevents werden nach Tiefe und Dauer klassifiziert. Ein Spannungseinbruch (Sag) ist eine kurzzeitige Absenkung auf typischerweise 10-90% der Nennspannung. Eine Überspannung (Swell) ist eine Erhöhung über 110%. Eine Unterbrechung liegt vor, wenn die Spannung unter 1% fällt. Die ITIC-Kurve (früher CBEMA) definiert, welche Kombinationen aus Tiefe und Dauer für elektronische Geräte tolerierbar sind.

Weitere relevante Parameter sind die Frequenzabweichung (normalerweise im Bereich ±0.5 Hz), die Spannungsunsymmetrie zwischen den drei Phasen, und der Flicker - schnelle Spannungsschwankungen, die zum Flackern von Lampen führen können.

Die Messung dieser Parameter folgt internationalen Normen. IEC 61000-4-30 definiert die Messmethoden, IEC 61000-4-7 die Oberschwingungsmessung mit synchronisierter FFT, und IEC 61000-4-15 die Flickermessung.

---

## 3. Gewünschte Funktionalität

### Signalerfassung

Das System muss dreiphasige Signale verarbeiten können: drei Spannungen (L1, L2, L3 gegen Neutralleiter) und optional drei Ströme. Die Abtastrate sollte mindestens 10 kHz betragen, um Oberschwingungen bis zur 50. Ordnung korrekt zu erfassen.

Für Entwicklung und Test wird ein Netz-Simulator benötigt, der verschiedene Szenarien generieren kann: ideales Netz, Netz mit definierten Oberschwingungen, Spannungseinbrüche verschiedener Tiefe und Dauer, Frequenzabweichungen, und unsymmetrische Belastungen.

Der Import von Messdaten aus Dateien sollte unterstützt werden. Das COMTRADE-Format ist ein Industriestandard für Störschreiberdaten, CSV für einfachere Anwendungsfälle. Für Echtzeit-Anwendungen wäre eine WebSocket-Schnittstelle wünschenswert, und MQTT für die Integration externer Messgeräte.

### Oberschwingungsanalyse

Die Analyse basiert auf der FFT, die synchron zur Netzfrequenz durchgeführt werden muss. Das bedeutet, dass das Messfenster exakt eine oder mehrere Perioden der Grundschwingung umfassen muss. Dazu wird eine Synchronisation benötigt, typischerweise über Zero-Crossing-Erkennung oder eine digitale PLL (Phase-Locked Loop).

Das System muss das Spektrum berechnen und die Amplituden der einzelnen Harmonischen (Grundwelle, 3., 5., 7. usw. bis zur 50.) anzeigen. Der THD wird aus diesen Werten berechnet. Auch Interharmonische - Frequenzen zwischen den Harmonischen - sollten erkannt werden können, da diese von bestimmten Lasten wie Frequenzumrichtern erzeugt werden.

Für Langzeitüberwachung sind Trends interessant: Wie entwickelt sich der THD über Stunden, Tage, Wochen? Statistische Auswertungen zeigen, wie oft Grenzwerte überschritten werden.

### Berechnung von Netzqualitätsparametern

Der True-RMS-Wert der Spannung muss korrekt berechnet werden, nicht nur für reine Sinusschwingungen, sondern auch bei verzerrten Signalen mit Oberschwingungen. Die Netzfrequenz muss präzise gemessen werden, mit einer Genauigkeit von mindestens 10 mHz.

Bei Dreiphasensystemen ist die Unsymmetrie ein wichtiger Parameter. Sie gibt an, wie stark die drei Phasenspannungen voneinander abweichen. Die Berechnung erfolgt über symmetrische Komponenten (Mitsystem, Gegensystem, Nullsystem).

Die Leistungsberechnung umfasst Wirkleistung P, Blindleistung Q, Scheinleistung S und den Leistungsfaktor PF. Bei oberschwingungsbehafteten Signalen ist die korrekte Berechnung nicht trivial.

Die Flickermessung nach IEC 61000-4-15 ist komplex und umfasst eine Kette von Filtern und statistischen Auswertungen. Der kurzfristige Flicker Pst (über 10 Minuten) und der langfristige Plt (über 2 Stunden) sind die Ergebnisse.

Alle Parameter müssen mit den Grenzwerten der EN 50160 verglichen werden können.

### Event-Erkennung

Spannungsereignisse müssen in Echtzeit erkannt werden. Ein Einbruch beginnt, wenn der RMS-Wert unter eine Schwelle (typisch 90% der Nennspannung) fällt, und endet, wenn er wieder darüber steigt. Die Tiefe (minimaler Wert während des Events) und die Dauer werden protokolliert.

Entsprechend werden Überspannungen (über 110%) und Unterbrechungen (unter 1%) erkannt. Jedes Event wird mit Zeitstempel, Dauer, Tiefe/Höhe und betroffener Phase gespeichert.

Die Klassifizierung nach ITIC-Kurve zeigt, ob das Event für typische IT-Geräte problematisch war. Die Wellenform sollte mit Pre- und Post-Trigger (einige Perioden vor und nach dem Event) gespeichert werden, um die Ursache analysieren zu können.

Transienten - sehr kurze Überspannungsspitzen - sind schwieriger zu erkennen und erfordern höhere Abtastraten und spezielle Algorithmen.

### Dashboard und Visualisierung

Das Dashboard muss einen schnellen Überblick über den aktuellen Netzzustand geben. Echtzeit-Anzeigen der Spannungs- und Stromverläufe aller drei Phasen, das Oberschwingungsspektrum als Balkendiagramm, und aktuelle Werte für RMS, Frequenz, THD, Leistung.

Ein Phasordiagramm (Zeigerdiagramm) zeigt die drei Phasenspannungen in der komplexen Ebene und macht Unsymmetrien sofort sichtbar.

Die Event-Liste zeigt alle erkannten Ereignisse mit Filterung nach Typ, Schwere und Zeitraum. Die ITIC-Kurve visualisiert, wo die Events im kritischen Bereich liegen.

Historische Trends zeigen die Entwicklung der Netzqualität über Zeit. Alarme bei Grenzwertüberschreitungen informieren den Benutzer über kritische Zustände.

### Berichterstattung

Das System muss Berichte nach EN 50160 generieren können. Diese enthalten statistische Auswertungen: für welchen Prozentsatz der Zeit lagen die Parameter innerhalb der Grenzwerte? Die Norm fordert typischerweise, dass 95% oder 99% der Messwerte innerhalb der Grenzen liegen.

Wöchentliche und monatliche Zusammenfassungen geben einen Überblick über die Netzqualität im Zeitraum. Event-Reports dokumentieren einzelne Störungen mit Wellenformen.

Die Berichte werden als PDF exportiert und sollten optional per E-Mail verschickt werden können.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. Für die numerischen Berechnungen steht MathNet.Numerics zur Verfügung. Die Speicherung von Zeitreihendaten erfolgt in InfluxDB oder TimescaleDB, relationale Daten (Events, Konfiguration) in PostgreSQL.

Das Frontend basiert auf Vue.js 3 mit Chart.js und D3.js für die Visualisierungen. Echtzeit-Updates erfolgen über SignalR.

Für die Report-Generierung wird eine PDF-Bibliothek wie QuestPDF oder iText verwendet. Hangfire übernimmt die zeitgesteuerte Generierung von Berichten.

Das System wird via Docker bereitgestellt.

---

## 5. Qualitätsanforderungen

Die Genauigkeit der Messungen ist kritisch. Die RMS-Berechnung muss auf ±0.1% genau sein, die Frequenzmessung auf ±10 mHz, die THD-Berechnung muss den Vorgaben der IEC entsprechen.

Die FFT muss synchron zur Netzfrequenz erfolgen, um korrekte Harmonischen-Amplituden zu erhalten. Event-Zeitstempel müssen auf ±1 ms genau sein, um Events verschiedener Messpunkte korrelieren zu können.

Die Event-Erkennung muss mit einer Latenz unter 100 ms erfolgen. Das Dashboard soll mit 1 Hz aktualisiert werden. Das System muss mindestens 10 Messpunkte gleichzeitig verwalten können.

---

## 6. Dokumentations- und Testanforderungen

Eine spezielle Normen-Dokumentation fasst die relevanten Abschnitte aus EN 50160 und IEC 61000-4-30 zusammen und beschreibt, wie die Anforderungen umgesetzt werden. Eine Algorithmen-Dokumentation erklärt die Berechnungsverfahren für FFT-Synchronisation, RMS, THD und Event-Erkennung.

Für die Validierung muss eine Suite von Referenz-Testszenarien erstellt werden. Diese umfasst ein ideales 50-Hz-Netz, Szenarien mit definiertem THD (z.B. exakt 5%), Spannungseinbrüche verschiedener Tiefe und Dauer, Überspannungen, Unterbrechungen, Frequenzabweichungen, und unsymmetrische Belastungen. Für jedes Szenario muss das erwartete Ergebnis dokumentiert sein.

Die Event-Erkennung muss mit Precision und Recall bewertet werden: werden alle Events erkannt (Recall), und sind die erkannten Events auch tatsächlich Events (Precision)?

Die Code-Coverage soll mindestens 80% betragen. Algorithmen für Netzqualitätsparameter erfordern Reviews durch mindestens zwei Personen.

---

## 7. Forschungskomponente

Das Team soll einen Vergleich verschiedener Algorithmen durchführen. Bei der FFT-Synchronisation werden Zero-Crossing-Erkennung, digitale PLL und interpolierte FFT verglichen. Bei der RMS-Berechnung Standard-RMS, Sliding-Window-RMS und DFT-basiertes RMS. Bei der Event-Erkennung schwellwertbasierte Verfahren, RMS-Verlaufsanalyse und Wavelet-basierte Methoden.

Vergleichskriterien sind Genauigkeit, Latenz, Robustheit gegen Störungen und Implementierungsaufwand.

Das Ergebnis ist ein Research-Report von mindestens 12 Seiten mit Messungen, Grafiken und Empfehlungen.

---

## 8. Optionale Erweiterungen

Für Bonuspunkte können Teams echte Messhardware integrieren. Ein Raspberry Pi mit ADC könnte Niederspannungssignale (über Spannungsteiler) erfassen. USB-Oszilloskope bieten eine weitere Möglichkeit. Für industrielle Anwendungen könnte ein PQ-Meter via Modbus angebunden werden. Die Hardware wird bei Bedarf gestellt.

---

Offenburg, den 14.01.2026

Dipl.-Ing. Martin Schuster
Technischer Leiter GridWatch Energy Solutions GmbH
