# Softwareprojekte im Zeitalter von KI-Assistenten

## Eine theoretische Analyse zur Anpassung von Lehrprojekten

---

## 1. Ausgangssituation und Problemstellung

### 1.1 Der Produktivitätssprung durch KI-Assistenten

Das CatchTheRabbit-Projekt demonstriert eindrucksvoll die Auswirkungen von KI-Assistenten wie Claude Code auf die Softwareentwicklung:

| Metrik | Traditionell (6-7 Studierende) | Mit Claude Code |
|--------|-------------------------------|-----------------|
| Personenstunden | 180-280h | ~5h |
| Produktivitätsfaktor | 1x | **36-56x** |
| Code-Output | ~5.100 LOC | ~5.100 LOC |
| Dokumentation | V-Modell komplett | V-Modell komplett |
| Testabdeckung | variabel | 83.8% |

Dieser massive Produktivitätssprung stellt die traditionelle Projektlehre vor fundamentale Herausforderungen.

### 1.2 Was KI-Assistenten besonders gut können

1. **Boilerplate-Code generieren** - CRUD-Operationen, API-Endpoints, Datenmodelle
2. **Bekannte Patterns implementieren** - MVC, Repository, Factory, etc.
3. **Dokumentation erstellen** - Technische Docs nach Vorlagen
4. **Tests schreiben** - Unit-, Integrations- und E2E-Tests
5. **Debugging** - Fehlermeldungen analysieren und beheben
6. **Refactoring** - Code nach Best Practices umstrukturieren
7. **Standard-Algorithmen** - Sortierung, Suche, bekannte Spielalgorithmen (Minimax)

### 1.3 Was KI-Assistenten weniger gut können

1. **Echte Stakeholder-Kommunikation** - Requirements Engineering mit realen Kunden
2. **Kreative Problemlösung** - Neuartige Algorithmen für unbekannte Probleme
3. **Hardware-Interaktion** - IoT, Sensoren, physische Systeme
4. **Team-Koordination** - Merge-Konflikte, Code-Reviews, Pair Programming
5. **Domänenwissen** - Fachliche Expertise in spezifischen Bereichen
6. **Security-Testing** - Echte Penetrationstests und Threat Modeling
7. **UX-Research** - Nutzerstudien, A/B-Tests mit echten Nutzern
8. **DevOps-Realität** - Echte Server, Netzwerkkonfiguration, Monitoring
9. **Legacy-Integration** - Arbeit mit schlecht dokumentierten Altsystemen
10. **Ethische Entscheidungen** - Datenschutz, Fairness, gesellschaftliche Auswirkungen

---

## 2. Strategien zur Projektanpassung

### 2.1 Strategie A: Komplexitätserweiterung (Vertikal)

**Prinzip:** Das Projekt bleibt thematisch ähnlich, aber die technische Komplexität wird drastisch erhöht.

**Umsetzung:**
- Microservices statt Monolith
- Event-Driven Architecture mit Message Queues
- Multi-Datenbank-Architekturen (SQL + NoSQL + Cache)
- Kubernetes-Deployment statt Docker-Compose
- CI/CD-Pipelines mit Quality Gates
- Observability Stack (Logging, Metrics, Tracing)

**Aufwandsfaktor:** 3-5x gegenüber Basisprojekt

### 2.2 Strategie B: Scope-Erweiterung (Horizontal)

**Prinzip:** Das Projekt umfasst deutlich mehr Features und Domänen.

**Umsetzung:**
- Mehrere verbundene Anwendungen (z.B. Admin-Portal + User-App + Analytics)
- Integration mit 3+ externen APIs
- Multi-Plattform (Web + Mobile + Desktop)
- Mehrsprachigkeit und Barrierefreiheit
- Umfangreiche Business-Logik

**Aufwandsfaktor:** 4-6x gegenüber Basisprojekt

### 2.3 Strategie C: Prozess-Intensivierung

**Prinzip:** Der Entwicklungsprozess selbst wird zum Lerninhalt.

**Umsetzung:**
- Pflicht zu Code-Reviews (jeder PR braucht 2 Approvals)
- Pair/Mob-Programming Sessions (dokumentiert)
- Sprint-Reviews mit echten Stakeholdern
- Retrospektiven mit Maßnahmenverfolgung
- Architektur-Decision-Records für JEDE Entscheidung
- Technische Schulden bewusst managen

**Aufwandsfaktor:** 2-3x gegenüber Basisprojekt

### 2.4 Strategie D: Research-Komponente

**Prinzip:** Das Projekt enthält genuinen Forschungsanteil.

**Umsetzung:**
- Eigene ML-Modelle trainieren (nicht nur APIs nutzen)
- Algorithmen-Vergleich mit statistischer Auswertung
- Nutzerstudien durchführen und auswerten
- Performance-Benchmarks und Optimierung
- Literaturrecherche und State-of-the-Art Analyse

**Aufwandsfaktor:** 3-4x gegenüber Basisprojekt

### 2.5 Strategie E: Real-World-Integration

**Prinzip:** Das Projekt interagiert mit der echten Welt.

**Umsetzung:**
- Hardware-Komponenten (IoT, Sensoren, Aktoren)
- Echte externe APIs (mit Rate-Limits, Kosten, Ausfällen)
- Deployment auf echte Infrastruktur (Cloud, Server)
- Integration mit Legacy-Systemen
- Datenschutz-Compliance (DSGVO)

**Aufwandsfaktor:** 4-6x gegenüber Basisprojekt

---

## 3. Didaktische Überlegungen

### 3.1 Lernziele im KI-Zeitalter

Die Lernziele müssen sich verschieben von:

| Traditionell | KI-Zeitalter |
|-------------|--------------|
| Code schreiben | Code verstehen und validieren |
| Syntax beherrschen | Architektur entwerfen |
| Algorithmen implementieren | Algorithmen auswählen und bewerten |
| Tests schreiben | Teststrategien entwickeln |
| Dokumentation erstellen | Requirements verstehen und hinterfragen |

### 3.2 Meta-Kompetenzen

Studierende sollten lernen:

1. **Prompt Engineering** - Wie formuliere ich Anforderungen an KI-Assistenten?
2. **Code Review** - Wie erkenne ich Fehler in KI-generiertem Code?
3. **Architekturentscheidungen** - Wann ist welcher Ansatz sinnvoll?
4. **KI-Limitationen** - Wann ist manuelle Arbeit besser?
5. **Ethik und Verantwortung** - Wer haftet für KI-generierten Code?

### 3.3 Bewertungskriterien anpassen

**Traditionell:**
- Funktionalität (40%)
- Codequalität (30%)
- Dokumentation (20%)
- Präsentation (10%)

**KI-Zeitalter:**
- Architekturentscheidungen und deren Begründung (25%)
- Prozessqualität (Reviews, Retrospektiven, Kommunikation) (25%)
- Testabdeckung und -strategie (20%)
- Innovation/Research-Komponente (15%)
- Reflexion über KI-Einsatz (15%)

---

## 4. Empfehlungen für Projektumfang

### 4.1 Zielaufwand berechnen

**Annahme:**
- Team: 6 Studierende
- Ziel-Aufwand: 30-40h pro Person = 180-240 Personenstunden
- Produktivitätsfaktor mit Claude Code: ~40x für Standardaufgaben

**Berechnung:**
```
Basis-Komplexität (ohne KI): 180-240h
Mit KI für Standardaufgaben: 180-240h / 40 = 4.5-6h

Zusätzlicher Aufwand durch Strategien:
- Komplexitätserweiterung: +100-150h
- Prozess-Intensivierung: +50-80h
- Research-Komponente: +60-100h
- Real-World-Integration: +80-120h

Gesamtziel: 180-240h pro Team mit KI-Einsatz
```

### 4.2 Empfohlene Projektkombination

Für einen Aufwand von **180-240 Personenstunden mit KI-Assistenten**:

| Komponente | Anteil | Stunden |
|------------|--------|---------|
| Basis-Implementierung (KI-unterstützt) | 5% | 10-15h |
| Komplexitätserweiterung (Microservices, K8s) | 25% | 45-60h |
| Prozess-Intensivierung (Reviews, Retros) | 20% | 36-48h |
| Research/Innovation | 25% | 45-60h |
| Real-World-Integration | 25% | 45-60h |

---

## 5. Organisatorische Rahmenbedingungen

### 5.1 Regeln für KI-Nutzung

1. **Transparenz-Pflicht:** Jeder KI-generierte Code muss als solcher markiert werden
2. **Review-Pflicht:** KI-Code muss von einem anderen Teammitglied reviewed werden
3. **Verständnis-Nachweis:** Studierende müssen KI-Code erklären können
4. **Dokumentationspflicht:** Prompts und KI-Interaktionen werden dokumentiert
5. **Keine KI für bestimmte Bereiche:** z.B. Architekturdokumentation, Retrospektiven

### 5.2 Prüfungsrelevante Aspekte

- **Mündliche Verteidigung:** Studierende müssen Code erklären können
- **Live-Coding:** Kleine Änderungen ohne KI durchführen
- **Architektur-Diskussion:** Warum diese Entscheidungen?
- **Prozess-Reflexion:** Was lief gut/schlecht im Team?

---

## 6. Zusammenfassung

Die Integration von KI-Assistenten in die Projektlehre erfordert:

1. **Projektumfang deutlich erhöhen** (Faktor 4-6x)
2. **Fokus auf Architektur und Prozess** statt reiner Implementierung
3. **Research-Komponenten einbauen** für genuinen Lerneffekt
4. **Real-World-Integration** für praktische Erfahrung
5. **Prozessqualität bewerten** nicht nur Ergebnis
6. **Transparenz und Reflexion** über KI-Einsatz fordern

Die folgenden Projektproposals sind nach diesen Prinzipien gestaltet.
