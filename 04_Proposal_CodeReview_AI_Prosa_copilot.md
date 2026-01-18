# Project Proposal: CodeGuardian - KI-gestütztes Code-Review-System (Copilot-Version)

## Projekteckdaten

Die DevQuality Labs GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung eines KI-gestützten Code-Review-Systems. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 35.000 Euro. Ansprechpartner ist Dr. Stefan Meier (Product Owner). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von GitHub Copilot (Claude Haiku/Sonnet).

---

## 1. Ausgangssituation und Projektziel

Die DevQuality Labs GmbH bietet Qualitätssicherungs-Tools an. Manuelle Code-Reviews sind zeitaufwändig. Statische Analyse-Tools finden Probleme, liefern aber oft kryptische Meldungen.

Die Vision: Ein System, das Code analysiert, gefundene Probleme mit verständlichen, KI-generierten Erklärungen anreichert und Fix-Vorschläge macht.

---

## 2. Besondere Herausforderung: LLM-Integration

Dieses Projekt verbindet klassische Softwareentwicklung mit KI-Integration. Die Nutzung von LLM-APIs (Claude) für natürlichsprachige Erklärungen erfordert sorgfältiges Prompt-Design.

---

## 3. Gewünschte Funktionalität

### Code-Upload und Analyse (Kernfunktionalität)

Benutzer können Code-Dateien hochladen oder Code direkt eingeben. Die Analyse unterstützt eine Programmiersprache: C# oder TypeScript/JavaScript.

Das System erkennt Code Smells wie zu lange Methoden (über 50 Zeilen), zu tiefe Verschachtelung (über 4 Ebenen) und hohe Komplexität.

### LLM-Integration (Kernfunktionalität)

Gefundene Probleme werden mit LLM-generierten Erklärungen angereichert. Statt "Methode zu lang" erklärt das System in natürlicher Sprache, warum das problematisch ist.

Fix-Vorschläge zeigen, wie das Problem behoben werden könnte.

Die Integration nutzt die Claude API. Caching verhindert wiederholte API-Aufrufe für gleichen Code.

### Dashboard (Kernfunktionalität)

Das Dashboard zeigt alle analysierten Code-Snippets mit ihren Findings. Filterung nach Severity (Critical, Warning, Info).

Findings können als "accepted" oder "dismissed" markiert werden.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. PostgreSQL speichert Findings, Redis cached LLM-Responses.

Das Frontend wird mit Vue.js 3 entwickelt.

Die LLM-Integration nutzt die API von Anthropic (Claude).

Das System wird via Docker deployed.

---

## 5. Qualitätsanforderungen

Die Analyse eines Code-Snippets mit weniger als 200 Zeilen muss unter 30 Sekunden dauern.

LLM-API-Kosten müssen pro Analyse getrackt werden. Ein Tages-Budget-Limit (z.B. 10€) verhindert Kostenexplosionen.

API-Keys müssen sicher gespeichert werden.

---

## 6. Dokumentations- und Testanforderungen

V-Modell-Standarddokumentation plus eine Prompt-Dokumentation, die die verwendeten Prompts beschreibt.

Die Testdokumentation umfasst Golden Tests - eine Suite von Code-Snippets mit bekannten Problemen und erwarteten Findings (mindestens 10 Testfälle).

Code-Coverage über 60%.

---

## 7. Vereinfachte Forschungskomponente

Das Team dokumentiert verschiedene Prompt-Varianten und vergleicht deren Ergebnisqualität. Mindestens 3 verschiedene Prompt-Versionen werden getestet.

Ein Report von 5 Seiten beschreibt die Prompts, deren Unterschiede und welcher am besten funktioniert.

---

## Hinweis zur KI-Unterstützung

Dieses Projekt ist für die Bearbeitung mit GitHub Copilot (Claude Haiku/Sonnet) ausgelegt. Copilot unterstützt bei:
- Code-Vervollständigung und Boilerplate-Generierung
- Einfachen Debugging-Aufgaben
- Code-Erklärungen und Dokumentation

Die Studierenden müssen aktiv die Architekturentscheidungen treffen und den generierten Code verstehen und überprüfen.

Meta-Aspekt: Dieses Projekt nutzt KI (Copilot) um ein KI-Tool (CodeGuardian) zu entwickeln.

---

Offenburg, den 13.01.2026

Dr. Markus Hoffmann
CEO DevQuality Labs GmbH
