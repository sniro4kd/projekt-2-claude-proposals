# Project Proposal: SignalScope - Echtzeit-Signalanalyse-Plattform

## Projekteckdaten

Die SensorTech Analytics GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung einer Signalanalyse-Plattform. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 35.000 Euro. Ansprechpartner ist Dr. Ing. Markus Reichert (CTO). Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von KI-Assistenten.

---

## 1. Ausgangssituation und Projektziel

Die SensorTech Analytics GmbH entwickelt Lösungen für industrielle Zustandsüberwachung, auch bekannt als Condition Monitoring. In modernen Fertigungsanlagen ist die frühzeitige Erkennung von Maschinenverschleiß ein entscheidender Faktor für die vorausschauende Instandhaltung. Vibrationssensoren an Motoren, Pumpen und Getrieben liefern kontinuierlich Daten, die analysiert werden müssen, um drohende Ausfälle rechtzeitig zu erkennen.

Aktuell fehlt der Firma eine flexible, webbasierte Plattform, die Vibrations- und Audiosignale erfassen, analysieren und visualisieren kann. Die bestehenden Lösungen sind entweder zu teuer, zu unflexibel oder nicht auf die spezifischen Anforderungen der Kunden zugeschnitten.

Das Ziel dieses Projekts ist die Entwicklung einer skalierbaren Echtzeit-Signalanalyse-Plattform. Diese soll Sensordaten entgegennehmen, mittels digitaler Signalverarbeitung analysieren, Anomalien erkennen und die Ergebnisse in einem übersichtlichen Dashboard für Ingenieure und Techniker darstellen.

---

## 2. Fachlicher Hintergrund

Die digitale Signalverarbeitung (DSP) bildet das Herzstück dieses Projekts. Vibrationssignale von Maschinen enthalten charakteristische Frequenzmuster, die auf den Zustand der Maschine schließen lassen. Ein gesundes Lager erzeugt ein anderes Frequenzspektrum als ein verschlissenes. Unwuchten in rotierenden Teilen zeigen sich als ausgeprägte Peaks bei der Drehfrequenz.

Die Fast Fourier Transformation (FFT) ist das wichtigste Werkzeug zur Analyse dieser Signale. Sie wandelt ein Zeitsignal in seine Frequenzbestandteile um. Für die kontinuierliche Überwachung werden Spektrogramme eingesetzt, die zeigen, wie sich das Frequenzspektrum über die Zeit verändert. Ergänzend kommen Filter zum Einsatz, um störende Frequenzbereiche auszublenden oder interessante Bereiche hervorzuheben.

Bei der Anomalieerkennung gibt es verschiedene Ansätze: einfache Schwellwertüberwachung für definierte Frequenzbänder, statistische Methoden wie Z-Score oder Interquartilsabstand, sowie maschinelles Lernen für komplexere Muster. Ein wichtiger Aspekt ist dabei die Baseline - das System muss lernen, was "normal" ist, bevor es Abweichungen erkennen kann.

---

## 3. Gewünschte Funktionalität

### Signalerfassung

Die Plattform soll Signaldaten aus verschiedenen Quellen entgegennehmen können. Primär werden Daten über eine REST-API eingespeist, aber auch der Import von Dateien (WAV für Audio, CSV für allgemeine Zeitreihen) soll möglich sein. Für die Entwicklung und Demonstration wird ein integrierter Signalgenerator benötigt, der realistische Testsignale erzeugen kann - von einfachen Sinustönen über Chirps bis hin zu simulierten Maschinensignalen mit typischen Fehlern.

Das System soll verschiedene Abtastraten unterstützen, typischerweise im Bereich von 1 kHz bis 48 kHz. Für Echtzeit-Anwendungen wäre eine WebSocket-Schnittstelle wünschenswert, über die Sensordaten kontinuierlich gestreamt werden können. Die Integration echter Sensoren via MQTT wäre ein nützliches Feature für fortgeschrittene Anwendungsfälle.

### Signalverarbeitung

Der Kern der Plattform ist die DSP-Engine. Diese muss die Fast Fourier Transformation implementieren, um Zeitsignale in den Frequenzbereich zu transformieren. Daraus lassen sich das Leistungsdichtespektrum und Spektrogramme berechnen. Die Implementierung verschiedener Fensterfunktionen (Hanning, Hamming, Blackman) ist essentiell, um Leckeffekte bei der FFT zu minimieren.

Filter sind ein weiterer wichtiger Bestandteil. FIR-Filter für Tiefpass, Hochpass und Bandpass sollten implementiert werden. IIR-Filter wie Butterworth oder Chebyshev wären eine sinnvolle Erweiterung. Für die Maschinendiagnose sind spezielle Analyseverfahren interessant: die Hüllkurvenanalyse zur Erkennung von Lagerschäden, die Cepstrum-Analyse für periodische Strukturen im Spektrum, und die Ordnungsanalyse für rotierende Maschinen mit variabler Drehzahl.

Statistische Kennwerte wie RMS (Effektivwert), Spitzenwert und Crest-Faktor sind grundlegende Indikatoren für den Maschinenzustand und sollten kontinuierlich berechnet werden.

### Anomalieerkennung

Das System soll Abweichungen vom Normalzustand erkennen und melden. Der einfachste Ansatz ist die Schwellwertüberwachung: für definierte Frequenzbänder werden Grenzwerte festgelegt, deren Überschreitung einen Alarm auslöst. Diese Grenzwerte sollten konfigurierbar sein.

Fortgeschrittenere Methoden nutzen statistische Verfahren, um zu erkennen, ob aktuelle Messwerte signifikant von historischen Werten abweichen. Noch anspruchsvoller sind ML-basierte Ansätze wie Isolation Forest, die komplexe Muster erkennen können, ohne dass explizite Regeln definiert werden müssen.

Ein wichtiges Feature ist die Trendanalyse: langsame Verschlechterungen über Wochen oder Monate zu erkennen, bevor ein kritischer Zustand erreicht wird. Das System sollte Baselines für den Normalzustand speichern und Veränderungen dokumentieren können.

### Visualisierung

Das Dashboard ist die Schnittstelle zum Benutzer und muss die komplexen Analyseergebnisse verständlich darstellen. Zeitsignale werden klassisch als Liniendiagramm dargestellt (Oszilloskop-Ansicht), Frequenzspektren als Balken- oder Liniendiagramm mit linearer oder logarithmischer Achse. Spektrogramme zeigen die zeitliche Entwicklung des Spektrums als Heatmap.

Alle Visualisierungen sollten Echtzeit-Updates unterstützen, idealerweise mit etwa 10 Updates pro Sekunde. Interaktive Funktionen wie Zoom, Pan und Cursor-Readout (Anzeige von Frequenz und Amplitude an der Cursorposition) erhöhen den Nutzen erheblich. Der Vergleich mehrerer Signale oder Messungen nebeneinander ist für die Diagnose hilfreich.

Alarme und Warnungen sollten visuell hervorgehoben werden. Eine Export-Funktion für Screenshots (PNG) und Rohdaten (CSV) rundet das Dashboard ab.

### Datenverwaltung

Messdaten müssen gespeichert und organisiert werden können. Jede Messung sollte mit Metadaten versehen werden können: welche Maschine, welcher Messpunkt, wann gemessen, unter welchen Betriebsbedingungen. Historische Daten sind für die Trendanalyse essentiell und sollten über längere Zeiträume (mindestens 90 Tage, besser ein Jahr) vorgehalten werden.

Die Möglichkeit, Messungen zu annotieren (Kommentare, Tags wie "Normalzustand" oder "nach Wartung") unterstützt die spätere Auswertung.

---

## 4. Technische Rahmenbedingungen

Das Backend soll in C# mit ASP.NET Core 9 entwickelt werden, da dies dem Firmenstandard entspricht. Für die numerischen Berechnungen steht die Bibliothek MathNet.Numerics zur Verfügung, eigene Implementierungen sind aber ausdrücklich erwünscht, um das Verständnis zu vertiefen.

Für die asynchrone Verarbeitung von Analyseaufträgen wird eine Message Queue (RabbitMQ) oder ein Background-Job-System (Hangfire) benötigt. Die Speicherung von Zeitreihendaten erfolgt in einer spezialisierten Datenbank wie InfluxDB oder TimescaleDB, während Konfigurationen und Metadaten in PostgreSQL abgelegt werden. Redis dient als Cache für häufig abgefragte Berechnungsergebnisse.

Das Frontend wird mit Vue.js 3 entwickelt, für die Visualisierungen kommen Chart.js oder D3.js zum Einsatz. Die Echtzeit-Kommunikation zwischen Server und Client erfolgt über SignalR (WebSocket).

Das gesamte System muss via Docker und Docker Compose deploybar sein.

---

## 5. Qualitätsanforderungen

Die DSP-Algorithmen müssen numerisch korrekt sein. Als Referenz dienen etablierte Implementierungen in NumPy/SciPy. Die Ergebnisse einer FFT mit 8192 Punkten sollten mit der Referenz übereinstimmen, die Berechnung sollte unter 50ms dauern.

Das Dashboard muss flüssige Echtzeit-Updates mit mindestens 10 Hz ermöglichen. Das System soll 20 gleichzeitige Signalstreams verarbeiten können. Die Berechnung eines Spektrogramms für eine Sekunde Audio sollte unter 200ms abgeschlossen sein.

Die Architektur muss horizontal skalierbar sein, sodass bei steigender Last weitere Worker hinzugefügt werden können.

---

## 6. Dokumentations- und Testanforderungen

Das Projekt folgt dem V-Modell. Neben den üblichen Dokumenten (Lastenheft, Pflichtenheft, High-Level- und Low-Level-Design, ADRs) wird eine spezielle DSP-Dokumentation verlangt, die die mathematischen Grundlagen der implementierten Algorithmen erklärt.

Für die Validierung der DSP-Algorithmen muss eine Suite von Referenz-Testsignalen erstellt werden: Sinustöne bekannter Frequenz, Chirps, weißes Rauschen, Impulse, AM-modulierte Signale, Überlagerungen mehrerer Frequenzen, und simulierte Maschinenfehler. Für jedes Testsignal muss das erwartete Analyseergebnis dokumentiert und gegen die Referenzimplementierung validiert werden.

Die Code-Coverage soll mindestens 80% betragen. Alle DSP-Algorithmen benötigen besonders sorgfältige Reviews durch mindestens zwei Personen.

---

## 7. Forschungskomponente

Als Research-Komponente soll das Team einen systematischen Vergleich verschiedener Algorithmen durchführen. Dies umfasst den Vergleich verschiedener FFT-Implementierungen (Radix-2, Bluestein, Bibliotheksimplementierung), die Analyse verschiedener Fensterfunktionen hinsichtlich Frequenzauflösung und spektralem Leckeffekt, sowie den Vergleich von Anomalieerkennungsverfahren (schwellwertbasiert, statistisch, ML-basiert) mit Precision/Recall-Metriken.

Das Ergebnis ist ein Research-Report von mindestens 12 Seiten mit Benchmark-Ergebnissen, Grafiken und Empfehlungen für den Produktiveinsatz.

---

## 8. Optionale Erweiterungen

Für Bonuspunkte können Teams echte Sensorhardware integrieren: MEMS-Beschleunigungssensoren wie ADXL345 oder MPU6050, USB-Mikrofone für Audioanalyse, oder einen ESP32 als Datenerfassungseinheit. Die Hardware wird bei Bedarf gestellt.

---

Offenburg, den 14.01.2026

Dr. Ing. Klaus Brenner
CTO SensorTech Analytics GmbH
