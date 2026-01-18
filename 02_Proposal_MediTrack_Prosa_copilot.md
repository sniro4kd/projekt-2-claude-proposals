# Project Proposal: MediTrack - Medikamenten-Management-System (Copilot-Version)

## Projekteckdaten

Die HealthSoft AG beauftragt ein Team von 6-7 Studierenden mit der Entwicklung eines Medikamenten-Management-Systems. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 40.000 Euro. Ansprechpartnerin ist Dr. Anna Bergmann (Product Owner). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von GitHub Copilot (Claude Haiku/Sonnet).

---

## 1. Ausgangssituation und Projektziel

Die HealthSoft AG entwickelt Software für Pflegeeinrichtungen. Ein häufiges Problem in Seniorenheimen ist die fehlerhafte oder vergessene Medikamentengabe.

Das Ziel ist die Entwicklung eines digitalen Medikamenten-Management-Systems, das Medikamentenpläne verwaltet, Pflegekräfte an fällige Gaben erinnert und die Ausgabe dokumentiert.

---

## 2. Besondere Herausforderung: Datenschutz

Da es sich um Gesundheitsdaten handelt, gelten nach Art. 9 DSGVO erhöhte Anforderungen. Alle Daten müssen verschlüsselt gespeichert werden. Jeder Zugriff auf Patientendaten muss protokolliert werden.

Eine einfache Datenschutz-Dokumentation ist Teil des Projekts.

---

## 3. Gewünschte Funktionalität

### Bewohner- und Medikamentenverwaltung (Kernfunktionalität)

Das System verwaltet Bewohnerdaten - Name, Geburtsdatum, Zimmernummer und bekannte Allergien. Medikamente werden mit Wirkstoff und Dosierung erfasst.

Für jeden Bewohner können individuelle Medikamentenpläne angelegt werden mit Zeitpunkten: morgens, mittags, abends, nachts.

### Medikamentengabe und Dokumentation (Kernfunktionalität)

Das Herzstück ist die Übersicht aller aktuell fälligen Gaben. Pflegekräfte sehen, welche Medikamente ausgegeben werden müssen.

Die Dokumentation erfolgt durch Auswahl von Bewohner und Medikament. Das System unterscheidet zwischen "gegeben", "verweigert" und "nicht gegeben".

Bei jeder Dokumentation werden automatisch die Pflegekraft und der Zeitstempel erfasst. Überfällige Gaben werden optisch hervorgehoben.

### Einfache Wechselwirkungsprüfung

Wenn einem Bewohner ein neues Medikament verordnet wird, prüft das System auf bekannte Wechselwirkungen mit einer einfachen Datenbank (10-20 exemplarische Wechselwirkungen).

### Benutzerverwaltung (Kernfunktionalität)

Verschiedene Rollen: Administratoren verwalten das System, Pflegekräfte dokumentieren Gaben.

Login mit Passwort. Automatische Session-Timeouts nach Inaktivität.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. PostgreSQL dient als Datenbank.

Das Frontend wird mit Vue.js 3 und TypeScript entwickelt.

Das System muss via Docker deploybar sein.

---

## 5. Qualitätsanforderungen

Alle Daten werden verschlüsselt gespeichert. Passwörter werden mit bcrypt gehasht.

Das System muss 10 gleichzeitige Benutzer unterstützen. Seitenaufbau unter 3 Sekunden.

---

## 6. Dokumentations- und Testanforderungen

Neben der V-Modell-Standarddokumentation ist eine einfache Datenschutz-Dokumentation Pflicht (3-4 Seiten), die beschreibt, welche Daten gespeichert werden und wie sie geschützt sind.

Die Testdokumentation umfasst Unit- und Integrationstests. Mindestens 15 Unit-Tests, 8 Integrationstests. Code-Coverage über 60%.

---

## 7. Vereinfachte Forschungskomponente

Das Team baut eine einfache Wechselwirkungsdatenbank mit 10-20 exemplarischen Wechselwirkungen auf. Ein kurzer Report (4 Seiten) beschreibt das Datenmodell und die Prüflogik.

---

## Hinweis zur KI-Unterstützung

Dieses Projekt ist für die Bearbeitung mit GitHub Copilot (Claude Haiku/Sonnet) ausgelegt. Copilot unterstützt bei:
- Code-Vervollständigung und Boilerplate-Generierung
- Einfachen Debugging-Aufgaben
- Code-Erklärungen und Dokumentation

Die Studierenden müssen aktiv die Architekturentscheidungen treffen und den generierten Code verstehen und überprüfen. Bei sicherheitskritischem Code ist besondere Sorgfalt geboten.

---

Offenburg, den 13.01.2026

Prof. Dr. Sabine Maier
CISO HealthSoft AG
