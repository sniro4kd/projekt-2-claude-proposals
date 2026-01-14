# Project Proposal: GreenFleet - Nachhaltiges Flottenmanagement

## Projekteckdaten

Die EcoLogistics AG beauftragt ein Team von 6-7 Studierenden mit der Entwicklung eines Flottenmanagement-Systems. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 38.000 Euro. Ansprechpartnerin ist Sarah Klein (Product Owner). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von KI-Assistenten.

---

## 1. Ausgangssituation und Projektziel

Die EcoLogistics AG betreibt einen Lieferdienst mit 50 Fahrzeugen - ein Mix aus Verbrennern, Hybriden und Elektrofahrzeugen. Das Unternehmen hat sich zum Ziel gesetzt, seinen CO2-Fußabdruck zu reduzieren und gleichzeitig die Flottenkosten zu optimieren.

Aktuell fehlt ein zentrales System, das alle Fahrzeuge im Blick hat. Touren werden manuell geplant, oft ohne Berücksichtigung der Fahrzeugtypen - ein Elektrofahrzeug wird für eine Tour eingeplant, die seine Reichweite übersteigt. Die CO2-Emissionen werden nur grob geschätzt, ein aussagekräftiges Reporting für Stakeholder existiert nicht.

Das Ziel ist ein Flottenmanagement-System, das Echtzeitdaten von allen Fahrzeugen erfasst, Routen CO2-optimiert plant (nicht nur nach Zeit oder Strecke), Wartungsintervalle vorhersagt und Nachhaltigkeits-Reports für Stakeholder generiert.

---

## 2. Besondere Herausforderung: Echte Daten und Optimierung

Dieses Projekt kombiniert mehrere komplexe Bereiche. IoT-Datenverarbeitung: GPS-Tracker und OBD-II-Adapter liefern kontinuierlich Daten, die verarbeitet und gespeichert werden müssen. Optimierungsalgorithmen: Die Routenplanung ist ein Vehicle Routing Problem (VRP), ein klassisches Optimierungsproblem der Informatik. Datenanalyse: Aus historischen Daten lassen sich Verbräuche prognostizieren und optimale Wartungszeitpunkte vorhersagen. Externe APIs: Kartendienste, Wetter- und Verkehrsdaten müssen integriert werden.

---

## 3. Gewünschte Funktionalität

### Fahrzeugverwaltung

Jedes Fahrzeug wird mit seinen Stammdaten erfasst: Kennzeichen, Fahrzeugtyp (Verbrenner, Hybrid, Elektro), Ladekapazität. Technische Daten wie Durchschnittsverbrauch, Reichweite und CO2-Ausstoß pro Kilometer werden pro Fahrzeugtyp hinterlegt.

Der aktuelle Status jedes Fahrzeugs ist ersichtlich: verfügbar, unterwegs, in Wartung. Die Wartungshistorie dokumentiert alle durchgeführten Arbeiten. Die Zuordnung von Fahrern zu Fahrzeugen kann verwaltet werden. Termine für Versicherung, TÜV und regelmäßige Inspektionen werden getrackt.

### Echtzeit-Tracking

Eine Kartenansicht zeigt die GPS-Positionen aller Fahrzeuge in Echtzeit. Die Daten können von echten GPS-Trackern stammen oder - für Entwicklung und Test - von einem Simulator generiert werden.

Für jedes Fahrzeug ist die aktuelle Route sichtbar, inklusive Geschwindigkeit und Fahrtrichtung. Geofencing ermöglicht Alerts, wenn ein Fahrzeug einen definierten Bereich verlässt. Historische Fahrten können gespeichert und wie ein Video abgespielt werden.

Die Integration von OBD-II-Daten (On-Board-Diagnose) würde zusätzliche Informationen liefern: aktueller Verbrauch, Motortemperatur, Fehlercodes. Dies erfordert allerdings entsprechende Hardware.

### Routenplanung und Optimierung

Das Herzstück des Systems ist die Tourenplanung. Eine Tour umfasst mehrere Stopps - Abholungen und Lieferungen. Das System plant die optimale Reihenfolge und das optimale Fahrzeug.

Die Optimierung kann nach verschiedenen Kriterien erfolgen: kürzeste Zeit, kürzeste Strecke, oder - das Alleinstellungsmerkmal - minimaler CO2-Ausstoß. Bei der CO2-Optimierung kann es sinnvoll sein, einen kleinen Umweg zu fahren, wenn dadurch ein Elektrofahrzeug statt eines Diesels eingesetzt werden kann.

Bei Elektrofahrzeugen muss das System die Reichweite berücksichtigen und bei Bedarf Ladestopps einplanen. Lieferzeitfenster (der Kunde ist nur zwischen 14 und 16 Uhr erreichbar) und Fahrzeugkapazitäten (der Transporter ist voll) sind weitere Constraints.

Die Einbeziehung von Verkehrslage und Wetterdaten verbessert die Planung. Bei Elektrofahrzeugen beeinflusst kaltes Wetter die Reichweite erheblich. Echtzeit-Umplanung bei unerwarteten Verzögerungen (Stau, Kunde nicht erreichbar) wäre die Kür.

### CO2-Tracking und Reporting

Für jede Fahrt werden die CO2-Emissionen berechnet, basierend auf Fahrzeugtyp, gefahrener Strecke und Fahrprofil. Die Emissionen werden aggregiert: pro Fahrzeug, pro Tag, pro Monat, für die gesamte Flotte.

Ein Vergleich zeigt, wie viel CO2 die optimierte Route gegenüber einer nicht optimierten spart. Das Nachhaltigkeits-Dashboard visualisiert die wichtigsten Kennzahlen. PDF-Reports für Stakeholder dokumentieren die Umweltbilanz.

Die Quantifizierung der CO2-Einsparung durch die Optimierung ist wichtig für das Marketing. Benchmarks gegen Branchendurchschnitte zeigen, wie gut die Flotte im Vergleich dasteht.

### Wartungsvorhersage

Basierend auf Kilometerstand und Zeit werden anstehende Wartungen angezeigt. Erinnerungen informieren rechtzeitig vor fälligen Terminen.

Fortgeschrittener ist die Vorhersage basierend auf Fahrverhalten: Wer viel Stadtverkehr fährt, braucht früher neue Bremsen. Ungewöhnlich hoher Verbrauch könnte auf ein Problem hindeuten und eine Warnung auslösen.

Mit OBD-II-Daten könnten Anomalien erkannt werden: ungewöhnliche Motortemperatur, häufige Fehlercodes.

### Auftragsmanagement

Lieferaufträge werden mit Abholadresse, Zieladresse, Zeitfenster und Größe/Gewicht erfasst. Das System kann Aufträge automatisch zu Touren zusammenfassen und Fahrzeugen zuordnen.

Der Status jedes Auftrags ist nachverfolgbar: offen, einem Fahrzeug zugeordnet, unterwegs, zugestellt. Kunden können benachrichtigt werden, wenn das Fahrzeug sich nähert. Die Lieferbestätigung kann mit Foto oder digitaler Unterschrift dokumentiert werden.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. PostgreSQL mit der PostGIS-Erweiterung speichert Geodaten effizient. Für die GPS-Historie kommt eine Zeitreihendatenbank (InfluxDB oder TimescaleDB) zum Einsatz. RabbitMQ verarbeitet die eingehenden GPS-Daten asynchron.

Das Frontend nutzt Vue.js 3 mit Leaflet für die Kartenvisualisierung, basierend auf OpenStreetMap. Für das Routing wird eine selbst gehostete OSRM-Instanz oder GraphHopper verwendet.

Die Optimierung nutzt eine spezialisierte Bibliothek wie Google OR-Tools oder OptaPlanner - das Rad muss hier nicht neu erfunden werden, aber die Algorithmen müssen verstanden und konfiguriert werden.

Eine Fahrer-App als PWA ermöglicht Navigation und Auftragsbestätigung.

---

## 5. Qualitätsanforderungen

Die Optimierung muss schnell sein: Eine Tour mit 20 Stopps muss in unter 5 Sekunden berechnet werden. Das System muss GPS-Daten von 50 Fahrzeugen verarbeiten, die alle 10 Sekunden senden. Das sind 300 Positionsupdates pro Minute.

Die GPS-Historie muss 90 Tage vorgehalten werden. Import von Aufträgen per CSV oder API ist erforderlich.

Die Integration externer Dienste ist essentiell: Kartenvisualisierung (OpenStreetMap), Routing-API (OSRM, GraphHopper oder Google), optional Wetter-API und Verkehrsdaten-API, optional Ladesäulen-Datenbank (OpenChargeMap).

---

## 6. Dokumentations- und Testanforderungen

Neben der V-Modell-Standarddokumentation ist ein Algorithmen-Vergleich Pflicht. Die Testdokumentation umfasst spezielle Tests für die Optimierungsalgorithmen und den GPS-Simulator.

Algorithmus-Tests prüfen verschiedene Szenarien: kleine Instanz (5 Stopps, 1 Fahrzeug) muss optimal gelöst werden. Mittlere Instanz (15 Stopps, 3 Fahrzeuge) muss nahe am Optimum liegen. Große Instanz (30 Stopps, 5 Fahrzeuge) muss in unter 5 Sekunden gelöst werden. Spezialfälle wie Elektrofahrzeuge mit Ladestopp-Constraints und enge Zeitfenster müssen korrekt behandelt werden.

Simulations-Tests validieren den GPS-Simulator: Bekannte Routen werden korrekt nachgefahren, Geschwindigkeiten sind realistisch, GPS-Drift wird simuliert, 50 Fahrzeuge laufen parallel.

Ein CO2-Validierungs-Report prüft die Plausibilität der Emissionsberechnungen.

---

## 7. Forschungskomponente: Algorithmen-Vergleich

Das Team muss mindestens zwei VRP-Algorithmen implementieren und vergleichen. Zur Auswahl stehen klassische Algorithmen (Nearest Neighbor als Baseline, Verbesserungsheuristiken wie 2-opt, Savings Algorithm nach Clarke-Wright), Metaheuristiken (Simulated Annealing, Genetic Algorithm, Tabu Search) oder die Nutzung von OR-Tools/OptaPlanner mit verschiedenen Konfigurationen.

Der Vergleich wird auf Benchmark-Datensätzen verschiedener Größe durchgeführt. Verglichen werden Laufzeit und Lösungsqualität. Ein Report von mindestens 8 Seiten dokumentiert die Ergebnisse mit Empfehlung für den Produktiveinsatz.

### GPS-Simulator

Da echte GPS-Tracker für 50 Fahrzeuge nicht praktikabel sind, muss das Team einen Simulator entwickeln. Dieser simuliert Fahrten entlang definierter Routen mit realistischen variablen Geschwindigkeiten und Stopps. Er muss mindestens 50 parallele Fahrzeuge simulieren können und steuerbar sein (Start, Stop, Pause, Geschwindigkeit).

### CO2-Berechnungsmodell

Das Team muss ein plausibles CO2-Berechnungsmodell entwickeln. Basiswerte definieren den CO2-Ausstoß pro Kilometer für verschiedene Fahrzeugtypen. Faktoren wie Geschwindigkeit (Autobahn vs. Stadt), Beladung und Steigungen beeinflussen den Verbrauch. Für Elektrofahrzeuge muss der Strommix berücksichtigt werden, um CO2-Äquivalente zu berechnen.

Die Validierung vergleicht die berechneten Werte mit offiziellen Daten (Herstellerangaben, Umweltbundesamt).

---

## 8. Gesellschaftliche Relevanz

Dieses Projekt adressiert ein Thema von gesellschaftlicher Bedeutung. Der Transportsektor ist für einen erheblichen Teil der CO2-Emissionen verantwortlich. Intelligente Routenplanung und der optimierte Einsatz von Elektrofahrzeugen können einen messbaren Beitrag zur Emissionsreduktion leisten.

---

Offenburg, den 13.01.2026

Thomas Grün
CSO EcoLogistics AG
