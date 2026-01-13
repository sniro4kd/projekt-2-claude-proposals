# Project Proposal: SmartCampus IoT Platform

---

| Eigenschaft | Wert |
|-------------|------|
| **Firma** | TechEdu Solutions GmbH |
| **Projekt** | SmartCampus |
| **Product Owner** | Dr. Maria Schneider |
| **Projektlaufzeit** | März - Juli 2026 |
| **Budget** | 35.000 Euro |
| **Version** | 1.0 |
| **Datum** | 13.01.2026 |
| **Zielgruppe** | 6-7 Studierende, 4.-6. Semester Angewandte Informatik |
| **Aufwand pro Person** | 30-40 Stunden (mit KI-Assistenten) |

---

## 1. Projektbeschreibung

### 1.1 Hintergrund

Die TechEdu Solutions GmbH entwickelt Softwarelösungen für Bildungseinrichtungen. Um die Digitalisierung an Hochschulen voranzutreiben, soll eine **IoT-Plattform für intelligentes Gebäudemanagement** entwickelt werden.

Das System soll Sensordaten aus Hörsälen erfassen (CO2, Temperatur, Luftfeuchtigkeit, Belegung), visualisieren und bei Grenzwertüberschreitungen automatisch Aktionen auslösen (Lüftung, Benachrichtigungen).

### 1.2 Projektziele

1. Entwicklung einer skalierbaren IoT-Datenplattform
2. Echtzeit-Dashboard für Facility Management
3. Automatisierte Benachrichtigungen und Aktoren-Steuerung
4. Mobile App für Studierende (Raumsuche, Auslastung)
5. Historische Datenanalyse und Vorhersagemodelle

---

## 2. Funktionale Anforderungen

### 2.1 Backend-System (Microservices)

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-101 | Das System MUSS Sensordaten via MQTT empfangen können | Muss |
| FA-102 | Das System MUSS Daten in einer Zeitreihendatenbank (InfluxDB/TimescaleDB) speichern | Muss |
| FA-103 | Das System MUSS eine REST-API für Frontend-Abfragen bereitstellen | Muss |
| FA-104 | Das System MUSS Grenzwerte konfigurierbar speichern können | Muss |
| FA-105 | Das System MUSS bei Grenzwertüberschreitung Events auslösen | Muss |
| FA-106 | Das System SOLL Daten aggregieren (Stunde, Tag, Woche, Monat) | Soll |
| FA-107 | Das System SOLL Vorhersagen zur Raumbelegung berechnen | Soll |
| FA-108 | Das System KANN externe Kalender-APIs integrieren (iCal, Exchange) | Kann |

### 2.2 Web-Dashboard

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-201 | Das Dashboard MUSS Echtzeit-Daten aller Sensoren anzeigen | Muss |
| FA-202 | Das Dashboard MUSS historische Daten als Diagramme darstellen | Muss |
| FA-203 | Das Dashboard MUSS Alarme visualisieren und quittierbar machen | Muss |
| FA-204 | Das Dashboard MUSS Grenzwerte konfigurierbar machen | Muss |
| FA-205 | Das Dashboard SOLL eine Gebäude-/Raumübersicht als Karte zeigen | Soll |
| FA-206 | Das Dashboard SOLL Export-Funktionen (CSV, PDF) bieten | Soll |
| FA-207 | Das Dashboard KANN Push-Benachrichtigungen im Browser unterstützen | Kann |

### 2.3 Mobile App

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-301 | Die App MUSS verfügbare Räume mit Auslastung anzeigen | Muss |
| FA-302 | Die App MUSS Raumdetails (Temperatur, CO2, Belegung) zeigen | Muss |
| FA-303 | Die App SOLL Räume als Favoriten speicherbar machen | Soll |
| FA-304 | Die App SOLL Benachrichtigungen bei freien Lieblingsräumen senden | Soll |
| FA-305 | Die App KANN Indoor-Navigation unterstützen | Kann |

### 2.4 Hardware-Integration (Simulator + Optional Real)

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-401 | Das System MUSS mit einem Sensor-Simulator getestet werden können | Muss |
| FA-402 | Der Simulator MUSS realistische Datenverläufe generieren | Muss |
| FA-403 | Das System SOLL mit echten ESP32/Arduino-Sensoren funktionieren | Soll |
| FA-404 | Das System KANN Aktoren (z.B. LED, Relay) ansteuern | Kann |

---

## 3. Nicht-funktionale Anforderungen

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-501 | Das System MUSS mindestens 100 Sensoren gleichzeitig verarbeiten | Muss |
| NFA-502 | Die Dashboard-Latenz MUSS unter 2 Sekunden liegen | Muss |
| NFA-503 | Das System MUSS 99% Verfügbarkeit erreichen (gemessen über Projektlaufzeit) | Muss |
| NFA-504 | Sensordaten MÜSSEN mindestens 90 Tage gespeichert werden | Muss |
| NFA-505 | Das System MUSS via Docker Compose deploybar sein | Muss |
| NFA-506 | Das System SOLL auf Kubernetes skalierbar sein | Soll |
| NFA-507 | Das System SOLL DSGVO-konform sein (Anonymisierung möglich) | Soll |
| NFA-508 | Die Mobile App SOLL auf iOS und Android laufen (Cross-Platform) | Soll |

---

## 4. Technische Vorgaben

### 4.1 Vorgegebener Tech-Stack

| Komponente | Technologie | Begründung |
|------------|-------------|------------|
| Backend | C# / ASP.NET Core 9 | Firmenstandard |
| Message Broker | RabbitMQ oder Mosquitto (MQTT) | IoT-Standard |
| Zeitreihendatenbank | InfluxDB oder TimescaleDB | Spezialisiert für Sensordaten |
| Relationale Daten | PostgreSQL | Konfiguration, User |
| Frontend Dashboard | Vue.js 3 / React 18 | Wahl des Teams |
| Mobile App | Flutter oder React Native | Cross-Platform |
| Container | Docker, Docker Compose | Pflicht |
| Optional | Kubernetes (K3s) | Bonuspunkte |

### 4.2 Architektur-Vorgaben

```
┌─────────────────────────────────────────────────────────────────┐
│                        Clients                                   │
├─────────────────┬─────────────────┬─────────────────────────────┤
│  Web Dashboard  │   Mobile App    │   External Systems          │
└────────┬────────┴────────┬────────┴──────────────┬──────────────┘
         │                 │                        │
         ▼                 ▼                        ▼
┌─────────────────────────────────────────────────────────────────┐
│                      API Gateway (NGINX/Traefik)                │
└─────────────────────────────┬───────────────────────────────────┘
                              │
         ┌────────────────────┼────────────────────┐
         │                    │                    │
         ▼                    ▼                    ▼
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│  Sensor Service │  │  Alert Service  │  │  Query Service  │
│  (MQTT → DB)    │  │  (Rules Engine) │  │  (REST API)     │
└────────┬────────┘  └────────┬────────┘  └────────┬────────┘
         │                    │                    │
         ▼                    ▼                    ▼
┌─────────────────────────────────────────────────────────────────┐
│                      Message Queue (RabbitMQ)                   │
└─────────────────────────────┬───────────────────────────────────┘
                              │
         ┌────────────────────┼────────────────────┐
         ▼                    ▼                    ▼
┌─────────────────┐  ┌─────────────────┐  ┌─────────────────┐
│   InfluxDB      │  │   PostgreSQL    │  │   Redis Cache   │
│   (Timeseries)  │  │   (Config/User) │  │   (Sessions)    │
└─────────────────┘  └─────────────────┘  └─────────────────┘
```

---

## 5. Pflichtdokumentation nach V-Modell

### 5.1 Erforderliche Dokumente

| Phase | Dokument | Beschreibung |
|-------|----------|--------------|
| Anforderungen | Lastenheft | Kundenanforderungen (dieses Proposal erweitert) |
| Spezifikation | Pflichtenheft | Technische Spezifikation aller Anforderungen |
| Entwurf | High-Level-Design | Architekturübersicht, Komponentendiagramme |
| Entwurf | Low-Level-Design | Klassendiagramme, Sequenzdiagramme, API-Specs |
| Entwurf | Datenbankdesign | Schema für alle Datenbanken |
| Projektmanagement | ADRs | Architecture Decision Records (mind. 5) |
| Projektmanagement | Projektprotokoll | Sprint-Protokolle, Retrospektiven |

### 5.2 Pflicht-Testdokumentation

| Dokument | Inhalt | Anforderung |
|----------|--------|-------------|
| **Mastertestplan** | Teststrategie, Testumgebungen, Verantwortlichkeiten, Zeitplan | Pflicht |
| **Komponententest-Spezifikation** | Testfälle für Unit-Tests aller Services | Mind. 50 Testfälle |
| **Integrationstest-Spezifikation** | Testfälle für Service-Kommunikation | Mind. 20 Testfälle |
| **Systemtest-Spezifikation** | End-to-End Testszenarien | Mind. 15 Testfälle |
| **Lasttest-Spezifikation** | Performance-Testfälle (100 Sensoren) | Mind. 5 Szenarien |
| **Komponententest-Report** | Ergebnisse der Unit-Tests | Mit Coverage-Analyse |
| **Integrationstest-Report** | Ergebnisse der Integrationstests | Alle Services |
| **Systemtest-Report** | Ergebnisse der E2E-Tests | Mit Screenshots |
| **Lasttest-Report** | Performance-Messergebnisse | Mit Grafiken |
| **Code-Coverage-Report** | Zeilenabdeckung pro Service | Ziel: >80% |
| **Anforderungsverifikation** | Traceability Matrix (Anforderung → Test) | 100% Abdeckung |

---

## 6. Spezielle Projektanforderungen

### 6.1 Research-Komponente (Pflicht)

Das Team MUSS eine der folgenden Research-Aufgaben durchführen und dokumentieren:

1. **Vorhersage-Algorithmus:** Vergleich von mindestens 3 Ansätzen zur Belegungsvorhersage (z.B. Linear Regression, ARIMA, Simple ML) mit statistischer Auswertung
2. **Anomalie-Erkennung:** Implementierung und Evaluation eines Algorithmus zur Erkennung ungewöhnlicher Sensormuster
3. **Energieoptimierung:** Simulation und Analyse von Energieeinsparungen durch intelligente Lüftungssteuerung

**Deliverable:** Research-Report (mind. 10 Seiten) mit Methodik, Ergebnissen, Diskussion

### 6.2 Prozess-Anforderungen (Pflicht)

| Anforderung | Beschreibung |
|-------------|--------------|
| Code-Reviews | Jeder Pull Request benötigt mindestens 1 Approval |
| Sprint-Länge | 2-Wochen-Sprints mit Review und Retrospektive |
| Daily Standups | Mind. 3x pro Woche (asynchron oder synchron) |
| Definition of Done | Vom Team definiert und dokumentiert |
| KI-Dokumentation | Alle wesentlichen KI-Interaktionen werden protokolliert |

### 6.3 Hardware-Komponente (Optional für Bonus)

Teams können für Bonuspunkte echte Hardware integrieren:
- ESP32 mit BME280 (Temperatur, Luftfeuchtigkeit)
- MH-Z19 (CO2-Sensor)
- PIR-Sensor (Bewegungserkennung)

Hardware wird bei Bedarf gestellt.

---

## 7. Abnahmekriterien

### 7.1 Muss-Kriterien für Projektabnahme

1. [ ] Alle Muss-Anforderungen erfüllt und getestet
2. [ ] Vollständige V-Modell-Dokumentation vorhanden
3. [ ] Alle Testdokumente und Reports vorhanden
4. [ ] Code-Coverage Backend >80%
5. [ ] System läuft stabil unter Last (100 simulierte Sensoren)
6. [ ] Docker-Compose Deployment funktioniert
7. [ ] Research-Report liegt vor
8. [ ] Jedes Teammitglied kann Code erklären (mündliche Prüfung)

### 7.2 Bewertungsschema

| Kategorie | Gewicht | Kriterien |
|-----------|---------|-----------|
| Funktionalität | 25% | Erfüllung aller Muss-/Soll-Anforderungen |
| Architektur & Design | 20% | ADRs, Skalierbarkeit, Clean Architecture |
| Testqualität | 20% | Coverage, Testdokumentation, Teststrategie |
| Research-Komponente | 15% | Methodik, Ergebnisse, Dokumentation |
| Prozessqualität | 10% | Reviews, Retrospektiven, Teamarbeit |
| KI-Reflexion | 10% | Dokumentation und Reflexion des KI-Einsatzes |

---

## 8. Warum dieses Projekt für KI-Zeitalter geeignet ist

| Aspekt | Begründung |
|--------|------------|
| **Microservices** | Mehr Architekturentscheidungen als Monolith |
| **IoT-Integration** | Echte Hardware-Simulation, nicht trivial |
| **Mehrere Datenbanken** | Zeitreihen + Relational + Cache |
| **Research-Pflicht** | Eigene Algorithmen, nicht nur API-Nutzung |
| **Umfangreiche Tests** | 5 Test-Ebenen mit Dokumentation |
| **Cross-Platform** | Web + Mobile erhöht Komplexität |
| **Prozess-Fokus** | Reviews und Retrospektiven als Pflicht |

---

## Projekt genehmigt

Offenburg, den 13.01.2026

_____Dr. Thomas Weber_____

TechEdu Solutions GmbH
Dr. Thomas Weber
CTO TechEdu Solutions GmbH
