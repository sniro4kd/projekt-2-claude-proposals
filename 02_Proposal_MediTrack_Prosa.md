# Project Proposal: MediTrack - Medikamenten-Management-System

## Projekteckdaten

Die HealthSoft AG beauftragt ein Team von 6-7 Studierenden mit der Entwicklung eines Medikamenten-Management-Systems. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 40.000 Euro. Ansprechpartnerin ist Dr. Anna Bergmann (Product Owner). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von KI-Assistenten.

---

## 1. Ausgangssituation und Projektziel

Die HealthSoft AG entwickelt Software für Pflegeeinrichtungen. Ein häufiges und ernstes Problem in Seniorenheimen ist die fehlerhafte oder vergessene Medikamentengabe. Jährlich entstehen dadurch erhebliche Gesundheitsrisiken für die Bewohner und hohe Kosten für die Einrichtungen.

Aktuell arbeiten viele Einrichtungen noch mit Papierlisten, händischen Unterschriften und unübersichtlichen Medikamentenschränken. Fehler werden oft erst spät bemerkt, Wechselwirkungen zwischen Medikamenten werden übersehen, und die Dokumentation für Prüfungen ist aufwändig.

Das Ziel ist die Entwicklung eines digitalen Medikamenten-Management-Systems, das Medikamentenpläne verwaltet, Pflegekräfte an fällige Gaben erinnert, die Ausgabe per Barcode dokumentiert, Wechselwirkungen automatisch prüft und die Lagerbestände überwacht.

---

## 2. Besondere Herausforderung: Datenschutz

Da es sich um Gesundheitsdaten handelt, gelten nach Art. 9 DSGVO erhöhte Anforderungen. Diese "besonderen Kategorien personenbezogener Daten" erfordern besondere Schutzmaßnahmen.

Alle Daten müssen verschlüsselt gespeichert werden - sowohl "at rest" (in der Datenbank) als auch "in transit" (bei der Übertragung). Jeder Zugriff auf Patientendaten muss in einem Audit-Log protokolliert werden: Wer hat wann was gesehen oder geändert?

Rollenbasierte Zugriffskontrolle stellt sicher, dass jeder nur das sieht, was er für seine Arbeit braucht. Für Statistiken und Auswertungen müssen Daten anonymisiert werden können.

Eine Datenschutz-Folgenabschätzung (DSFA) ist bei dieser Art von Projekt Pflicht und muss vom Team erstellt werden.

---

## 3. Gewünschte Funktionalität

### Bewohner- und Medikamentenverwaltung

Das System muss Bewohnerdaten verwalten können - Name, Geburtsdatum, Zimmernummer und vor allem bekannte Allergien. Medikamente werden mit Wirkstoff, Dosierung und Pharmazentralnummer (PZN) erfasst.

Für jeden Bewohner können individuelle Medikamentenpläne angelegt werden. Zeitpunkte für die Gabe werden definiert: morgens, mittags, abends, nachts, oder auch "nach Bedarf". Jede Änderung am Medikamentenplan wird historisiert - wer hat wann was geändert.

Der Import von Medikamenten aus einer externen Datenbank würde die Datenpflege erleichtern. Auch das Hochladen von Arztverordnungen als PDF wäre praktisch für die Dokumentation.

### Medikamentengabe und Dokumentation

Das Herzstück im Alltag ist die Übersicht aller aktuell fälligen Gaben. Pflegekräfte sehen auf einen Blick, welche Medikamente jetzt ausgegeben werden müssen.

Die Dokumentation soll per Barcode- oder QR-Code-Scan erfolgen: Medikamentenpackung scannen, Bewohner-Armband scannen, fertig. Das System unterscheidet zwischen "gegeben", "verweigert" (Bewohner wollte nicht) und "nicht gegeben" (anderer Grund).

Bei jeder Dokumentation werden automatisch die Pflegekraft, der Zeitstempel und optional ein Kommentar erfasst. Überfällige Gaben werden optisch hervorgehoben. Push-Benachrichtigungen erinnern die Pflegekräfte rechtzeitig. Eine digitale Unterschrift per Touch-Display auf dem Tablet wäre eine sinnvolle Ergänzung.

### Wechselwirkungsprüfung

Wenn einem Bewohner ein neues Medikament verordnet wird, prüft das System automatisch auf bekannte Wechselwirkungen mit seiner bestehenden Medikation. Wechselwirkungen werden nach Schweregrad klassifiziert: leicht, mittel, schwer.

Bei schweren Wechselwirkungen wird die Eingabe blockiert - nur ein Arzt kann dies mit expliziter Bestätigung überschreiben. Die Wechselwirkungsdatenbank muss wartbar sein, damit neue Erkenntnisse eingepflegt werden können. Auch Allergien sollten bei der Prüfung berücksichtigt werden.

### Lagerverwaltung und Bestellung

Das System führt Lagerbestände für alle Medikamente. Bei jeder dokumentierten Gabe wird der Bestand automatisch reduziert. Unterschreitet der Bestand einen definierten Mindestbestand, wird eine Warnung ausgelöst.

Das Tracking von Verfallsdaten ist wichtig - bald ablaufende Medikamente sollten vorrangig verwendet oder rechtzeitig entsorgt werden. Das System könnte Bestellvorschläge generieren und diese im Idealfall direkt an eine Apotheken-Schnittstelle übermitteln.

### Reporting und Audit

Ein vollständiger Audit-Log protokolliert alle Aktionen: wer hat wann was getan. Dies ist für Prüfungen und im Streitfall essentiell.

Berichte pro Bewohner können als PDF exportiert werden - für Arztbesuche, Verlegungen oder Prüfungen. Statistiken zur Gabe-Compliance zeigen, wie zuverlässig die Medikamentengabe erfolgt. Anonymisierte Auswertungen über alle Bewohner ermöglichen Qualitätsanalysen. Die Dokumentation sollte MDK-konform exportierbar sein.

### Benutzerverwaltung und Sicherheit

Verschiedene Rollen haben unterschiedliche Berechtigungen: Administratoren verwalten das System, Ärzte können Wechselwirkungswarnungen überschreiben, Pflegekräfte dokumentieren Gaben, die Heimleitung sieht Statistiken.

Zwei-Faktor-Authentifizierung ist bei Gesundheitsdaten Pflicht. Automatische Session-Timeouts sorgen dafür, dass unbeaufsichtigte Geräte keine Sicherheitslücke darstellen. Nach mehreren fehlgeschlagenen Login-Versuchen wird das Konto gesperrt. Single-Sign-On über LDAP oder Active Directory erleichtert die Integration in bestehende IT-Landschaften.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt, da dies dem Firmenstandard entspricht und sich im Gesundheitswesen (HIPAA-konform) bewährt hat. PostgreSQL dient als Datenbank - Open Source und mit guter Verschlüsselungsunterstützung.

Das Frontend wird mit Vue.js 3 und TypeScript als Progressive Web App (PWA) entwickelt. Eine PWA ermöglicht Offline-Funktionalität (kritisch, wenn das WLAN ausfällt) und kommt ohne App-Store-Veröffentlichung aus.

Für die Authentifizierung wird ASP.NET Identity mit TOTP (Time-based One-Time Password) für die Zwei-Faktor-Authentifizierung genutzt. PDF-Export erfolgt über QuestPDF oder iText7, Barcode-Scanning über ZXing.NET im Backend und QuaggaJS im Frontend.

Das System muss via Docker deploybar sein.

---

## 5. Qualitätsanforderungen

Die Sicherheitsanforderungen stehen im Vordergrund. Alle Daten müssen mit AES-256 verschlüsselt gespeichert werden. Jede API-Kommunikation läuft über HTTPS. Passwörter werden mit bcrypt oder Argon2 gehasht.

Das System muss gegen die OWASP Top 10 Sicherheitslücken geschützt sein. Ein Security-Audit durch ein anderes Team oder einen Dozenten ist Pflicht, idealerweise ergänzt durch Penetrationstests.

Das System muss 50 gleichzeitige Benutzer unterstützen, mit Seitenaufbau unter 2 Sekunden. Offline-Fähigkeit ist kritisch - wenn das Netzwerk ausfällt, muss die Medikamentengabe trotzdem dokumentiert werden können und später synchronisiert werden. Tägliche automatische Backups sind Pflicht.

---

## 6. Dokumentations- und Testanforderungen

Neben der V-Modell-Standarddokumentation sind zwei spezielle Dokumente Pflicht: eine Datenschutz-Folgenabschätzung (DSFA) nach Art. 35 DSGVO und ein Security-Konzept.

Die DSFA beschreibt systematisch alle Verarbeitungsvorgänge, bewertet deren Notwendigkeit und Verhältnismäßigkeit, analysiert die Risiken für die Rechte der Betroffenen und definiert Maßnahmen zur Risikominimierung. Mindestens 8 Seiten Umfang.

Die Testdokumentation umfasst neben den üblichen Unit-, Integrations- und Systemtests eine spezielle Security-Test-Spezifikation mit mindestens 20 Testfällen basierend auf OWASP. Alle Eingabefelder werden auf SQL-Injection getestet, alle Ausgaben auf XSS. Authentifizierung wird auf Brute-Force und Session-Hijacking geprüft, Autorisierung auf Privilege Escalation.

Ein Penetrationstest durch ein anderes Team oder extern ist Pflicht.

---

## 7. Forschungskomponente: Wechselwirkungsdatenbank

Das Team muss eine einfache Wechselwirkungsdatenbank aufbauen. Dies umfasst die Recherche öffentlich verfügbarer Wechselwirkungsdaten, den Entwurf eines geeigneten Datenmodells, die Implementierung einer Prüflogik mit Schweregrad-Klassifikation und die Evaluation mit Testfällen bekannter Wechselwirkungen.

Es geht um das Prinzip, nicht um medizinische Vollständigkeit - 20-30 exemplarische Wechselwirkungen sind ausreichend.

---

## 8. Besondere Prozessanforderungen

Wegen der Security-Kritikalität benötigt jeder Pull Request zwei Approvals statt nur einem. Alle Authentifizierungs-Komponenten erhalten dedizierte Security-Reviews. Zu Projektbeginn wird ein Threat Modeling Workshop durchgeführt, um potenzielle Angriffsvektoren zu identifizieren.

Code, der mit KI-Assistenten erstellt wurde, muss besonders sorgfältig auf Security-Probleme geprüft werden.

---

Offenburg, den 13.01.2026

Prof. Dr. Sabine Maier
CISO HealthSoft AG
