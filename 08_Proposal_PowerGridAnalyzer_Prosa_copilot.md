# Project Proposal: PowerGrid Analyzer - Netzqualitäts-Monitoring-System (Copilot-Version)

## Projekteckdaten

Die GridWatch Energy Solutions GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung eines Netzqualitäts-Analysesystems. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 35.000 Euro. Ansprechpartner ist Dipl.-Ing. Frank Neumann (Technischer Leiter). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von GitHub Copilot (Claude Haiku/Sonnet).

---

## 1. Ausgangssituation und Projektziel

Die GridWatch Energy Solutions GmbH entwickelt Monitoring-Systeme für elektrische Energieversorgungsnetze. Oberschwingungen und Spannungseinbrüche sind wichtige Themen für die Netzqualität.

Das Ziel ist eine Plattform zur Analyse der Netzqualität, die Spannungssignale erfasst (simuliert), Parameter berechnet und Events erkennt.

---

## 2. Fachlicher Hintergrund

Das europäische Netz arbeitet mit 230V und 50 Hz. Oberschwingungen sind Vielfache der Grundfrequenz. Der THD (Total Harmonic Distortion) fasst alle Oberschwingungen zusammen. Spannungseinbrüche sind kurzzeitige Absenkungen der Spannung.

---

## 3. Gewünschte Funktionalität

### Signalerfassung (Kernfunktionalität)

Das System verarbeitet einphasige Spannungssignale (vereinfacht gegenüber Dreiphasensystem).

Ein Netz-Simulator generiert verschiedene Szenarien: ideales Netz, Netz mit Oberschwingungen, Spannungseinbrüche.

Import von Messdaten aus CSV-Dateien.

### Oberschwingungsanalyse (Kernfunktionalität)

Die Analyse basiert auf der FFT. Das System berechnet das Spektrum und zeigt die Amplituden der Harmonischen (Grundwelle, 3., 5., 7. bis zur 15.).

Der THD wird berechnet und angezeigt.

### Berechnung von Netzqualitätsparametern (Kernfunktionalität)

Der RMS-Wert der Spannung wird berechnet. Die Netzfrequenz wird gemessen.

Vergleich mit Grenzwerten (z.B. THD < 8%).

### Event-Erkennung (Kernfunktionalität)

Spannungseinbrüche werden erkannt, wenn der RMS-Wert unter 90% fällt. Tiefe und Dauer werden protokolliert.

Jedes Event wird mit Zeitstempel gespeichert.

### Dashboard (Kernfunktionalität)

Echtzeit-Anzeige von Spannungsverlauf und Frequenzspektrum. Aktuelle Werte für RMS, Frequenz, THD.

Event-Liste zeigt alle erkannten Ereignisse.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. MathNet.Numerics für Berechnungen.

PostgreSQL speichert Events und Konfiguration.

Das Frontend basiert auf Vue.js 3 mit Chart.js.

Das System wird via Docker bereitgestellt.

---

## 5. Qualitätsanforderungen

Die RMS-Berechnung muss auf ±1% genau sein. Die THD-Berechnung muss plausible Ergebnisse liefern.

Event-Erkennung mit Latenz unter 500ms. Dashboard-Updates mit 1 Hz.

---

## 6. Dokumentations- und Testanforderungen

V-Modell-Standarddokumentation plus eine kurze Algorithmen-Dokumentation für FFT und RMS-Berechnung.

Referenz-Testszenarien: ideales Netz, Netz mit 5% THD, Spannungseinbruch auf 80%.

Code-Coverage über 60%.

---

## 7. Vereinfachte Forschungskomponente

Das Team vergleicht verschiedene Methoden zur RMS-Berechnung: Standard-Formel vs. gleitender Durchschnitt.

Ein Report von 4-5 Seiten beschreibt die Methoden und deren Vor-/Nachteile.

---

## Hinweis zur KI-Unterstützung

Dieses Projekt ist für die Bearbeitung mit GitHub Copilot (Claude Haiku/Sonnet) ausgelegt. Copilot unterstützt bei:
- Code-Vervollständigung und Boilerplate-Generierung
- Einfachen Debugging-Aufgaben
- Code-Erklärungen und Dokumentation

Die Studierenden müssen aktiv die Architekturentscheidungen treffen und den generierten Code verstehen und überprüfen.

---

Offenburg, den 14.01.2026

Dipl.-Ing. Martin Schuster
Technischer Leiter GridWatch Energy Solutions GmbH
