# Project Proposal: SmartCampus IoT Platform (Copilot-Version)

## Projekteckdaten

Die TechEdu Solutions GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung einer IoT-Plattform für intelligentes Gebäudemanagement. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 35.000 Euro. Ansprechpartnerin ist Dr. Maria Schneider (Product Owner). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von GitHub Copilot (Claude Haiku/Sonnet).

---

## 1. Ausgangssituation und Projektziel

Die TechEdu Solutions GmbH entwickelt Softwarelösungen für Bildungseinrichtungen. Um die Digitalisierung an Hochschulen voranzutreiben, soll eine IoT-Plattform für intelligentes Gebäudemanagement entwickelt werden.

Das Problem: In Hörsälen und Seminarräumen fehlt oft der Überblick über die tatsächliche Nutzung und die Raumluftqualität. Räume werden beheizt oder gekühlt, obwohl sie leer stehen.

Das System soll Sensordaten aus Hörsälen erfassen - CO2-Gehalt, Temperatur und Belegung - diese visualisieren und bei Grenzwertüberschreitungen Benachrichtigungen auslösen.

---

## 2. Fachlicher Hintergrund

IoT-Systeme basieren auf dem Zusammenspiel von Sensoren, Datenübertragung und Auswertung. Sensoren messen physikalische Größen und übermitteln diese typischerweise per MQTT (Message Queuing Telemetry Transport), einem leichtgewichtigen Protokoll.

---

## 3. Gewünschte Funktionalität

### Backend-System (Kernfunktionalität)

Das Backend nimmt Sensordaten entgegen, speichert diese und verarbeitet sie. Die Kommunikation mit Sensoren erfolgt über MQTT. Die Daten werden in einer Datenbank gespeichert.

Das System benötigt eine Möglichkeit, Grenzwerte zu konfigurieren - ab welcher CO2-Konzentration soll gewarnt werden? Wenn Grenzwerte überschritten werden, soll eine E-Mail-Benachrichtigung oder ein Log-Eintrag erfolgen.

Eine REST-API macht die Daten für das Frontend verfügbar.

### Web-Dashboard (Kernfunktionalität)

Das Dashboard zeigt aktuelle Sensordaten an. Es zeigt Echtzeitdaten aller Sensoren mit regelmäßiger Aktualisierung.

Historische Daten werden als einfache Diagramme darstellbar sein - Temperaturverlauf über den Tag. Eine Übersicht aller Räume mit Status (OK/Warnung) ermöglicht schnelle Orientierung.

### Sensor-Simulator (Kernfunktionalität)

Für die Entwicklung wird ein Sensor-Simulator benötigt, der realistische Datenverläufe generiert - plausible Muster wie einen ansteigenden CO2-Gehalt bei zunehmender Belegung.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. Als Message Broker für MQTT kommt Mosquitto in Frage.

Die Daten werden in PostgreSQL gespeichert (relationale Daten und Sensordaten).

Das Frontend kann mit Vue.js 3 oder React 18 entwickelt werden.

Das gesamte System muss via Docker und Docker Compose deploybar sein.

---

## 5. Qualitätsanforderungen

Das System muss mindestens 20 simulierte Sensoren gleichzeitig verarbeiten können. Die Dashboard-Aktualisierung soll im 5-Sekunden-Intervall erfolgen.

Sensordaten müssen mindestens 30 Tage gespeichert werden.

---

## 6. Dokumentations- und Testanforderungen

Das Projekt folgt dem V-Modell. Neben den üblichen Dokumenten (Lastenheft, Pflichtenheft, High-Level-Design) wird Wert auf grundlegende Tests gelegt.

Für Unit-Tests sind mindestens 20 Testfälle zu dokumentieren, für Integrationstests mindestens 10. Die Code-Coverage soll über 60% liegen.

---

## 7. Vereinfachte Forschungskomponente

Als Research-Komponente analysiert das Team verschiedene Ansätze zur Grenzwertüberwachung: einfache statische Schwellwerte vs. gleitende Durchschnitte. Ein kurzer Report (5 Seiten) dokumentiert die Vor- und Nachteile.

---

## Hinweis zur KI-Unterstützung

Dieses Projekt ist für die Bearbeitung mit GitHub Copilot (Claude Haiku/Sonnet) ausgelegt. Copilot unterstützt bei:
- Code-Vervollständigung und Boilerplate-Generierung
- Einfachen Debugging-Aufgaben
- Code-Erklärungen und Dokumentation

Die Studierenden müssen aktiv die Architekturentscheidungen treffen und den generierten Code verstehen und überprüfen.

---

Offenburg, den 13.01.2026

Dr. Thomas Weber
CTO TechEdu Solutions GmbH
