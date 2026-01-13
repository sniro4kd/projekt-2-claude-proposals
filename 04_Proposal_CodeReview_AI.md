# Project Proposal: CodeGuardian - KI-gestütztes Code-Review-System

---

| Eigenschaft | Wert |
|-------------|------|
| **Firma** | DevQuality Labs GmbH |
| **Projekt** | CodeGuardian |
| **Product Owner** | Dr. Stefan Meier |
| **Projektlaufzeit** | März - Juli 2026 |
| **Budget** | 35.000 Euro |
| **Version** | 1.0 |
| **Datum** | 13.01.2026 |
| **Zielgruppe** | 6-7 Studierende, 4.-6. Semester Angewandte Informatik |
| **Aufwand pro Person** | 30-40 Stunden (mit KI-Assistenten) |

---

## 1. Projektbeschreibung

### 1.1 Hintergrund

Die DevQuality Labs GmbH bietet Qualitätssicherungs-Tools für Softwareunternehmen an. Ein wachsender Markt sind **KI-gestützte Code-Review-Systeme**, die Code automatisch auf Best Practices, Security-Issues und Code Smells prüfen.

Es soll ein System entwickelt werden, das:
- Git-Repositories analysiert
- Pull Requests automatisch reviewed
- Findings mit LLM-generierten Erklärungen und Fixes anreichert
- Ein Dashboard für Team-Metriken bietet

### 1.2 Besondere Herausforderung: LLM-Integration und Evaluation

Dieses Projekt verbindet klassische Softwareentwicklung mit **KI-Integration**:
- Nutzung von LLM-APIs (Claude, GPT) für natürlichsprachige Erklärungen
- Eigene Heuristiken für statische Code-Analyse
- **Evaluation und Benchmarking** der KI-Qualität
- Meta-Reflexion: KI bewertet Code, der teils mit KI erstellt wurde

---

## 2. Funktionale Anforderungen

### 2.1 Repository-Integration

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-101 | Das System MUSS GitHub Repositories anbinden können (OAuth) | Muss |
| FA-102 | Das System MUSS Push-Events via Webhook empfangen können | Muss |
| FA-103 | Das System MUSS Pull Requests analysieren können | Muss |
| FA-104 | Das System MUSS Analyse-Ergebnisse als PR-Kommentare posten | Muss |
| FA-105 | Das System SOLL GitLab unterstützen | Soll |
| FA-106 | Das System KANN Bitbucket unterstützen | Kann |
| FA-107 | Das System SOLL lokale Git-Repos per CLI analysieren können | Soll |

### 2.2 Statische Code-Analyse

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-201 | Das System MUSS C#-Code analysieren können | Muss |
| FA-202 | Das System MUSS TypeScript/JavaScript analysieren können | Muss |
| FA-203 | Das System MUSS Python analysieren können | Muss |
| FA-204 | Das System MUSS Code Smells erkennen (lange Methoden, hohe Komplexität) | Muss |
| FA-205 | Das System MUSS Security-Issues erkennen (SQL Injection, XSS-Pattern) | Muss |
| FA-206 | Das System MUSS Style-Violations erkennen (basierend auf konfigurbaren Regeln) | Muss |
| FA-207 | Das System SOLL Custom-Regeln per YAML definierbar machen | Soll |
| FA-208 | Das System SOLL existierende Linter integrieren (ESLint, Roslyn, Pylint) | Soll |

### 2.3 LLM-Integration

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-301 | Das System MUSS Findings mit LLM-generierten Erklärungen anreichern | Muss |
| FA-302 | Das System MUSS LLM-generierte Fix-Vorschläge bieten | Muss |
| FA-303 | Das System MUSS verschiedene LLM-Provider unterstützen (Claude, GPT) | Muss |
| FA-304 | Das System MUSS Rate-Limiting für LLM-Calls implementieren | Muss |
| FA-305 | Das System MUSS LLM-Responses cachen (gleicher Code → gleiche Erklärung) | Muss |
| FA-306 | Das System SOLL Confidence-Scores für LLM-Suggestions zeigen | Soll |
| FA-307 | Das System SOLL Prompt-Templates konfigurierbar machen | Soll |
| FA-308 | Das System KANN lokale LLMs (Ollama) als Fallback unterstützen | Kann |

### 2.4 Review-Dashboard

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-401 | Das System MUSS eine Übersicht aller analysierten PRs zeigen | Muss |
| FA-402 | Das System MUSS Findings nach Severity filtern können | Muss |
| FA-403 | Das System MUSS Findings als "accepted" oder "dismissed" markierbar machen | Muss |
| FA-404 | Das System MUSS Code-Diff mit inline Findings anzeigen | Muss |
| FA-405 | Das System SOLL Trends über Zeit visualisieren (Issue-Entwicklung) | Soll |
| FA-406 | Das System SOLL Team-Metriken zeigen (Issues pro Entwickler, Fix-Rate) | Soll |
| FA-407 | Das System SOLL Export-Funktion für Reports bieten | Soll |

### 2.5 Feedback-Loop und Verbesserung

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| FA-501 | Das System MUSS User-Feedback zu Findings erfassen ("helpful", "not helpful") | Muss |
| FA-502 | Das System MUSS Feedback-Statistiken auswerten | Muss |
| FA-503 | Das System SOLL häufig dismisste Regeln vorschlagen zu deaktivieren | Soll |
| FA-504 | Das System KANN Feedback für Prompt-Optimierung nutzen | Kann |

---

## 3. Nicht-funktionale Anforderungen

### 3.1 Performance

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-601 | Analyse eines PRs (< 500 LOC) MUSS unter 30 Sekunden dauern | Muss |
| NFA-602 | LLM-Enrichment SOLL unter 10 Sekunden pro Finding dauern | Soll |
| NFA-603 | Das System MUSS 50 gleichzeitige Analysen verarbeiten können | Muss |
| NFA-604 | Das System MUSS Analyse-Jobs in einer Queue verarbeiten | Muss |

### 3.2 Skalierbarkeit und Kosten

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-701 | Das System MUSS LLM-API-Kosten pro Analyse tracken | Muss |
| NFA-702 | Das System MUSS ein Budget-Limit pro Tag/Monat haben | Muss |
| NFA-703 | Das System MUSS bei Budget-Erreichen auf Basis-Analyse (ohne LLM) fallen | Muss |
| NFA-704 | Das System SOLL Caching nutzen um API-Kosten zu reduzieren | Soll |

### 3.3 Security

| ID | Anforderung | Priorität |
|----|-------------|-----------|
| NFA-801 | Das System MUSS OAuth-Tokens sicher speichern (encrypted) | Muss |
| NFA-802 | Das System MUSS API-Keys für LLM-Provider sicher verwalten | Muss |
| NFA-803 | Das System DARF keinen sensiblen Code an LLM senden (Konfiguration) | Muss |
| NFA-804 | Das System MUSS Webhook-Signatures validieren | Muss |

---

## 4. Technische Vorgaben

### 4.1 Tech-Stack

| Komponente | Technologie | Begründung |
|------------|-------------|------------|
| Backend | C# / ASP.NET Core 9 | Firmenstandard |
| Job Queue | Hangfire oder RabbitMQ | Background Processing |
| Datenbank | PostgreSQL | Findings, Metrics |
| Cache | Redis | LLM Response Cache |
| Frontend | Vue.js 3 | Dashboard |
| Git-Integration | LibGit2Sharp + GitHub API | Repository-Zugriff |
| LLM | Anthropic Claude API + OpenAI API | Multi-Provider |
| Static Analysis | Roslyn (C#), ESLint, Pylint | Code-Analyse |
| Container | Docker, Docker Compose | Deployment |

### 4.2 Architektur

```
┌─────────────────────────────────────────────────────────────────────────┐
│                            GitHub/GitLab                                 │
│                                │                                         │
│                         Webhook (Push/PR)                                │
└────────────────────────────────┼────────────────────────────────────────┘
                                 │
                                 ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                          API Gateway                                     │
└────────────────────────────────┼────────────────────────────────────────┘
                                 │
         ┌───────────────────────┼───────────────────────┐
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Webhook        │    │  Dashboard      │    │  API            │
│  Controller     │    │  Controller     │    │  Controller     │
└────────┬────────┘    └────────┬────────┘    └────────┬────────┘
         │                      │                      │
         │                      ▼                      │
         │             ┌─────────────────┐             │
         │             │   PostgreSQL    │◄────────────┘
         │             │   (Findings,    │
         │             │    Metrics)     │
         │             └─────────────────┘
         │
         ▼
┌─────────────────────────────────────────────────────────────────────────┐
│                         Job Queue (Hangfire/RabbitMQ)                    │
└────────────────────────────────┼────────────────────────────────────────┘
                                 │
         ┌───────────────────────┼───────────────────────┐
         │                       │                       │
         ▼                       ▼                       ▼
┌─────────────────┐    ┌─────────────────┐    ┌─────────────────┐
│  Clone/Fetch    │    │  Static         │    │  LLM            │
│  Worker         │    │  Analysis       │    │  Enrichment     │
│                 │    │  Worker         │    │  Worker         │
└─────────────────┘    └─────────────────┘    └────────┬────────┘
                                                       │
                                                       ▼
                                              ┌─────────────────┐
                                              │  Redis Cache    │
                                              │  + LLM APIs     │
                                              │  (Claude, GPT)  │
                                              └─────────────────┘
```

---

## 5. Pflichtdokumentation nach V-Modell

### 5.1 Erforderliche Dokumente

| Phase | Dokument | Besonderheit |
|-------|----------|--------------|
| Anforderungen | Lastenheft | Rule-Katalog definieren |
| Spezifikation | Pflichtenheft | LLM-Prompts spezifizieren |
| Entwurf | High-Level-Design | Worker-Architektur |
| Entwurf | Low-Level-Design | Regel-Engine Design |
| Entwurf | Prompt Engineering Dokumentation | **PFLICHT** |
| Projektmanagement | ADRs | Mind. 5, davon 2 zu LLM-Integration |
| Projektmanagement | LLM-Kosten-Analyse | **PFLICHT** |

### 5.2 Pflicht-Testdokumentation

| Dokument | Inhalt | Spezielle Anforderungen |
|----------|--------|-------------------------|
| **Mastertestplan** | Teststrategie inkl. LLM-Tests | LLM-Teststrategie beschreiben |
| **Komponententest-Spezifikation** | Unit-Tests für Analyzer | Mind. 50 Testfälle |
| **Integrationstest-Spezifikation** | GitHub-API, LLM-API Tests | Mind. 20 Testfälle |
| **Golden-Test-Spezifikation** | Erwartete Findings für Beispielcode | **PFLICHT** - Mind. 30 Snippets |
| **LLM-Evaluation-Spezifikation** | Qualitätskriterien für LLM-Output | **PFLICHT** - Rubrik definieren |
| **Systemtest-Spezifikation** | E2E PR-Analyse Szenarien | Mind. 10 Szenarien |
| **Komponententest-Report** | Ergebnisse Unit-Tests | Coverage >80% |
| **Integrationstest-Report** | API-Integrations-Ergebnisse | Mock vs. Real API |
| **Golden-Test-Report** | Analyzer-Genauigkeit | Precision/Recall Metriken |
| **LLM-Evaluation-Report** | Qualität der LLM-Outputs | **PFLICHT** - Mit Beispielen |
| **Systemtest-Report** | E2E-Ergebnisse | Screenshots |
| **Anforderungsverifikation** | Traceability Matrix | 100% Muss-Anforderungen |
| **Kosten-Report** | LLM-API-Kosten während Tests | Pro Provider |

### 5.3 Besondere Testanforderungen

**Golden Tests (Pflicht):**

Das Team MUSS eine **Test-Suite mit bekannten Code-Snippets** erstellen:

| Sprache | Snippet-Typ | Erwartete Findings |
|---------|-------------|-------------------|
| C# | SQL Injection | Security: SQL Injection |
| C# | God Class | Smell: Too Many Methods |
| C# | Long Method | Smell: Method Too Long |
| TypeScript | XSS Pattern | Security: XSS Risk |
| TypeScript | Callback Hell | Smell: Deep Nesting |
| Python | Hardcoded Password | Security: Credentials |
| Python | Bare Except | Style: Bare Except |

**LLM-Evaluation (Pflicht):**

| Kriterium | Beschreibung | Messung |
|-----------|--------------|---------|
| Accuracy | Ist die Erklärung fachlich korrekt? | Human Review (Sample) |
| Helpfulness | Hilft der Fix-Vorschlag? | User Feedback |
| Consistency | Gleiche Erklärung für gleichen Code? | Automatisch |
| Safety | Keine falschen Security-Entwarnung? | Golden Tests |

---

## 6. Spezielle Projektanforderungen

### 6.1 Prompt Engineering (Research-Komponente)

Das Team MUSS systematisches **Prompt Engineering** durchführen und dokumentieren:

1. **Baseline Prompts:** Initiale Prompts für jede Aufgabe (Erklärung, Fix)
2. **Iterative Verbesserung:** Mind. 3 Iterationen pro Prompt-Typ
3. **A/B-Testing:** Vergleich verschiedener Prompt-Varianten
4. **Evaluation:** Qualitätsmessung nach definierter Rubrik

**Deliverables:**
- Prompt Engineering Dokumentation (mind. 10 Seiten)
- Finale Prompts mit Begründung
- Evaluationsergebnisse

### 6.2 LLM-Kosten-Analyse (Pflicht)

Das Team MUSS eine **Kosten-Nutzen-Analyse** für LLM-Einsatz erstellen:

1. **Kosten-Tracking:** Tokens und Kosten pro Analyse
2. **Provider-Vergleich:** Claude vs. GPT (Qualität, Kosten, Latenz)
3. **Caching-Effektivität:** Wie viel spart Caching?
4. **Break-Even:** Ab wann lohnt sich lokales LLM?

**Deliverable:** Kosten-Analyse-Report (mind. 5 Seiten)

### 6.3 Meta-Reflexion: KI analysiert KI-Code

Das Team SOLL dokumentieren:
- Wie gut erkennt das System Issues in KI-generiertem Code?
- Welche typischen Probleme erzeugt KI-Code?
- Wie kann man KI-Code besser reviewen?

**Deliverable:** Reflexionsbericht (2-3 Seiten)

### 6.4 Prozess-Anforderungen

| Anforderung | Beschreibung |
|-------------|--------------|
| Code-Reviews | Jeder PR benötigt 1 Approval |
| Prompt-Reviews | Neue Prompts benötigen Team-Review |
| LLM-Budget | Max. 50€ pro Woche für API-Calls |
| Sprint-Reviews | Alle 2 Wochen mit Demo |

---

## 7. Abnahmekriterien

### 7.1 Muss-Kriterien für Projektabnahme

1. [ ] Alle Muss-Anforderungen erfüllt
2. [ ] GitHub-Integration funktioniert (PR-Kommentare)
3. [ ] Mindestens 20 Analyse-Regeln implementiert
4. [ ] LLM-Enrichment funktioniert mit 2 Providern
5. [ ] Golden Tests: Precision >80%, Recall >70%
6. [ ] Prompt Engineering Dokumentation liegt vor
7. [ ] Kosten-Analyse durchgeführt
8. [ ] Alle Testdokumente und Reports vorhanden
9. [ ] Code-Coverage >80%
10. [ ] Docker-Deployment funktioniert

### 7.2 Bewertungsschema

| Kategorie | Gewicht | Kriterien |
|-----------|---------|-----------|
| Funktionalität | 20% | Erfüllung der Anforderungen |
| Analyse-Qualität | 20% | Precision/Recall der Regeln |
| LLM-Integration | 20% | Prompt Engineering, Evaluation |
| Testqualität | 15% | Coverage, Golden Tests |
| Research & Doku | 15% | Kosten-Analyse, Meta-Reflexion |
| Prozessqualität | 10% | Reviews, Budget-Management |

---

## 8. Warum dieses Projekt für KI-Zeitalter geeignet ist

| Aspekt | Begründung |
|--------|------------|
| **Meta-Level** | KI-Tool mit KI erstellen → Reflexion |
| **Prompt Engineering** | Echte Skill, nicht automatisierbar |
| **LLM-Evaluation** | Qualitative Bewertung nötig |
| **Kosten-Analyse** | Praktische Business-Entscheidung |
| **Golden Tests** | Aufwändige Testdaten-Erstellung |
| **Multi-Provider** | Echte API-Integration |
| **Feedback-Loop** | Mensch-in-der-Schleife Design |

---

## Projekt genehmigt

Offenburg, den 13.01.2026

_____Dr. Markus Hoffmann_____

DevQuality Labs GmbH
Dr. Markus Hoffmann
CEO DevQuality Labs GmbH
