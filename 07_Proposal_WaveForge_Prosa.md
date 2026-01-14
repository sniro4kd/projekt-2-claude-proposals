# Project Proposal: WaveForge - Interaktive DSP-Lern- und Simulationsplattform

## Projekteckdaten

Die EduSignal Technologies GmbH beauftragt ein Team von 6-7 Studierenden mit der Entwicklung einer interaktiven DSP-Lernplattform. Das Projekt läuft von März bis Juli 2026 mit einem Budget von 35.000 Euro. Ansprechpartner ist Prof. Dr. Ing. Andreas Körner. Der geschätzte Aufwand pro Person beträgt 30-40 Stunden unter Einsatz von KI-Assistenten.

---

## 1. Ausgangssituation und Projektziel

Die EduSignal Technologies GmbH entwickelt Lernsoftware für technische Hochschulen. In der Lehre der digitalen Signalverarbeitung besteht eine Lücke zwischen theoretischen Vorlesungsinhalten und praktischer Anwendung. Studierende lernen Formeln und Konzepte, haben aber selten die Möglichkeit, diese interaktiv zu erleben und zu experimentieren.

Bestehende Tools wie MATLAB sind mächtig, aber teuer und haben eine steile Lernkurve. Webbasierte Alternativen sind oft zu simpel oder nicht auf die Lehre zugeschnitten. Die Firma sieht einen wachsenden Markt für moderne, browserbasierte Lernwerkzeuge.

Das Ziel dieses Projekts ist die Entwicklung einer webbasierten DSP-Simulationsplattform, die Studierenden ermöglicht, Konzepte der digitalen Signalverarbeitung interaktiv zu erkunden. Parameter können in Echtzeit verändert werden, und die Auswirkungen sind sofort sichtbar. Als Bonus soll die Plattform C-Code für Embedded-Systeme exportieren können, um die Brücke zur praktischen Anwendung zu schlagen.

---

## 2. Fachlicher Hintergrund

Die digitale Signalverarbeitung umfasst ein breites Spektrum an Themen. Im Zentrum stehen Filter, die unerwünschte Frequenzanteile aus Signalen entfernen. FIR-Filter (Finite Impulse Response) sind stabil und haben eine lineare Phase, benötigen aber viele Koeffizienten für steile Flanken. IIR-Filter (Infinite Impulse Response) erreichen die gleiche Dämpfung mit weniger Koeffizienten, können aber instabil werden und haben nichtlineare Phasenverläufe.

Beim Filterdesign gibt es verschiedene Methoden. Die Window-Methode ist am einfachsten zu verstehen: man startet mit einem idealen Filter und multipliziert mit einer Fensterfunktion. Die Wahl des Fensters (Rechteck, Hanning, Hamming, Kaiser) beeinflusst das Ergebnis. Der Parks-McClellan-Algorithmus findet optimale Filterkoeffizienten nach dem Minimax-Kriterium. Bei IIR-Filtern unterscheidet man Butterworth (maximal flacher Frequenzgang), Chebyshev (erlaubt Ripple für steilere Flanken) und elliptische Filter (steilste Flanken, Ripple in beiden Bändern).

Modulationsverfahren sind ein weiteres zentrales Thema. Bei der analogen Modulation unterscheidet man Amplitudenmodulation (AM), bei der die Amplitude des Trägers variiert wird, und Frequenzmodulation (FM), bei der die Frequenz variiert wird. Digitale Modulationsverfahren wie ASK, FSK und PSK übertragen diskrete Symbole. QAM kombiniert Amplituden- und Phasenmodulation für höhere Datenraten. Die Visualisierung durch Konstellationsdiagramme und Augendiagramme hilft beim Verständnis dieser Verfahren.

---

## 3. Gewünschte Funktionalität

### Signalgenerator

Die Plattform benötigt einen vielseitigen Signalgenerator als Ausgangspunkt für alle Experimente. Grundlegende Signalformen sind Sinus, Rechteck, Dreieck und Sägezahn mit konfigurierbarer Frequenz und Amplitude. Rauschsignale (weiß und rosa) sind für realistische Tests unerlässlich. Chirp-Signale mit linear ansteigender Frequenz eignen sich zur Analyse von Filterverhalten über einen breiten Frequenzbereich.

Signale sollten addiert und multipliziert werden können, um komplexere Szenarien zu erzeugen. Der Upload eigener Audiodateien erweitert die Experimentierfreudigkeit, und die Möglichkeit, das Mikrofon des Computers zu nutzen, macht das Lernerlebnis noch greifbarer.

### Filterdesign-Modul

Das Herzstück der Plattform ist das interaktive Filterdesign. Der Benutzer wählt einen Filtertyp (Tiefpass, Hochpass, Bandpass, Bandsperre), gibt die gewünschten Parameter an (Grenzfrequenzen, Ordnung, Dämpfung) und sieht sofort das Ergebnis.

Die Visualisierung umfasst den Frequenzgang (Betrag und Phase), die Impuls- und Sprungantwort, sowie das Pol-Nullstellen-Diagramm in der komplexen Ebene. Idealerweise kann der Benutzer Pole und Nullstellen auch direkt im Diagramm verschieben und sieht die Auswirkungen auf den Frequenzgang.

Die Filterkoeffizienten werden angezeigt und können exportiert werden. Verschiedene Designmethoden sollten verfügbar sein: die Window-Methode mit verschiedenen Fensterfunktionen für FIR-Filter, sowie Butterworth und Chebyshev für IIR-Filter. Fortgeschrittene Methoden wie Parks-McClellan oder elliptische Filter wären wünschenswerte Erweiterungen.

### Modulationsverfahren

Ein eigenes Modul widmet sich der Simulation von Modulationsverfahren. Für jedes Verfahren werden Modulator und Demodulator implementiert, sodass der gesamte Übertragungsweg simuliert werden kann.

Analoge Verfahren umfassen AM und FM. Der Benutzer kann Trägerfrequenz, Modulationsindex und Nachrichtensignal wählen und sieht das modulierte Signal sowohl im Zeitbereich als auch im Frequenzspektrum.

Digitale Verfahren wie ASK, FSK und PSK zeigen, wie binäre Daten übertragen werden. QAM mit verschiedenen Konstellationen (4-QAM, 16-QAM) demonstriert höhere spektrale Effizienz. Konstellationsdiagramme zeigen die Symbole in der komplexen Ebene, Augendiagramme visualisieren die Intersymbolinterferenz.

Die Simulation von Rauscheinfluss und die Darstellung von Bitfehlerraten-Kurven wären fortgeschrittene Features, die das Verständnis vertiefen.

### Visualisierung

Alle Signale werden in Echtzeit visualisiert, mit flüssigen Updates bei Parameteränderungen. Die Darstellung umfasst Zeitbereich (wie ein Oszilloskop), Frequenzspektrum (FFT) und Spektrogramm (Zeit-Frequenz-Darstellung).

Interaktive Funktionen wie Zoom, Pan und Cursor-Readout sind essentiell für detaillierte Analysen. Mehrere Signale sollten überlagert darstellbar sein, um Vergleiche zu ermöglichen. Eine Split-View mit Zeit- und Frequenzdarstellung nebeneinander ist besonders praktisch.

Die Möglichkeit, Audiowiedergabe für die erzeugten Signale zu aktivieren, macht abstrakte Konzepte hörbar und damit greifbarer.

### Code-Generator für Embedded-Systeme

Ein besonderes Feature ist der Export von C-Code für Embedded-Targets. Filter, die im Tool designt wurden, können als C-Arrays (Koeffizienten) und Funktionen (Filteralgorithmus) exportiert werden.

Der generierte Code sollte verschiedene Formate unterstützen: Floating-Point für Desktop-Anwendungen, Fixed-Point (Q15, Q31) für ressourcenbeschränkte Mikrocontroller. Idealerweise ist der Code kompatibel mit der ARM CMSIS-DSP Bibliothek, die auf vielen Cortex-M Prozessoren verfügbar ist.

Header-Dateien mit Konfigurationsparametern runden den Export ab. Auch Export nach Python/NumPy oder MATLAB wäre für viele Benutzer nützlich.

### Lernmodus

Die Plattform soll nicht nur ein Werkzeug sein, sondern auch lehren. Zu jedem Modul werden erklärende Texte angezeigt, die die mathematischen Hintergründe erläutern. Formeln werden mit LaTeX schön dargestellt.

Vordefinierte Beispiel-Szenarien führen durch typische Anwendungsfälle: "Design eines Tiefpassfilters für Audio", "Simulation einer FM-Radioübertragung", "Vergleich verschiedener Fensterfunktionen". Interaktive Tutorials könnten die Benutzer Schritt für Schritt durch komplexere Themen führen.

---

## 4. Technische Rahmenbedingungen

Das Backend wird in C# mit ASP.NET Core 9 entwickelt. Für numerisch aufwändige Algorithmen (insbesondere Filterdesign-Methoden wie Parks-McClellan) wird das Backend genutzt, ergänzt durch MathNet.Numerics.

Das Frontend basiert auf Vue.js 3 mit TypeScript. Die DSP-Engine für einfache Berechnungen (FFT, Filter) läuft direkt im Browser für minimale Latenz. Die Web Audio API ermöglicht Audiowiedergabe und Mikrofonzugriff. Für rechenintensive Aufgaben könnte WebAssembly zum Einsatz kommen.

Die Visualisierung nutzt D3.js für komplexe Diagramme (Pol-Nullstellen) und Canvas API für performante Echtzeit-Darstellungen. Formeln werden mit KaTeX oder MathJax gerendert.

Benutzerprojekte und Presets werden in PostgreSQL gespeichert. Das gesamte System wird via Docker bereitgestellt.

---

## 5. Qualitätsanforderungen

Die Visualisierung muss flüssig sein, mit mindestens 30 FPS bei Parameteränderungen. Filterdesign-Berechnungen sollten unter 100ms abgeschlossen sein, FFT mit 4096 Punkten unter 20ms im Browser.

Die numerische Korrektheit ist kritisch. Alle Filterkoeffizienten müssen mit Referenzimplementierungen (SciPy) übereinstimmen. Der generierte C-Code muss kompilieren und korrekte Ergebnisse liefern.

Die Benutzeroberfläche soll intuitiv bedienbar sein, ohne Handbuch. Die Plattform muss im Browser laufen, ohne Installation, und sowohl auf Desktop als auch auf Tablets funktionieren.

---

## 6. Dokumentations- und Testanforderungen

Neben der Standard-V-Modell-Dokumentation werden zwei spezielle Dokumente verlangt: eine Filterdesign-Dokumentation, die alle implementierten Algorithmen mathematisch beschreibt, und eine Modulations-Dokumentation für alle Modulationsverfahren.

Alle Filter müssen gegen Referenzimplementierungen validiert werden. Die Koeffizienten eines FIR-Tiefpasses mit der Window-Methode müssen mit SciPy's firwin-Funktion übereinstimmen. Entsprechend für IIR-Filter mit butter und cheby1.

Der generierte C-Code muss auf mindestens einem Embedded-Target validiert werden: er muss kompilieren (GCC ARM), numerisch korrekte Ergebnisse liefern, und echtzeitfähig auf einem Cortex-M4 sein.

Usability-Tests mit mindestens 5 Testpersonen (idealerweise Studierende) sollen die Bedienbarkeit evaluieren.

Ein didaktisches Konzept dokumentiert die Lernziele pro Modul, die Progression von einfach zu komplex, und welche Visualisierungen welche Konzepte am besten vermitteln.

---

## 7. Forschungskomponente

Das Team soll einen systematischen Vergleich von Filterdesign-Methoden durchführen. Bei FIR-Filtern werden Window-Methode (mit verschiedenen Fenstern), Frequenz-Sampling und Parks-McClellan verglichen. Bei IIR-Filtern Butterworth, Chebyshev und elliptische Filter.

Vergleichskriterien sind: benötigte Filterordnung für gleiche Spezifikation, Gruppenlaufzeit, Implementierungsaufwand, und numerische Stabilität.

Das Ergebnis ist ein Research-Report von mindestens 12 Seiten, ein interaktiver Vergleich im Tool selbst, und ein Empfehlungs-Guide, der Anwendern hilft, die richtige Methode für ihren Anwendungsfall zu wählen.

---

## 8. Optionale Erweiterungen

Für Bonuspunkte kann das Team den generierten C-Code auf einem echten Mikrocontroller (STM32 oder ESP32) validieren. Eine Live-Verbindung via USB würde den Vergleich zwischen Simulation und realer Hardware ermöglichen. Die Hardware wird bei Bedarf gestellt.

---

Offenburg, den 14.01.2026

Prof. Dr. Ing. Heinrich Wagner
Geschäftsführer EduSignal Technologies GmbH
