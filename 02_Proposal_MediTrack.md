# Project Proposal: MediTrack - Medikamenten-Management-System

---

| Eigenschaft | Wert |
|-------------|------|
| **Firma** | HealthSoft AG |
| **Projekt** | MediTrack |
| **Product Owner** | Dr. Anna Bergmann |
| **Projektlaufzeit** | März - Juli 2026 |
| **Budget** | 40.000 Euro |
| **Version** | 1.0 |
| **Datum** | 13.01.2026 |
| **Zielgruppe** | 6-7 Studierende, 4.-6. Semester Angewandte Informatik |
| **Aufwand pro Person** | 30-40 Stunden (mit KI-Assistenten) |

---

## 1. Projektbeschreibung

### 1.1 Hintergrund

Die HealthSoft AG entwickelt Software für Pflegeeinrichtungen. Ein häufiges Problem in Seniorenheimen ist die fehlerhafte oder vergessene Medikamentengabe. Jährlich entstehen dadurch erhebliche Gesundheitsrisiken und Kosten.

Es soll ein **Medikamenten-Management-System** entwickelt werden, das:
- Medikamentenpläne digital verwaltet
- Pflegekräfte an Gaben erinnert
- Die Ausgabe per Barcode/QR-Code dokumentiert
- Wechselwirkungen automatisch prüft
- Lagerbestände überwacht

### 1.2 Besondere Herausforderung: Datenschutz

Da es sich um **Gesundheitsdaten** handelt (Art. 9 DSGVO - besondere Kategorien personenbezogener Daten), gelten erhöhte Anforderungen an:
- Verschlüsselung (at rest und in transit)
- Zugriffsprotokollierung (Audit-Log)
- Rollenbasierte Zugriffskontrolle
- Anonymisierung für Statistiken

---

## 2. Funktionale Anforderungen

### 2.1 Bewohner- und Medikamentenverwaltung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-101 | Das System MUSS Bewohnerdaten (Name, Geburtsdatum, Zimmer, Allergien) verwalten | Muss |
| FA-102 | Das System MUSS Medikamente mit Wirkstoff, Dosierung, PZN verwalten | Muss |
| FA-103 | Das System MUSS individuelle Medikamentenpläne pro Bewohner ermöglichen | Muss |
| FA-104 | Das System MUSS Zeitpunkte für Gaben definierbar machen (morgens, mittags, abends, nachts, nach Bedarf) | Muss |
| FA-105 | Das System MUSS Änderungen am Medikamentenplan historisieren | Muss |
| FA-106 | Das System SOLL Medikamente aus einer externen Datenbank importieren können (z.B. vereinfachte PZN-Datenbank) | Soll |
| FA-107 | Das System SOLL Arztverordnungen als PDF hochladbar machen | Soll |

### 2.2 Medikamentengabe und Dokumentation

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-201 | Das System MUSS eine Übersicht aller fälligen Gaben zum aktuellen Zeitpunkt zeigen | Muss |
| FA-202 | Das System MUSS die Gabe per Barcode-/QR-Code-Scan dokumentierbar machen | Muss |
| FA-203 | Das System MUSS Gabe, Verweigerung und Nichtgabe unterscheiden können | Muss |
| FA-204 | Das System MUSS bei jeder Dokumentation Pflegekraft, Zeitstempel, Kommentar erfassen | Muss |
| FA-205 | Das System MUSS überfällige Gaben optisch hervorheben | Muss |
| FA-206 | Das System SOLL Push-Benachrichtigungen an Pflegekräfte senden | Soll |
| FA-207 | Das System SOLL eine Unterschriften-Funktion (Touch) für die Gabe bieten | Soll |

### 2.3 Wechselwirkungsprüfung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-301 | Das System MUSS bei neuen Medikamenten auf bekannte Wechselwirkungen prüfen | Muss |
| FA-302 | Das System MUSS Wechselwirkungen nach Schweregrad klassifizieren (leicht, mittel, schwer) | Muss |
| FA-303 | Das System MUSS schwere Wechselwirkungen blockieren (mit Override durch Arzt) | Muss |
| FA-304 | Das System MUSS die Wechselwirkungsdatenbank wartbar machen | Muss |
| FA-305 | Das System SOLL Allergien bei Wechselwirkungsprüfung berücksichtigen | Soll |

### 2.4 Lagerverwaltung und Bestellung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-401 | Das System MUSS Lagerbestände pro Medikament führen | Muss |
| FA-402 | Das System MUSS bei Gabe den Bestand automatisch reduzieren | Muss |
| FA-403 | Das System MUSS bei Unterschreitung des Mindestbestands warnen | Muss |
| FA-404 | Das System SOLL Verfallsdaten tracken und warnen | Soll |
| FA-405 | Das System SOLL Bestellvorschläge generieren | Soll |
| FA-406 | Das System KANN Bestellungen an Apotheken-Schnittstelle übermitteln | Kann |

### 2.5 Reporting und Audit

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-501 | Das System MUSS einen vollständigen Audit-Log führen (wer, wann, was) | Muss |
| FA-502 | Das System MUSS Berichte pro Bewohner exportierbar machen (PDF) | Muss |
| FA-503 | Das System MUSS Statistiken zur Gabe-Compliance berechnen | Muss |
| FA-504 | Das System SOLL anonymisierte Auswertungen über alle Bewohner ermöglichen | Soll |
| FA-505 | Das System SOLL MDK-konforme Dokumentation exportieren | Soll |

### 2.6 Benutzerverwaltung und Sicherheit

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-601 | Das System MUSS verschiedene Rollen unterstützen (Admin, Arzt, Pflegekraft, Leitung) | Muss |
| FA-602 | Das System MUSS Zwei-Faktor-Authentifizierung unterstützen | Muss |
| FA-603 | Das System MUSS automatische Session-Timeouts haben | Muss |
| FA-604 | Das System MUSS fehlgeschlagene Logins protokollieren und nach 5 Versuchen sperren | Muss |
| FA-605 | Das System SOLL Single-Sign-On (LDAP/AD) unterstützen | Soll |

---

## 3. Nicht-funktionale Anforderungen

### 3.1 Security-Anforderungen (KRITISCH)

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-701 | Alle Daten MÜSSEN verschlüsselt gespeichert werden (AES-256) | Muss |
| NFA-702 | Alle API-Kommunikation MUSS über HTTPS erfolgen | Muss |
| NFA-703 | Passwörter MÜSSEN mit bcrypt/Argon2 gehasht werden | Muss |
| NFA-704 | Das System MUSS gegen OWASP Top 10 geschützt sein | Muss |
| NFA-705 | Ein Security-Audit MUSS durchgeführt werden (durch anderes Team/Dozent) | Muss |
| NFA-706 | Das System SOLL Penetrationstests bestehen | Soll |

### 3.2 Performance und Verfügbarkeit

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-801 | Das System MUSS 50 gleichzeitige Benutzer unterstützen | Muss |
| NFA-802 | Seitenaufbau MUSS unter 2 Sekunden erfolgen | Muss |
| NFA-803 | Das System MUSS offline-fähig sein (PWA mit Sync) | Muss |
| NFA-804 | Das System MUSS tägliche automatische Backups haben | Muss |

### 3.3 Deployment und Betrieb

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-901 | Das System MUSS via Docker Compose deploybar sein | Muss |
| NFA-902 | Das System MUSS automatische Datenbankmigrationen unterstützen | Muss |
| NFA-903 | Das System SOLL Health-Checks für Monitoring bieten | Soll |
| NFA-904 | Das System SOLL strukturierte Logs (JSON) für Log-Aggregation ausgeben | Soll |

---

## 4. Technische Vorgaben

### 4.1 Tech-Stack

| Komponente | Technologie | Begründung |
|------------|-------------|------------|
| Backend | C# / ASP.NET Core 9 | Firmenstandard, HIPAA-erprobt |
| Datenbank | PostgreSQL | Open Source, verschlüsselungsfähig |
| Frontend | Vue.js 3 mit TypeScript | PWA-fähig |
| Mobile | PWA (Progressive Web App) | Offline-Support, kein App-Store |
| Auth | ASP.NET Identity + TOTP | 2FA-Support |
| PDF-Export | QuestPDF oder iText7 | Berichterstellung |
| Container | Docker, Docker Compose | Deployment |
| Barcode | ZXing.NET / QuaggaJS | Barcode-Scanning |

### 4.2 Architektur-Vorgaben

```
┌─────────────────────────────────────────────────────────────────┐
│                        PWA Frontend (Vue.js)                     │
│  ┌───────────┐  ┌───────────┐  ┌───────────┐  ┌───────────┐    │
│  │ Dashboard │  │  Gabe-UI  │  │  Lager    │  │  Reports  │    │
│  └───────────┘  └───────────┘  └───────────┘  └───────────┘    │
│                              │                                   │
│                    Service Worker (Offline)                      │
└──────────────────────────────┬──────────────────────────────────┘
                               │ HTTPS + JWT
                               ▼
┌─────────────────────────────────────────────────────────────────┐
│                    ASP.NET Core API                              │
├─────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐ ┌─────────────┐ ┌─────────────┐ ┌───────────┐ │
│  │ Auth        │ │ Medication  │ │ Inventory   │ │ Reporting │ │
│  │ Controller  │ │ Controller  │ │ Controller  │ │ Controller│ │
│  └──────┬──────┘ └──────┬──────┘ └──────┬──────┘ └─────┬─────┘ │
│         │               │               │               │       │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │                    Business Services                        ││
│  │  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐      ││
│  │  │ Interaction  │  │ Notification │  │ Audit        │      ││
│  │  │ Checker      │  │ Service      │  │ Service      │      ││
│  │  └──────────────┘  └──────────────┘  └──────────────┘      ││
│  └─────────────────────────────────────────────────────────────┘│
│         │               │               │               │       │
│  ┌─────────────────────────────────────────────────────────────┐│
│  │                    Data Access Layer                        ││
│  │         (Entity Framework Core + Encryption)                ││
│  └─────────────────────────────────────────────────────────────┘│
└──────────────────────────────┬──────────────────────────────────┘
                               │
                               ▼
┌─────────────────────────────────────────────────────────────────┐
│              PostgreSQL (encrypted at rest)                      │
│  ┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐           │
│  │Bewohner  │ │Medikament│ │Gaben     │ │Audit_Log │           │
│  └──────────┘ └──────────┘ └──────────┘ └──────────┘           │
└─────────────────────────────────────────────────────────────────┘
```

---

## 5. Pflichtdokumentation nach V-Modell

### 5.1 Erforderliche Dokumente

| Phase | Dokument | Besonderheit |
|-------|----------|--------------|
| Anforderungen | Lastenheft | Mit Datenschutz-Kapitel |
| Spezifikation | Pflichtenheft | Security-Anforderungen detailliert |
| Entwurf | High-Level-Design | Verschlüsselungsarchitektur |
| Entwurf | Low-Level-Design | Audit-Log Design |
| Entwurf | Datenmodell | Mit Verschlüsselungsfeldern |
| Projektmanagement | Datenschutz-Folgenabschätzung (DSFA) | **PFLICHT** |
| Projektmanagement | Security-Konzept | **PFLICHT** |
| Projektmanagement | ADRs | Mind. 5, davon 2 zu Security |

### 5.2 Pflicht-Testdokumentation

| Dokument | Inhalt | Spezielle Anforderungen |
|----------|--------|-------------------------|
| **Mastertestplan** | Teststrategie inkl. Security-Tests | Security-Testansatz beschreiben |
| **Komponententest-Spezifikation** | Unit-Tests für alle Services | Mind. 60 Testfälle |
| **Integrationstest-Spezifikation** | API-Tests, DB-Tests | Mind. 25 Testfälle |
| **Systemtest-Spezifikation** | E2E-Tests für kritische Workflows | Mind. 15 Szenarien |
| **Security-Test-Spezifikation** | OWASP-basierte Testfälle | **PFLICHT** - Mind. 20 Testfälle |
| **Komponententest-Report** | Ergebnisse der Unit-Tests | Coverage >80% |
| **Integrationstest-Report** | API-Test-Ergebnisse | Mit Response-Validierung |
| **Systemtest-Report** | E2E-Test-Ergebnisse | Screenshots aller Workflows |
| **Security-Test-Report** | Ergebnisse der Security-Tests | **PFLICHT** - Alle Findings dokumentiert |
| **Penetrationstest-Report** | Externer oder Cross-Team Test | Mind. Basis-Pentest |
| **Code-Coverage-Report** | Detaillierte Coverage-Analyse | Pro Komponente |
| **Anforderungsverifikation** | Traceability Matrix | 100% Muss-Anforderungen |

### 5.3 Besondere Testanforderungen

**Security-Tests (Pflicht):**

| Test-Kategorie | Beschreibung | Tool-Vorschlag |
|----------------|--------------|----------------|
| SQL Injection | Alle Eingabefelder testen | SQLMap, manuelle Tests |
| XSS | Alle Ausgaben testen | OWASP ZAP |
| Authentication | Brute-Force, Session-Hijacking | Manuelle Tests |
| Authorization | Privilege Escalation | Manuelle Tests |
| CSRF | Token-Validierung | OWASP ZAP |
| Sensitive Data | Verschlüsselung prüfen | Manuelle Prüfung |

---

## 6. Spezielle Projektanforderungen

### 6.1 Datenschutz-Komponente (Pflicht)

Das Team MUSS eine **Datenschutz-Folgenabschätzung (DSFA)** nach Art. 35 DSGVO erstellen:

1. **Systematische Beschreibung** der Verarbeitungsvorgänge
2. **Bewertung der Notwendigkeit** und Verhältnismäßigkeit
3. **Bewertung der Risiken** für die Rechte der Betroffenen
4. **Maßnahmen** zur Bewältigung der Risiken

**Deliverable:** DSFA-Dokument (mind. 8 Seiten)

### 6.2 Wechselwirkungsdatenbank (Research-Komponente)

Das Team MUSS eine einfache Wechselwirkungsdatenbank aufbauen:

1. **Recherche:** Öffentlich verfügbare Wechselwirkungsdaten sammeln
2. **Datenmodell:** Geeignetes Schema für Wechselwirkungen entwerfen
3. **Algorithmus:** Prüflogik mit Schweregrad-Klassifikation implementieren
4. **Evaluation:** Testfälle mit bekannten Wechselwirkungen

**Hinweis:** Es geht um das Prinzip, nicht um medizinische Vollständigkeit (20-30 exemplarische Wechselwirkungen reichen)

### 6.3 Prozess-Anforderungen

| Anforderung | Beschreibung |
|-------------|--------------|
| Code-Reviews | Jeder PR benötigt 2 Approvals (wegen Security) |
| Security-Review | Dedizierte Security-Reviews für alle Auth-Komponenten |
| Sprint-Reviews | Alle 2 Wochen mit Stakeholder-Feedback |
| Threat Modeling | Einmalig zu Projektbeginn durchführen |
| KI-Nutzung | KI-Code muss auf Security geprüft werden |

---

## 7. Abnahmekriterien

### 7.1 Muss-Kriterien für Projektabnahme

1. [ ] Alle Muss-Anforderungen erfüllt
2. [ ] Security-Test-Report ohne kritische Findings
3. [ ] DSFA liegt vor und ist vollständig
4. [ ] Audit-Log funktioniert und ist vollständig
5. [ ] Offline-Modus funktioniert (PWA)
6. [ ] Alle Testdokumente und Reports vorhanden
7. [ ] Code-Coverage >80%
8. [ ] Externes/Cross-Team Security-Review durchgeführt
9. [ ] Docker-Deployment funktioniert

### 7.2 Bewertungsschema

| Kategorie | Gewicht | Kriterien |
|-----------|---------|-----------|
| Funktionalität | 20% | Erfüllung der Muss-/Soll-Anforderungen |
| Security | 25% | DSFA, Security-Tests, Verschlüsselung, Audit |
| Architektur & Design | 15% | ADRs, Clean Architecture, Offline-Konzept |
| Testqualität | 20% | Coverage, alle Testdokumente, Security-Tests |
| Prozessqualität | 10% | Reviews, Threat Modeling, Dokumentation |
| KI-Reflexion | 10% | Besonders: Security-Aspekte bei KI-Code |

---

## 8. Warum dieses Projekt für KI-Zeitalter geeignet ist

| Aspekt | Begründung |
|--------|------------|
| **Security-Fokus** | KI-Code muss kritisch auf Sicherheit geprüft werden |
| **Datenschutz (DSGVO)** | Rechtliche Komponente, nicht automatisierbar |
| **Offline-PWA** | Komplexere Architektur als reine Web-App |
| **Wechselwirkungen** | Research und Datenaufbereitung nötig |
| **Audit-Anforderungen** | Durchgängige Nachvollziehbarkeit |
| **Security-Tests** | Manuelle Prüfung und Expertise erforderlich |
| **Cross-Team-Review** | Soziale/organisatorische Komponente |

---

## Projekt genehmigt

Offenburg, den 13.01.2026

_____Prof. Dr. Sabine Maier_____

HealthSoft AG
Prof. Dr. Sabine Maier
CISO HealthSoft AG
