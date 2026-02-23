# Project Proposal

| | |
|---|---|
| Firma | ERP_Champion GmbH |
| Projekt | SecureCollab |
| Product Owner | Frank Niederbronn B.Sc. |
| Projektlaufzeit | März – Juni 2026 |
| Budget | 20.000 Euro |
| Version | 2.0 |
| Datum | 23.02.2026 |
| Dokumentenverantwortlicher | Frank Niederbronn |

---

ERP_Champion GmbH arbeitet im Rahmen von Kundenprojekten regelmäßig mit externen Partnern zusammen — Beratungshäusern, Zulieferern und freiberuflichen Spezialisten. Dabei werden häufig vertrauliche Dokumente ausgetauscht: Verträge, technische Spezifikationen, Angebote, Protokolle und Projektpläne. Bislang geschieht dieser Austausch in der Praxis über E-Mail-Anhänge, gelegentlich über persönliche Cloud-Speicher-Accounts einzelner Mitarbeiter und in manchen Fällen sogar über USB-Sticks bei Vor-Ort-Terminen. Dieses Vorgehen ist nicht nur umständlich, sondern auch aus Sicherheits- und Compliance-Sicht problematisch: Es gibt keine zentrale Übersicht darüber, wer wann auf welches Dokument zugegriffen hat, Versionskonflikte sind an der Tagesordnung, und bei einem Audit können wir nicht nachweisen, welcher Mitarbeiter welchem Externen welches Dokument bereitgestellt hat.

**SecureCollab** soll dieses Problem lösen. Es handelt sich um ein browserbasiertes, sicheres Dateimanagement-System, das die Zusammenarbeit mit internen und externen Beteiligten ermöglicht — mit vollständiger **Zugriffskontrolle**, **Versionierung**, **Kommentarfunktion** und einem lückenlosen **Audit-Trail**. Das System soll die bisherigen ad-hoc-Lösungen ablösen und unserem Unternehmen helfen, die Anforderungen der DSGVO und interner Compliance-Richtlinien einzuhalten.

## Dateiverwaltung und Ordnerstruktur

Das Herzstück von SecureCollab ist eine **hierarchische Ordnerstruktur**, ähnlich wie man sie aus dem Windows Explorer oder Finder kennt, allerdings im Browser. Benutzer sollen Ordner erstellen, umbenennen, verschieben und löschen können. Innerhalb der Ordner werden Dateien abgelegt, die entweder per **Drag & Drop** direkt in den Browser gezogen oder über einen klassischen Dateiauswahl-Dialog hochgeladen werden. Die maximale Dateigröße soll bei 50 MB pro Datei liegen, was für unsere typischen Dokumente (PDF, Word, Excel, Bilder, Textdateien) bei weitem ausreicht.

Zu den hochgeladenen Dateien soll das System eine **Vorschau** anbieten können, ohne dass der Benutzer die Datei erst herunterladen muss. Mindestens für PDF-Dateien, gängige Bildformate (PNG, JPG, GIF) und Textdateien (.txt, .csv, .md) soll eine Vorschau direkt im Browser möglich sein. Für andere Dateitypen genügt es, den Dateinamen, die Größe, den Upload-Zeitpunkt und den Ersteller anzuzeigen.

Darüber hinaus sollen Dateien mit **frei wählbaren Tags** versehen werden können — beispielsweise „Vertrag", „Entwurf", „Freigegeben" oder „Vertraulich". Diese Tags sollen bei der **Suche** als Filter dienen. Die Suchfunktion soll es ermöglichen, nach Dateinamen und nach Tags zu suchen. Eine Volltextsuche im Dateiinhalt wäre wünschenswert, ist aber nicht zwingend erforderlich, wenn sie den Rahmen des Projekts sprengen würde.

Benutzer sollen einzelne Dateien herunterladen können. Darüber hinaus soll es möglich sein, einen gesamten Ordner als ZIP-Archiv herunterzuladen — das erspart bei der Übergabe größerer Dokumentenpakete an externe Partner viel Zeit.

## Versionierung

Ein zentrales Problem beim heutigen Dokumentenaustausch per E-Mail ist die Versionskonfusion: „Angebot_final.pdf", „Angebot_final_v2.pdf", „Angebot_final_v2_korrektur_FN.pdf" — das kennt wohl jeder. SecureCollab soll dieses Problem durch eine automatische **Versionierung** lösen.

Wenn ein Benutzer eine Datei mit demselben Namen in denselben Ordner hochlädt, soll das System dies als neue Version derselben Datei erkennen und behandeln — nicht als separate Datei. Die ältere Version bleibt erhalten und ist über eine **Versionshistorie** abrufbar, die anzeigt, wer wann welche Version hochgeladen hat. Der Benutzer soll zwischen den Versionen wechseln und bei Bedarf eine ältere Version **wiederherstellen** können (Rollback).

Für Textdateien (insbesondere .txt, .csv, .md) soll eine **Diff-Ansicht** angeboten werden, die die Unterschiede zwischen zwei ausgewählten Versionen hervorhebt — ähnlich wie man es aus Git-Diffs kennt, mit grün markierten Ergänzungen und rot markierten Löschungen. Für Binärdateien (PDF, Bilder) genügt der Hinweis, dass eine neue Version existiert, ohne inhaltlichen Vergleich.

## Kommentare und Diskussionen

An jede Datei sollen **Kommentare** angehängt werden können. Die Kommentare sollen als **threaded Discussions** organisiert sein — das heißt, man kann auf einen bestehenden Kommentar antworten, wodurch eine nachvollziehbare Diskussion entsteht, anstatt eine flache, chronologische Liste. Dies ist besonders wichtig bei Vertragsprüfungen, wo verschiedene Abteilungen Anmerkungen zu einem Dokument machen und darüber diskutieren.

Jeder Benutzer soll seine eigenen Kommentare bearbeiten und löschen können. Kommentare anderer Benutzer sollen nur von Administratoren löschbar sein. Wenn ein Kommentar gelöscht wird, der Antworten hat, soll der Inhalt durch einen Platzhalter wie „Kommentar wurde entfernt" ersetzt werden, damit die Thread-Struktur erhalten bleibt.

Es wäre außerdem hilfreich, wenn Benutzer in Kommentaren andere Benutzer per **@-Mention** erwähnen könnten und diese darüber benachrichtigt werden — entweder per E-Mail oder über eine Benachrichtigungsanzeige innerhalb der Anwendung. Diese Funktion ist allerdings als „Soll" einzustufen, nicht als „Muss".

## Zugriffskontrolle und Rollen

Die Zugriffskontrolle ist für unser Unternehmen der kritischste Aspekt des Systems. Wir arbeiten mit vertraulichen Dokumenten, und es muss sichergestellt sein, dass jeder Benutzer nur die Dateien sehen und bearbeiten kann, für die er berechtigt ist.

Das System soll ein **rollenbasiertes Zugriffskonzept (RBAC)** mit mindestens vier Rollen implementieren:

Der **Administrator** hat Vollzugriff auf das gesamte System. Er kann Benutzer anlegen, Rollen zuweisen, Benutzer deaktivieren, den Audit-Trail einsehen und Systemeinstellungen ändern. In der Regel sind das nur ein bis zwei Personen pro Installation.

Der **Manager** kann innerhalb seines Zuständigkeitsbereichs Ordner erstellen, Dateien hochladen und herunterladen, Freigaben erteilen und Kommentare verfassen. Er kann auch Berechtigungen für Unterordner vergeben, allerdings nur Rechte weitergeben, die er selbst besitzt.

Der **Mitarbeiter** kann Dateien hochladen, herunterladen und kommentieren — jedoch nur in Ordnern, für die er eine explizite Berechtigung hat. Er kann keine Berechtigungen an andere vergeben.

Der **Externe Gast** hat den eingeschränktesten Zugang. Er kann nur die für ihn freigegebenen Ordner und Dateien einsehen und herunterladen. Er hat keine Upload-Berechtigung (es sei denn, sie wird explizit für einen bestimmten Ordner erteilt) und sieht keine anderen Bereiche des Systems.

Besonders wichtig ist, dass sich Berechtigungen auf Ordnerebene **vererben**: Wenn ein Manager die Berechtigung für den Ordner „Projekt Alpha" erhält, soll er automatisch auch auf alle Unterordner zugreifen können. Es muss aber möglich sein, für einen bestimmten Unterordner die Berechtigung einzuschränken oder zu überschreiben — etwa wenn innerhalb von „Projekt Alpha" ein Unterordner „Gehälter" existiert, der nur für den Administrator sichtbar sein soll. Diese Kombination aus Vererbung und Überschreibung ist komplex und muss sorgfältig entworfen und getestet werden.

## Freigabe-Links und externe Zusammenarbeit

Nicht alle externen Partner sollen ein dauerhaftes Benutzerkonto im System benötigen. Für den gelegentlichen Dokumentenaustausch soll es möglich sein, **Freigabe-Links** zu generieren, die ohne Login funktionieren. Ein solcher Link soll konfigurierbar sein: Der Ersteller legt fest, ob der Link nach einer bestimmten Zeit abläuft (Ablaufdatum), wie oft die Datei maximal heruntergeladen werden darf (Download-Limit), und ob der Link durch ein zusätzliches Passwort geschützt sein soll.

Für eine engere Zusammenarbeit — wenn ein externer Partner beispielsweise über mehrere Wochen regelmäßig auf bestimmte Dokumente zugreifen und diese kommentieren soll — wäre es wünschenswert, wenn der Manager dem Externen per **E-Mail-Einladung** einen temporären Gastzugang einrichten könnte. Der eingeladene Partner erhält eine E-Mail mit einem Einladungslink, über den er sich mit einer minimalen Registrierung (Name und Passwort) anmelden kann. Sein Zugang ist auf die freigegebenen Ordner beschränkt und kann jederzeit vom Manager widerrufen werden.

## Audit-Trail

Für die Compliance ist ein lückenloser **Audit-Trail** unverzichtbar. Jede relevante Aktion im System soll protokolliert werden: Wer hat wann welche Datei hochgeladen, heruntergeladen, angesehen, gelöscht oder umbenannt? Wer hat wem welche Berechtigung erteilt oder entzogen? Wer hat einen Freigabe-Link erstellt und wann wurde er genutzt? Wer hat sich wann angemeldet und abgemeldet?

Der Audit-Trail muss **unveränderlich** sein — das heißt, selbst ein Administrator darf bestehende Einträge nicht bearbeiten oder löschen können. Er soll lediglich die Einträge **lesen**, nach verschiedenen Kriterien **filtern** (nach Benutzer, nach Aktion, nach Zeitraum, nach Datei) und als **CSV exportieren** können. Technisch gesehen muss das Audit-Log als Append-Only-Struktur implementiert werden, die keine UPDATE- oder DELETE-Operationen auf bestehende Einträge zulässt.

Die Granularität des Audit-Trails soll fein genug sein, um bei einem Compliance-Audit nachweisen zu können, dass ein bestimmtes Dokument zu einem bestimmten Zeitpunkt nur von den dafür autorisierten Personen eingesehen werden konnte.

## Authentifizierung und Sicherheit

Die Sicherheit des Systems geht über die Zugriffskontrolle hinaus. Für die Authentifizierung ist eine Registrierung per E-Mail-Adresse und Passwort vorgesehen. Passwörter müssen serverseitig mit einem modernen Hashing-Algorithmus gespeichert werden — bcrypt oder Argon2, keinesfalls MD5 oder SHA256 ohne Salt. Es sollen Mindestanforderungen an die Passwortstärke durchgesetzt werden: Mindestens 8 Zeichen, mindestens ein Großbuchstabe, ein Kleinbuchstabe und eine Ziffer.

Zusätzlich zur Passwort-Authentifizierung wünschen wir uns eine optionale **Zwei-Faktor-Authentifizierung (2FA)** über TOTP — also die Möglichkeit, eine Authenticator-App wie Google Authenticator oder Authy zu verwenden. Bei der Aktivierung von 2FA soll dem Benutzer ein QR-Code angezeigt werden, den er mit seiner App scannt. Bei jedem Login gibt er dann zusätzlich zum Passwort den aktuellen 6-stelligen Code aus der App ein. 2FA soll für Administratoren verpflichtend und für alle anderen Rollen optional sein.

Als Schutz gegen Brute-Force-Angriffe soll ein **Rate Limiting** auf dem Login-Endpunkt implementiert werden: Nach fünf fehlgeschlagenen Login-Versuchen in Folge soll der Account für 15 Minuten gesperrt werden, und der Administrator soll darüber per E-Mail informiert werden.

Die hochgeladenen Dateien sollen **serverseitig verschlüsselt** gespeichert werden (AES-256 oder vergleichbar). Das Schlüsselmanagement soll so gestaltet sein, dass ein direkter Zugriff auf das Dateisystem (z.B. durch einen kompromittierten Server) nicht ausreicht, um die Dateien im Klartext zu lesen. Die Details des Schlüsselmanagements sollen im Systementwurf dokumentiert und begründet werden.

Das System muss gegen die gängigsten Angriffsvektoren geschützt sein, insbesondere Cross-Site Scripting (XSS) — relevant, da Benutzer Dateinamen und Kommentare eingeben —, Cross-Site Request Forgery (CSRF), SQL Injection und Directory Traversal bei Datei-Uploads. Die HTTPS-Nutzung soll in der Produktionsumgebung erzwungen werden.

## DSGVO und Datenschutz

Da das System personenbezogene Daten verarbeitet (E-Mail-Adressen, Benutzernamen, hochgeladene Dokumente, die personenbezogene Daten enthalten können), muss es **DSGVO-konform** sein. Konkret bedeutet das:

Jeder Benutzer soll das **Recht auf Auskunft** haben — er soll eine Übersicht aller über ihn gespeicherten Daten abrufen können. Darüber hinaus soll er sein **Recht auf Löschung** ausüben können: Wenn ein Benutzer die Löschung seines Accounts verlangt, müssen alle seine personenbezogenen Daten gelöscht werden — Profildaten, eigene Kommentare, Alert-Einstellungen, Sessions. Dateien, die der Benutzer hochgeladen hat, sollen allerdings nicht automatisch gelöscht werden, da sie im Unternehmenskontext gebraucht werden könnten — stattdessen soll der Ersteller-Name anonymisiert werden (z.B. durch „Gelöschter Benutzer"). Audit-Log-Einträge mit dem Benutzernamen sollen ebenfalls pseudonymisiert werden, da der Audit-Trail aus Compliance-Gründen nicht gelöscht werden darf.

Diese Abwägung zwischen Löschpflicht und Aufbewahrungspflicht ist bewusst als offener Punkt formuliert — das Entwicklungsteam soll hier im Pflichtenheft einen konkreten Vorschlag ausarbeiten und begründen.

## Gestaltung und Benutzeroberfläche

Die Oberfläche soll professionell, aufgeräumt und funktional sein — es handelt sich um ein Business-Tool, kein Consumer-Produkt. Die Navigation soll intuitiv sein, sodass auch Externe ohne Einführung verstehen, wie sie eine Datei herunterladen oder einen Kommentar hinterlassen. Das Branding von ERP_Champion (Logo, Unternehmensfarben) soll sichtbar sein, aber die Bedienbarkeit nicht einschränken.

Auf dem Desktop soll eine zweispaltige Ansicht verfügbar sein: links die Ordnerstruktur als Baum, rechts der Inhalt des ausgewählten Ordners mit Dateien, Vorschau und Kommentaren. Auf Tablets soll die Ordnerstruktur als ausklappbares Menü realisiert werden. Eine vollwertige Smartphone-Unterstützung ist nicht erforderlich, aber das System soll auf kleinen Bildschirmen zumindest grundlegend bedienbar sein (Dateien ansehen und herunterladen).

## Architektur

```
┌───────────────────────────────────────────────────────────────┐
│                     Browser (Client)                          │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │             SPA (Vue / React / etc.)                    │  │
│  │  ┌──────────────┐ ┌──────────────┐ ┌───────────────┐   │  │ 
│  │  │ Ordner-      │ │ Datei-       │ │ Admin-Panel   │   │  │ 
│  │  │ Navigation   │ │ Vorschau &   │ │ (Benutzer,    │   │  │ 
│  │  │ (Baum)       │ │ Kommentare   │ │  Audit-Log)   │   │  │ 
│  │  └──────────────┘ └──────────────┘ └───────────────┘   │  │ 
│  └────────────────────────┬────────────────────────────────┘  │
│                           │                                   │
│                       REST API                                │
└───────────────────────────┼───────────────────────────────────┘
                            │                                    
                            ▼                                    
┌───────────────────────────────────────────────────────────────┐
│                   Application Server                          │
│                                                               │
│  ┌──────────────────┐  ┌────────────────────────────────┐    │ 
│  │ REST Controller  │  │  Auth & Security Middleware    │    │ 
│  │ (Dateien, Ord-   │  │  (JWT/Session, 2FA-TOTP,      │    │  
│  │  ner, Kommentare │  │   Rate Limiting, RBAC)        │    │  
│  │  Sharing, Audit) │  │                               │    │  
│  └────────┬─────────┘  └────────────────────────────────┘    │ 
│           │                                                   │
│           ▼                                                   │
│  ┌─────────────────────────────────────────────────────────┐  │
│  │               Business Logic                            │  │
│  │  ┌──────────┐ ┌───────────┐ ┌────────────────┐         │  │ 
│  │  │ Datei-   │ │ Versions- │ │ Berechtigungs- │         │  │ 
│  │  │ Service  │ │ Service   │ │ Service (RBAC  │         │  │ 
│  │  │          │ │           │ │ + Vererbung)   │         │  │ 
│  │  └──────────┘ └───────────┘ └────────────────┘         │  │ 
│  │  ┌──────────┐ ┌───────────┐ ┌────────────────┐         │  │ 
│  │  │ Audit-   │ │ Sharing-  │ │ Notification-  │         │  │ 
│  │  │ Service  │ │ Service   │ │ Service        │         │  │ 
│  │  │ (Append- │ │ (Links,   │ │ (E-Mail,       │         │  │ 
│  │  │  Only)   │ │  Gäste)   │ │  @-Mentions)   │         │  │ 
│  │  └──────────┘ └───────────┘ └────────────────┘         │  │ 
│  └────────────────┬─────────────────┬──────────────────────┘  │
│                   │                 │                         │
│                   ▼                 ▼                         │
│  ┌─────────────────┐  ┌─────────────────────────┐            │ 
│  │  Datenbank      │  │  Verschlüsselter        │            │ 
│  │  (Benutzer,     │  │  Dateispeicher           │            │
│  │   Ordner,       │  │  (AES-256,              │            │ 
│  │   Metadaten,    │  │   Key Management)       │            │ 
│  │   Audit-Log,    │  │                         │            │ 
│  │   Kommentare)   │  │                         │            │ 
│  └─────────────────┘  └─────────────────────────┘            │ 
└───────────────────────────────────────────────────────────────┘
```

Die Architektur soll sich an unserem bestehenden Technologie-Stack orientieren, damit unsere hauseigenen Entwickler das System später weiterentwickeln und warten können. Besonders hervorzuheben sind zwei Aspekte: Erstens muss der **Audit-Service** so implementiert werden, dass er als unabhängige Komponente funktioniert und die Unveränderlichkeit der Einträge architektonisch gewährleistet — nicht nur durch Anwendungslogik, sondern idealerweise auch auf Datenbankebene (z.B. durch fehlende UPDATE/DELETE-Berechtigungen auf der Audit-Tabelle). Zweitens muss der **Berechtigungsservice** die Vererbungslogik effizient umsetzen, sodass die Berechtigungsprüfung bei tiefen Ordnerhierarchien nicht zu Performance-Problemen führt.

## Deployment und Betrieb

Das System soll mittels Docker containerisiert und per `docker-compose` startbar sein. Die Konfiguration — insbesondere Datenbankverbindung, SMTP-Zugangsdaten, Verschlüsselungsschlüssel und die TOTP-Konfiguration — soll über Umgebungsvariablen erfolgen. Eine verständliche Installationsanleitung ist Teil der erwarteten Liefergegenstände, ebenso wie Hinweise zur Ersteinrichtung (initiales Admin-Konto, Verschlüsselungsschlüssel-Generierung).

Für den E-Mail-Versand (Einladungen, @-Mentions, Brute-Force-Warnungen) soll SMTP verwendet werden. Für die Entwicklungs- und Testphase empfehlen wir Mailtrap oder einen ähnlichen Dienst.

## Qualität und Tests

Angesichts der sicherheitskritischen Natur des Systems erwarten wir eine besonders gründliche Test-Strategie. Die Zugriffskontrolle muss intensiv getestet werden — insbesondere die Vererbungs- und Überschreibungslogik für Ordnerberechtigungen. Typische Testszenarien wären: „Ein externer Gast hat Zugriff auf Ordner A, aber nicht auf den übergeordneten Ordner. Kann er trotzdem auf Ordner A zugreifen? Sieht er den übergeordneten Ordner in der Navigation?" Oder: „Ein Manager entzieht einem Mitarbeiter den Zugriff auf einen Unterordner, obwohl der Mitarbeiter Zugriff auf den Elternordner hat. Wird die Berechtigung korrekt überschrieben?"

Der Audit-Trail muss verifiziert werden: Wird jede Aktion korrekt protokolliert? Ist es tatsächlich unmöglich, Einträge zu verändern oder zu löschen — auch über direkte Datenbankzugriffe?

Die Verschlüsselung soll getestet werden: Sind die Dateien auf dem Dateisystem tatsächlich nicht lesbar, wenn man ohne den Schlüssel darauf zugreift?

Die allgemeine Code-Coverage soll mindestens 70% betragen. Die API soll über Swagger/OpenAPI dokumentiert sein.

Bugfixing und neue Features sollen später von unseren hauseigenen Entwicklern gemacht werden. Daher ist sauberer, gut strukturierter und testbarer Code wichtiger als eine maximale Feature-Menge. Die DSGVO-relevante Löschlogik muss korrekt und vollständig implementiert sein und darf keine verwaisten personenbezogenen Daten hinterlassen.

Um trotz des recht geringen Budgets ein passendes Produkt zu erstellen, sollen Werkstudenten dies komplett umsetzen. HR empfiehlt hier Studierende des Studienganges AI von der HS Offenburg, da nur diese über die fachliche Tiefe verfügen.

---

Projekt genehmigt:

Offenburg, den 23.02.2026

*\_\_\_\_Jack Berlinthal\_\_\_\_\_*

ERP_Champion GmbH
Dr. Jack Berlinthal
CEO / CIO ERP_Champion GmbH
