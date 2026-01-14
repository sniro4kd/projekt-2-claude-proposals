# Project Proposal: CodeGuardian - KI-gestütztes Code-Review-System

## Projekteckdaten

Die DevQuality Labs GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung eines KI-gestützten Code-Review-Systems. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 35.000 Euro. Ansprechpartner ist Dr. Stefan Meier (Product Owner). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von KI-Assistenten.

---

## 1. Ausgangssituation und Projektziel

Die DevQuality Labs GmbH bietet Qualitätssicherungs-Tools für Softwareunternehmen an. Ein wachsender Markt sind KI-gestützte Code-Review-Systeme, die Code automatisch auf Best Practices, Security-Issues und Code Smells prüfen.

Manuelle Code-Reviews sind zeitaufwändig und von der Erfahrung des Reviewers abhängig. Statische Code-Analyse-Tools finden zwar Probleme, liefern aber oft kryptische Meldungen ohne Erklärung oder Lösungsvorschlag.

Die Vision: Ein System, das Git-Repositories analysiert, Pull Requests automatisch reviewed, gefundene Probleme mit verständlichen, KI-generierten Erklärungen anreichert und konkrete Fix-Vorschläge macht. Ein Dashboard zeigt Team-Metriken zur Code-Qualität über Zeit.

---

## 2. Besondere Herausforderung: LLM-Integration und Evaluation

Dieses Projekt verbindet klassische Softwareentwicklung mit KI-Integration. Die Nutzung von LLM-APIs (Claude, GPT) für natürlichsprachige Erklärungen erfordert sorgfältiges Prompt Engineering. Eigene Heuristiken für statische Code-Analyse müssen entwickelt werden, da LLMs allein nicht zuverlässig genug sind.

Besonders interessant ist die Evaluation und das Benchmarking der KI-Qualität: Wie gut sind die generierten Erklärungen? Helfen die Fix-Vorschläge wirklich? Gibt es Halluzinationen?

Die Meta-Ebene ist faszinierend: Ein KI-Tool, das Code bewertet, der selbst teils mit KI erstellt wurde.

---

## 3. Gewünschte Funktionalität

### Repository-Integration

Das System muss GitHub-Repositories anbinden können, authentifiziert über OAuth. Push-Events und Pull Requests werden via Webhook empfangen. Die Analyse-Ergebnisse sollen direkt als Kommentare im Pull Request erscheinen - so wie ein menschlicher Reviewer Feedback geben würde.

GitLab-Unterstützung wäre eine sinnvolle Erweiterung, Bitbucket optional. Für Entwickler ohne Cloud-Repository sollte auch eine CLI-Variante existieren, die lokale Repositories analysiert.

### Statische Code-Analyse

Die Analyse muss mehrere Programmiersprachen unterstützen: C# als Firmenstandard, TypeScript/JavaScript für Frontend-Code, Python für Data-Science-Projekte.

Die Erkennung umfasst mehrere Kategorien. Code Smells sind Muster, die auf Probleme hindeuten: zu lange Methoden, zu hohe zyklomatische Komplexität, tiefe Verschachtelung, God Classes mit zu vielen Verantwortlichkeiten. Security Issues sind Sicherheitslücken wie SQL-Injection-Anfälligkeit, XSS-Patterns, oder hardcodierte Credentials. Style Violations sind Verstöße gegen Coding-Conventions, basierend auf konfigurierbaren Regeln.

Eigene Regeln sollten per YAML definierbar sein. Die Integration existierender Linter (ESLint für JavaScript, Roslyn Analyzers für C#, Pylint für Python) reichert die Analyse an.

### LLM-Integration

Das Alleinstellungsmerkmal ist die Anreicherung der Findings mit LLM-generierten Erklärungen. Statt einer kryptischen Meldung "CC > 15" erklärt das System in natürlicher Sprache, warum hohe zyklomatische Komplexität problematisch ist und wie man die Methode vereinfachen könnte.

Fix-Vorschläge zeigen konkreten Code, der das Problem behebt. Das System muss verschiedene LLM-Provider unterstützen - Claude und GPT als Minimum - um Ausfälle eines Providers abzufangen und Kosten zu optimieren.

Rate-Limiting verhindert, dass API-Budgets überschritten werden. Caching ist essentiell: Wenn derselbe Code-Abschnitt mehrfach analysiert wird, muss nicht jedes Mal das LLM aufgerufen werden. Gleicher Input sollte gleichen Output liefern (Konsistenz).

Confidence-Scores könnten anzeigen, wie sicher sich das System bei einer Suggestion ist. Prompt-Templates sollten konfigurierbar sein, um die Ergebnisqualität zu optimieren. Für Umgebungen ohne Internet-Zugang könnte ein lokales LLM (via Ollama) als Fallback dienen.

### Review-Dashboard

Das Dashboard zeigt alle analysierten Pull Requests mit ihren Findings. Filterung nach Severity (Critical, Warning, Info) ermöglicht Fokussierung auf das Wichtige.

Findings können als "accepted" (wird behoben) oder "dismissed" (Fehlalarm, bewusste Entscheidung) markiert werden. Die Code-Diff-Ansicht zeigt Findings inline im geänderten Code.

Trends über Zeit visualisieren, ob die Code-Qualität besser oder schlechter wird. Team-Metriken zeigen Issues pro Entwickler und Fix-Raten - natürlich nicht zum Blame, sondern um Schulungsbedarf zu erkennen. Reports können exportiert werden.

### Feedback-Loop

Das System lernt aus dem Feedback der Nutzer. "War diese Erklärung hilfreich?" - Ja/Nein. Diese Daten fließen in Statistiken ein: Welche Regeln produzieren viele Fehlalarme? Welche LLM-Erklärungen werden als nicht hilfreich bewertet?

Regeln, die häufig dismissed werden, könnten zur Deaktivierung vorgeschlagen werden. Langfristig könnte das Feedback sogar zur Prompt-Optimierung genutzt werden.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. Für Background Processing von Analyse-Jobs kommt Hangfire oder RabbitMQ zum Einsatz. PostgreSQL speichert Findings und Metriken, Redis cached LLM-Responses.

Das Frontend wird mit Vue.js 3 entwickelt. Für die Git-Integration werden LibGit2Sharp (lokaler Zugriff) und die GitHub API (Cloud-Integration) verwendet.

Die LLM-Integration nutzt die APIs von Anthropic (Claude) und OpenAI. Für die statische Analyse werden Roslyn (C#), ESLint (JavaScript) und Pylint (Python) integriert.

Das System wird via Docker deployed.

---

## 5. Qualitätsanforderungen

Die Analyse eines Pull Requests mit weniger als 500 geänderten Zeilen muss unter 30 Sekunden dauern. Die LLM-Anreicherung sollte unter 10 Sekunden pro Finding liegen. Das System muss 50 gleichzeitige Analysen verarbeiten können.

LLM-API-Kosten müssen pro Analyse getrackt werden. Ein Budget-Limit pro Tag und Monat verhindert Kostenexplosionen. Wenn das Budget erreicht ist, fällt das System auf Basis-Analyse ohne LLM zurück.

OAuth-Tokens und LLM-API-Keys müssen sicher (verschlüsselt) gespeichert werden. Sensible Code-Abschnitte (über Konfiguration markierbar) dürfen nicht an externe LLMs gesendet werden. Webhook-Signatures müssen validiert werden, um Manipulation zu verhindern.

---

## 6. Dokumentations- und Testanforderungen

Neben der V-Modell-Standarddokumentation sind zwei spezielle Dokumente Pflicht: eine Prompt Engineering Dokumentation und eine LLM-Kosten-Analyse.

Die Testdokumentation umfasst Golden Tests - eine Suite von Code-Snippets mit bekannten Problemen und erwarteten Findings. Für jede Sprache und jeden Problemtyp gibt es definierte Testfälle: C#-Code mit SQL-Injection muss als Security-Issue erkannt werden, eine 200-Zeilen-Methode als Smell.

Die LLM-Evaluation prüft die Qualität der generierten Texte: Sind die Erklärungen fachlich korrekt? Helfen die Fix-Vorschläge? Sind die Ergebnisse konsistent? Werden gefährliche Security-Entwarnung vermieden?

Precision und Recall messen die Erkennungsqualität: Werden alle Probleme gefunden (Recall)? Sind die gemeldeten Probleme auch wirklich Probleme (Precision)?

---

## 7. Forschungskomponente: Prompt Engineering

Das Team muss systematisches Prompt Engineering durchführen und dokumentieren. Beginnend mit Baseline-Prompts für jede Aufgabe (Erklärung generieren, Fix vorschlagen) werden mindestens drei Iterationen zur Verbesserung durchgeführt.

A/B-Testing vergleicht verschiedene Prompt-Varianten: Ist ein kurzer Prompt besser als ein ausführlicher? Hilft Few-Shot-Learning mit Beispielen? Die Evaluation erfolgt nach einer definierten Rubrik.

Ergebnis ist eine Dokumentation von mindestens 10 Seiten mit den finalen Prompts, der Begründung für Design-Entscheidungen und den Evaluationsergebnissen.

### LLM-Kosten-Analyse

Eine wirtschaftliche Analyse vergleicht die LLM-Provider: Tokens und Kosten pro Analyse, Qualitätsunterschiede zwischen Claude und GPT, Latenzvergleich. Wie effektiv ist Caching - wie viel spart es tatsächlich? Ab welchem Nutzungsvolumen würde sich ein lokales LLM lohnen?

---

## 8. Meta-Reflexion

Ein besonderer Aspekt dieses Projekts ist die Meta-Ebene: Das Team entwickelt ein KI-Tool zur Code-Analyse, wobei es selbst KI-Assistenten einsetzt. Die Reflexion dokumentiert: Wie gut erkennt das entwickelte System Issues in KI-generiertem Code? Welche typischen Probleme erzeugt KI-Code? Welche Empfehlungen ergeben sich für das Review von KI-Code?

---

## 9. Besondere Prozessanforderungen

Wegen der Kosten-Sensitivität gibt es ein wöchentliches API-Budget von maximal 50€. Neue Prompts benötigen nicht nur ein normales Code-Review, sondern ein Team-Review - schlechte Prompts können teure Folgen haben.

---

Offenburg, den 13.01.2026

Dr. Markus Hoffmann
CEO DevQuality Labs GmbH
