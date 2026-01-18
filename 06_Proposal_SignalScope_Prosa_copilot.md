# Project Proposal: SignalScope - Echtzeit-Signalanalyse-Plattform (Copilot-Version)

## Projekteckdaten

Die SensorTech Analytics GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung einer Signalanalyse-Plattform. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 35.000 Euro. Ansprechpartner ist Dr. Ing. Markus Reichert (CTO). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von GitHub Copilot (Claude Haiku/Sonnet).

---

## 1. Ausgangssituation und Projektziel

Die SensorTech Analytics GmbH entwickelt Lösungen für industrielle Zustandsüberwachung (Condition Monitoring). Vibrationssensoren an Maschinen liefern Daten, die analysiert werden müssen.

Das Ziel ist die Entwicklung einer webbasierten Signalanalyse-Plattform, die Sensordaten entgegennimmt, mittels FFT analysiert und die Ergebnisse visualisiert.

---

## 2. Fachlicher Hintergrund

Die digitale Signalverarbeitung (DSP) bildet das Herzstück dieses Projekts. Die Fast Fourier Transformation (FFT) wandelt ein Zeitsignal in seine Frequenzbestandteile um. Statistische Kennwerte wie RMS (Effektivwert) sind grundlegende Indikatoren.

---

## 3. Gewünschte Funktionalität

### Signalerfassung (Kernfunktionalität)

Die Plattform nimmt Signaldaten über eine REST-API entgegen. Der Import von CSV-Dateien ist möglich.

Ein integrierter Signalgenerator erzeugt Testsignale: Sinus, Rechteck und Rauschen mit konfigurierbarer Frequenz und Amplitude.

### Signalverarbeitung (Kernfunktionalität)

Die DSP-Engine implementiert die Fast Fourier Transformation (FFT). Daraus wird das Frequenzspektrum berechnet.

Einfache Filter (Tiefpass, Hochpass) können auf das Signal angewendet werden.

Statistische Kennwerte: RMS, Spitzenwert, Mittelwert.

### Visualisierung (Kernfunktionalität)

Signale werden visualisiert: Zeitbereich (Oszilloskop-Ansicht) und Frequenzspektrum (FFT).

Interaktive Funktionen: Zoom und Pan. Mehrere Signale können verglichen werden.

### Einfache Schwellwertüberwachung

Für definierte Frequenzbänder können Grenzwerte festgelegt werden. Bei Überschreitung wird eine Warnung angezeigt.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. Für die numerischen Berechnungen steht MathNet.Numerics zur Verfügung.

PostgreSQL speichert Messdaten und Konfigurationen.

Das Frontend wird mit Vue.js 3 entwickelt, für die Visualisierungen kommt Chart.js zum Einsatz.

Das System wird via Docker deployed.

---

## 5. Qualitätsanforderungen

Die FFT-Berechnung mit 4096 Punkten muss unter 100ms dauern.

Das Dashboard muss flüssige Updates ermöglichen.

Die FFT-Ergebnisse müssen mit einer Referenz (z.B. NumPy) übereinstimmen.

---

## 6. Dokumentations- und Testanforderungen

V-Modell-Standarddokumentation plus eine kurze DSP-Dokumentation, die die FFT erklärt.

Für die Validierung werden Referenz-Testsignale erstellt: Sinustöne bekannter Frequenz, Rechteck, Rauschen.

Code-Coverage über 60%.

---

## 7. Vereinfachte Forschungskomponente

Das Team vergleicht verschiedene Fensterfunktionen (Rechteck, Hanning, Hamming) bei der FFT und dokumentiert deren Auswirkungen auf das Spektrum.

Ein Report von 5 Seiten mit Grafiken zeigt die Unterschiede.

---

## Hinweis zur KI-Unterstützung

Dieses Projekt ist für die Bearbeitung mit GitHub Copilot (Claude Haiku/Sonnet) ausgelegt. Copilot unterstützt bei:
- Code-Vervollständigung und Boilerplate-Generierung
- Einfachen Debugging-Aufgaben
- Code-Erklärungen und Dokumentation

Die Studierenden müssen aktiv die Architekturentscheidungen treffen und den generierten Code verstehen und überprüfen.

---

Offenburg, den 14.01.2026

Dr. Ing. Klaus Brenner
CTO SensorTech Analytics GmbH
