# Project Proposal: WaveForge - Interaktive DSP-Lern- und Simulationsplattform (Copilot-Version)

## Projekteckdaten

Die EduSignal Technologies GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung einer interaktiven DSP-Lernplattform. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 35.000 Euro. Ansprechpartner ist Prof. Dr. Ing. Andreas Körner. Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von GitHub Copilot (Claude Haiku/Sonnet).

---

## 1. Ausgangssituation und Projektziel

Die EduSignal Technologies GmbH entwickelt Lernsoftware für technische Hochschulen. In der Lehre der digitalen Signalverarbeitung besteht eine Lücke zwischen Theorie und Praxis.

Das Ziel ist eine webbasierte DSP-Simulationsplattform, die Studierenden ermöglicht, Konzepte interaktiv zu erkunden. Parameter können verändert werden und die Auswirkungen sind sofort sichtbar.

---

## 2. Fachlicher Hintergrund

Die digitale Signalverarbeitung umfasst Filter, die unerwünschte Frequenzanteile entfernen. FIR-Filter (Finite Impulse Response) sind stabil und einfacher zu verstehen. Beim Filterdesign gibt es verschiedene Methoden, die Window-Methode ist am einfachsten.

---

## 3. Gewünschte Funktionalität

### Signalgenerator (Kernfunktionalität)

Grundlegende Signalformen: Sinus, Rechteck, Dreieck mit konfigurierbarer Frequenz und Amplitude. Rauschsignale für Tests. Signale können addiert werden.

### Filterdesign-Modul (Kernfunktionalität)

Der Benutzer wählt einen Filtertyp (Tiefpass, Hochpass), gibt Parameter an (Grenzfrequenz, Ordnung) und sieht das Ergebnis.

Die Visualisierung zeigt den Frequenzgang (Betrag) und die Impulsantwort. Die Filterkoeffizienten werden angezeigt.

Die Window-Methode mit verschiedenen Fensterfunktionen (Rechteck, Hanning, Hamming) wird implementiert.

### Visualisierung (Kernfunktionalität)

Signale werden in Echtzeit visualisiert: Zeitbereich und Frequenzspektrum (FFT).

Interaktive Funktionen: Zoom und Parameter-Slider. Split-View mit Zeit- und Frequenzdarstellung nebeneinander.

### Lernmodus (Kernfunktionalität)

Zu jedem Modul werden erklärende Texte angezeigt. Formeln werden mit LaTeX dargestellt.

Vordefinierte Beispiel-Szenarien: "Design eines Tiefpassfilters", "Vergleich verschiedener Fensterfunktionen".

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt, ergänzt durch MathNet.Numerics.

Das Frontend basiert auf Vue.js 3 mit TypeScript. Die DSP-Engine für FFT und Filter läuft im Browser.

Die Visualisierung nutzt Chart.js oder Canvas API. Formeln werden mit KaTeX gerendert.

PostgreSQL speichert Benutzerprojekte. Das System wird via Docker bereitgestellt.

---

## 5. Qualitätsanforderungen

Die Visualisierung muss flüssig sein mit mindestens 20 FPS bei Parameteränderungen.

Filterdesign-Berechnungen unter 200ms, FFT mit 2048 Punkten unter 50ms im Browser.

Die Filterkoeffizienten müssen mit Referenzimplementierungen (SciPy) übereinstimmen.

---

## 6. Dokumentations- und Testanforderungen

V-Modell-Standarddokumentation plus eine Filterdesign-Dokumentation, die die implementierten Algorithmen beschreibt.

Filter werden gegen Referenzimplementierungen validiert.

Code-Coverage über 60%.

---

## 7. Vereinfachte Forschungskomponente

Das Team vergleicht verschiedene Fensterfunktionen beim FIR-Filterdesign: Rechteck, Hanning, Hamming, Blackman.

Vergleichskriterien: Frequenzauflösung, Sperrdämpfung, benötigte Filterordnung.

Ein Report von 5-6 Seiten mit Grafiken und Empfehlungen.

---

## Hinweis zur KI-Unterstützung

Dieses Projekt ist für die Bearbeitung mit GitHub Copilot (Claude Haiku/Sonnet) ausgelegt. Copilot unterstützt bei:
- Code-Vervollständigung und Boilerplate-Generierung
- Einfachen Debugging-Aufgaben
- Code-Erklärungen und Dokumentation

Die Studierenden müssen aktiv die Architekturentscheidungen treffen und den generierten Code verstehen und überprüfen.

---

Offenburg, den 14.01.2026

Prof. Dr. Ing. Heinrich Wagner
Geschäftsführer EduSignal Technologies GmbH
