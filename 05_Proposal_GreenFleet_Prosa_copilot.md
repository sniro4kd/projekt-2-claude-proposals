# Project Proposal: GreenFleet - Nachhaltiges Flottenmanagement (Copilot-Version)

## Projekteckdaten

Die EcoLogistics AG beauftragt ein Team von 6-7 Studierenden mit der Entwicklung eines Flottenmanagement-Systems. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 38.000 Euro. Ansprechpartnerin ist Sarah Klein (Product Owner). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von GitHub Copilot (Claude Haiku/Sonnet).

---

## 1. Ausgangssituation und Projektziel

Die EcoLogistics AG betreibt einen Lieferdienst mit Fahrzeugen - ein Mix aus Verbrennern und Elektrofahrzeugen. Das Unternehmen möchte seinen CO2-Fußabdruck reduzieren.

Das Ziel ist ein Flottenmanagement-System, das Fahrzeugdaten verwaltet, Routen plant und CO2-Emissionen berechnet.

---

## 2. Fachlicher Hintergrund

Das System kombiniert Fahrzeugverwaltung mit einfacher Routenplanung und CO2-Berechnung.

---

## 3. Gewünschte Funktionalität

### Fahrzeugverwaltung (Kernfunktionalität)

Jedes Fahrzeug wird mit Stammdaten erfasst: Kennzeichen, Fahrzeugtyp (Verbrenner, Elektro), Verbrauch pro 100km, CO2-Ausstoß pro Kilometer.

Der aktuelle Status ist ersichtlich: verfügbar, unterwegs, in Wartung.

### Kartenansicht mit Fahrzeugpositionen (Kernfunktionalität)

Eine Kartenansicht zeigt die Positionen aller Fahrzeuge. Für Entwicklung und Test werden die Positionen von einem einfachen Simulator generiert.

Die Karte basiert auf OpenStreetMap mit Leaflet.

### Einfache Tourenplanung (Kernfunktionalität)

Eine Tour umfasst Start, mehrere Stopps und Ziel. Das System berechnet die Route und zeigt sie auf der Karte.

Die Routenberechnung nutzt eine externe API (OSRM oder GraphHopper).

### CO2-Tracking (Kernfunktionalität)

Für jede Fahrt werden die CO2-Emissionen berechnet basierend auf Fahrzeugtyp und gefahrener Strecke.

Ein Dashboard zeigt die Gesamtemissionen pro Fahrzeug und für die gesamte Flotte.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. PostgreSQL speichert alle Daten.

Das Frontend nutzt Vue.js 3 mit Leaflet für die Kartenvisualisierung.

Für das Routing wird OSRM oder GraphHopper verwendet.

Das System wird via Docker deployed.

---

## 5. Qualitätsanforderungen

Eine Route mit 10 Stopps muss in unter 5 Sekunden berechnet werden.

Das System muss Daten von 10 simulierten Fahrzeugen verwalten können.

---

## 6. Dokumentations- und Testanforderungen

V-Modell-Standarddokumentation.

Die Testdokumentation umfasst Unit- und Integrationstests. Mindestens 15 Unit-Tests, 8 Integrationstests.

Code-Coverage über 60%.

---

## 7. Vereinfachte Forschungskomponente

Das Team entwickelt ein einfaches CO2-Berechnungsmodell. Der Report (4-5 Seiten) beschreibt:
- CO2-Werte für verschiedene Fahrzeugtypen
- Vergleich mit offiziellen Daten (Herstellerangaben)
- Berechnung der Einsparung bei Elektrofahrzeugen

---

## Hinweis zur KI-Unterstützung

Dieses Projekt ist für die Bearbeitung mit GitHub Copilot (Claude Haiku/Sonnet) ausgelegt. Copilot unterstützt bei:
- Code-Vervollständigung und Boilerplate-Generierung
- Einfachen Debugging-Aufgaben
- Code-Erklärungen und Dokumentation

Die Studierenden müssen aktiv die Architekturentscheidungen treffen und den generierten Code verstehen und überprüfen.

---

Offenburg, den 13.01.2026

Thomas Grün
CSO EcoLogistics AG
