# Project Proposal: SmartCampus IoT Platform

## Projekteckdaten

Die TechEdu Solutions GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung einer IoT-Plattform für intelligentes Gebäudemanagement. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 35.000 Euro. Ansprechpartnerin ist Dr. Maria Schneider (Product Owner). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von KI-Assistenten.

---

## 1. Ausgangssituation und Projektziel

Die TechEdu Solutions GmbH entwickelt Softwarelösungen für Bildungseinrichtungen. Um die Digitalisierung an Hochschulen voranzutreiben, soll eine IoT-Plattform für intelligentes Gebäudemanagement entwickelt werden.

Das Problem: In Hörsälen und Seminarräumen fehlt oft der Überblick über die tatsächliche Nutzung und die Raumluftqualität. Räume werden beheizt oder gekühlt, obwohl sie leer stehen. Bei hoher CO2-Konzentration wird nicht gelüftet, was die Konzentrationsfähigkeit beeinträchtigt. Studierende suchen vergeblich nach freien Lernplätzen.

Das System soll Sensordaten aus Hörsälen erfassen - CO2-Gehalt, Temperatur, Luftfeuchtigkeit und Belegung - diese visualisieren und bei Grenzwertüberschreitungen automatisch Aktionen auslösen, sei es eine Benachrichtigung an das Facility Management oder die Ansteuerung der Lüftungsanlage.

---

## 2. Fachlicher Hintergrund

IoT-Systeme basieren auf dem Zusammenspiel von Sensoren, Datenübertragung und Auswertung. Sensoren messen physikalische Größen und übermitteln diese typischerweise per MQTT (Message Queuing Telemetry Transport), einem leichtgewichtigen Protokoll, das für ressourcenbeschränkte Geräte optimiert ist.

Die Herausforderung bei Sensordaten liegt in der schieren Menge: Hundert Sensoren, die alle zehn Sekunden Daten senden, erzeugen über 800.000 Datenpunkte pro Tag. Klassische relationale Datenbanken stoßen hier an Grenzen. Zeitreihendatenbanken wie InfluxDB oder TimescaleDB sind auf solche Anwendungsfälle spezialisiert.

Für die Visualisierung in Echtzeit müssen Daten vom Server zum Browser "gepusht" werden können. WebSockets oder Server-Sent Events ermöglichen diese bidirektionale Kommunikation.

---

## 3. Gewünschte Funktionalität

### Backend-System

Das Herzstück des Systems ist ein Backend, das Sensordaten entgegennimmt, speichert und verarbeitet. Die Kommunikation mit Sensoren soll über das MQTT-Protokoll erfolgen, das in der IoT-Welt weitverbreitet ist. Die Daten werden in einer Zeitreihendatenbank gespeichert, die für genau diese Art von Daten optimiert ist.

Neben den Rohdaten benötigt das System eine Möglichkeit, Grenzwerte zu konfigurieren - ab welcher CO2-Konzentration soll gewarnt werden? Welche Temperatur ist zu hoch? Diese Konfiguration muss flexibel sein und für verschiedene Räume unterschiedlich einstellbar.

Wenn Grenzwerte überschritten werden, soll das System Events auslösen können. Das kann eine E-Mail-Benachrichtigung sein, ein Eintrag in einem Alarm-Log, oder im Idealfall das Einschalten eines Aktors wie einer Lüftung.

Für Auswertungen und Berichte müssen die Daten aggregiert werden können - Durchschnittswerte pro Stunde, Tag, Woche oder Monat. Eine REST-API macht die Daten für Frontends und externe Systeme verfügbar. Die Integration externer Kalendersysteme würde ermöglichen, Raumbelegungsdaten mit Vorlesungsplänen abzugleichen.

### Web-Dashboard

Das Dashboard ist die zentrale Schnittstelle für Facility Manager und Administratoren. Es zeigt Echtzeitdaten aller Sensoren an und muss sofort aktualisiert werden, wenn neue Messwerte eintreffen.

Historische Daten sollen als Diagramme darstellbar sein - Temperaturverlauf über den Tag, CO2-Entwicklung während einer Vorlesung. Alarme müssen visuell hervorgehoben und von den Nutzern quittierbar sein.

Eine Gebäude- oder Raumübersicht in Kartenform würde die Orientierung erleichtern - wo genau ist gerade die CO2-Konzentration kritisch? Export-Funktionen für Berichte runden das Dashboard ab.

### Mobile App

Für Studierende ist eine mobile App interessant, die verfügbare Räume mit ihrer aktuellen Auslastung anzeigt. Wo ist gerade ein freier Platz zum Lernen? Welche Temperatur herrscht dort?

Studierende sollten Räume als Favoriten speichern können und benachrichtigt werden, wenn ihr Lieblingslernplatz frei wird. Indoor-Navigation wäre ein spannendes Feature für größere Campus.

### Hardware-Integration

Für die Entwicklung und Tests wird zunächst ein Sensor-Simulator benötigt, der realistische Datenverläufe generiert - nicht einfach Zufallswerte, sondern plausible Muster wie einen ansteigenden CO2-Gehalt bei zunehmender Belegung.

Das System soll aber auch mit echter Hardware funktionieren können. ESP32 oder Arduino-basierte Sensoren sind kostengünstig und gut dokumentiert. Als Erweiterung könnten auch Aktoren angesteuert werden - eine LED, die bei Grenzwertüberschreitung aufleuchtet, oder ein Relay, das eine Lüftung einschaltet.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt, da dies dem Firmenstandard entspricht. Als Message Broker für die MQTT-Kommunikation kommen RabbitMQ oder Mosquitto in Frage.

Die Zeitreihendaten werden in InfluxDB oder TimescaleDB gespeichert, relationale Daten (Benutzer, Konfigurationen) in PostgreSQL. Redis dient als Cache für häufig abgefragte Daten und Sessions.

Das Frontend kann mit Vue.js 3 oder React 18 entwickelt werden - die Entscheidung liegt beim Team. Für die mobile App bieten sich Cross-Platform-Frameworks wie Flutter oder React Native an.

Das gesamte System muss via Docker und Docker Compose deploybar sein. Wer Bonuspunkte sammeln möchte, kann eine Kubernetes-Variante mit K3s implementieren.

---

## 5. Qualitätsanforderungen

Das System muss mindestens 100 Sensoren gleichzeitig verarbeiten können, ohne dass die Performance leidet. Die Dashboard-Latenz - die Zeit vom Eintreffen eines Messwerts bis zur Anzeige - muss unter zwei Sekunden liegen.

Eine Verfügbarkeit von 99% über die Projektlaufzeit ist anzustreben. Sensordaten müssen mindestens 90 Tage gespeichert werden, um Trends analysieren zu können.

Falls eine mobile App entwickelt wird, sollte diese auf iOS und Android laufen.

---

## 6. Dokumentations- und Testanforderungen

Das Projekt folgt dem V-Modell. Neben den üblichen Dokumenten (Lastenheft, Pflichtenheft, High-Level- und Low-Level-Design, ADRs) wird besonderer Wert auf die Testdokumentation gelegt.

Der Mastertestplan beschreibt die Teststrategie. Für Unit-Tests sind mindestens 50 Testfälle zu dokumentieren, für Integrationstests mindestens 20, für Systemtests mindestens 15 End-to-End-Szenarien. Die Code-Coverage soll über 80% liegen.

Besonders wichtig sind Lasttests, die zeigen, dass das System mit 100 simulierten Sensoren stabil läuft. Mindestens 5 Lasttest-Szenarien sind zu dokumentieren.

---

## 7. Forschungskomponente

Als Research-Komponente muss das Team eine der folgenden Aufgaben bearbeiten:

Erstens: Ein Vorhersage-Algorithmus für die Raumbelegung. Mindestens drei verschiedene Ansätze (z.B. lineare Regression, ARIMA, einfaches Machine Learning) sollen verglichen und statistisch ausgewertet werden.

Zweitens: Ein Algorithmus zur Anomalie-Erkennung, der ungewöhnliche Sensormuster identifiziert - etwa ein plötzlicher Temperaturanstieg, der auf einen Defekt hindeuten könnte.

Drittens: Eine Simulation und Analyse von Energieeinsparungen durch intelligente Lüftungssteuerung - wie viel CO2 und Kosten könnten gespart werden?

Das Ergebnis ist ein Research-Report von mindestens 10 Seiten mit Methodik, Ergebnissen und Diskussion.

---

## 8. Optionale Erweiterungen

Für Bonuspunkte können Teams echte Hardware integrieren: ESP32 mit BME280-Sensor für Temperatur und Luftfeuchtigkeit, MH-Z19 für CO2, PIR-Sensor für Bewegungserkennung. Die Hardware wird bei Bedarf gestellt.

---

Offenburg, den 13.01.2026

Dr. Thomas Weber
CTO TechEdu Solutions GmbH
