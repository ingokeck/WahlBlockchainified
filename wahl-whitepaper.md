# Whitepaper: Papierwahl blockchainunterstützt

Ingo R. Keck, Version 1.0 vom 2017-09-30

## Status Quo

Über Jahrzehnte hinweg haben sich freie und geheime Wahlen mit Wählerregister, Wahlzettel aus Papier und überwachter 
Auszählung als die beste Methode bestätigt, um ein korrektes und nachprüfbares Ergebnis zu erhalten.

Momentan läuft eine Wahl in Deutschland so ab:

* Jeder Wähler ist in einem Wahlregister vermerkt
* wenn der Wähler abstimmen will, wird ihm ein Wahlzettel aus Papier gegeben, den der Wähler im Geheimen ausfüllt.
* Der Wähler wird als "gewählt" in einem durchnummerierten Wahlregister (Papier) gezeichnet, dann darf er seinen gefalteten Stimmzettel in die Wahlurne werfen.
* Nach Ende des Abstimmungszeitraums werden die Urnen unter Aufsicht geöffnet und die enthaltenen Stimmen gezählt.
* Das Wahllokal kann sowohl währen der Abstimmung als auch während der Auszählung von Wahlbeobachtern observiert werden.
* Nachzählungen oder das mehrfache Auszählen der Stimmen zur Kontrolle ist problemlos möglich.
* Der lokale Wahlleiter bestätigt das lokale Ergebnis und gibt es zum zentralen Wahlleiter durch.
* Der zentrale Wahlleiter gibt das Gesamtergebnis und die lokalen Ergebnisse öffentlich bekannt.
* lokale Wahlleiter können jetzt nochmals nachprüfen, ob ihr lokales Ergebnis korrekt gezählt wurde. 
* Die Öffentlichkeit kann prüfen, ob das Gesamtergebnis korrekt aus den publizierten Einzelergebnissen berechnet wurde.

Prinzipiell ist dieses System sehr sicher konstruiert und umgesetzt. Die Möglichkeit zur nachträglichen Kontrolle ist 
an allen Stellen gegeben.

## Angriffsmöglichkeiten Status Quo

Folgende Angriffsmöglichkeiten sind denkbar:

* Das Wählerregister wird geändert. Größere Änderungen hier sind riskant für die Fälscher, denn die Absolutzahl der Wähler (Einwohner über 18) ist öffentlich bekannt und kann leicht nachkontrolliert werden. Die Zahl der abgegeben Stimmzettel muß zur Zahl der als gewählt markierten Personen passen. Tatsächliche Stimmabgaben können leicht durch anwesende Wahlbeobachter gezählt werden. Für Briefwahl müssen ausgefüllte Briefwahlanträge vorhanden sein (können ebenfalls nachkontrolliert werden).
* Wähler werden an der Stimmabgabe gehindert. Dies dürfte sehr schnell öffentlich  durch die gehinderten Wähler bekannt werden.
* Bei der Auszählung werden Stimmen falsch gezählt. Dies kann durch anwesende Wahlbeobachter und kontrollierte Nach- oder Zweitzählungen verhindert und aufgedeckt werden.
* Fälschung bei Übertragung zum zentralen Wahlleiter: Hier kann im Prinzip der lokale Wahlleiter sein übertragenes Ergebnis am Tag der Veröffentlichung nachkontrollieren. 
* Fälschung beim Berechnen des Gesamtergebnisses: Hier kann die Öffentlichkeit nachkontrollieren.

Zentrale digitale Angriffe auf das System sind dank der Basis auf Papier und der lokalen Kontrolle nicht möglich.

Tatsächlich sind die meisten bisher erkannten Wahlfälschungen gefälschte Stimmabgaben für echte Wähler (i.d.R. Briefwahl wie z.B. [1]), von denen der Fälscher sicher sein konnte, daß sie nicht zur Wahl gehen würden. Diese Fälschungen sind generell schwierig zu entdecken wenn sie im kleinen Umfang betrieben werden. 

Es gibt jedoch einen weiteren Schwachpunkt in diesem System: Die Weiterleitung der korrekten Ergebnisse von lokaler Ebene zum zentralen Wahlleiter. Hier können nur wenige Personen die Korrektheit nachkontrollieren (der lokale Wahlleiter und diejenigen Helfer / Beobachter, die die ganze Auszählung überwacht haben), die Kontrolle muß zeitlich versetzt zur Wahl erfolgen (Tage bzw. Wochen später) und es wird vermutlich als zusätzlichen Aufwand empfunden, der gerne unterbleibt.

Tatsächlich hat kürzlich eine Untersuchung des CCC aufgedeckt, daß gerade dieser letzte Schwachpunkt der Datenübertragung technisch ungesichert und damit leicht angreifbar erfolgt.[2] Daher schlage ich in diesem Artikel vor, an dieser Stelle transparente und sichere Technologien einzusetzen.

[1] Hessenschau: Kommunalwahl in Kelsterbach - Verdacht auf Wahlbetrug in mehr als 30 Fällen [http://www.hessenschau.de/politik/verdacht-auf-wahlbetrug-in-kelsterbach-in-ueber-30-faellen,kelsterbach-wahlbetrug-100.html](http://www.hessenschau.de/politik/verdacht-auf-wahlbetrug-in-kelsterbach-in-ueber-30-faellen,kelsterbach-wahlbetrug-100.html)

[2] Bericht: Analyse einer Wahlsoftware [https://ccc.de/system/uploads/230/original/PC-Wahl\_Bericht\_CCC.pdf](https://ccc.de/system/uploads/230/original/PC-Wahl_Bericht_CCC.pdf)

## Blockchain basierte Ergebnismeldung

Die vorgeschlagene Lösung behält den Ablauf der Wahl so wie bisher bei. Nur die Meldung des lokalen Ergebnisses an die Öffentlichkeit und an den zentralen Wahlleiter erfolgt durch ein öffentliches, transparentes und kryptographisch abgesichertes System, so daß Fälschungen leicht durch jedermann aufgedeckt werden können.

Die zentralen Anforderungen:

* Der lokale Wahlleiter meldet das lokale Ergebnis sofort nach der Auszählung öffentlich und kryptographisch abgesichert an den zentralen Wahlleiter
* lokale Helfer können das lokale Ergebnis bestätigen 
* der lokale Wahlleiter kann die lokale Meldung auch sofort kontrollieren und die Kontrolle bestätigen.

Diese Anforderungen werden durch folgendes System erfüllt:

* Vor der Wahl wird auf einer öffentlichen Blockchain die Liste der lokalen Wahlleiter und ihrer öffentlichen Schlüssel veröffentlicht (digital signiert vom zentralen Wahlleiter, dessen Identität und öffentlicher Schlüssel ebenfalls bekannt ist)
* Das lokale Ergebnis wird vom lokalen Wahlleiter digital signiert und auf einer öffentlichen Blockchain veröffentlicht (maschinenlesbar und mit abfotografierten Papierdokumenten).
* lokale Helfer können ihre signierte Bestätigung ebenfalls auf der selben Blockchain veröffentlichen.
* der lokale Wahlleiter kann die Bestätigung der Kontrolle des Ergebnisses von der Blockchain ebenfalls signieren und auf der Blockchain veröffentlichen
* die Öffentlichkeit kann die Blockchain lesen, die Signaturen kontrollieren und die korrekten Ergebnisse zum Gesamtergebnis zusammenfassen. 

In der Praxis wird man auf der Blockchain nicht die vollständigen Listen und Dokumente veröffentlichen, sondern stattdessen ihre digitalen Signaturen (z.B. SHA265) und die eigentlichen Dokumente anderswo unter ihren Signaturen bereitstellen. Hier bietet sich IPFS (ipfs.io) als einfache und sichere Lösung an.

## Praktische Umsetzung

Das System besteht aus zwei Programmen, die aus Gründen der Transparenz Open Source sein müssen: 

1. Ein lokaler, gesicherter Client ("Signierer") der folgendes erlaubt:
  * Erstellen eines passwortgeschützten Schlüsselpaares
  * Export des öffentlichen Schlüssels
  * Signieren von Ergebnismeldungen
  * Signieren von Fotos/Scans
  * Erstellen von signierten Transaktionen für die Blockchain, die die Referenzen auf die Daten enthalten
  * Erstellen von signierten Datenpakten zum Export, die vom zweiten Programm veröffentlicht werden.

Dieser lokale Client sollte nur auf einem abgesicherten Computer mit frisch installierten System ohne Zugang zum Internet betrieben werden. Der Datenaustausch erfolg nur in die Richtung Export für das zweite Programm. Es sollte nicht möglich sein den privaten Schlüssel zu exportieren.

2. Ein lokaler Client ("Melder") mit Internetzugang, der folgendes Erlaubt:
  * Empfang von signierten Datenpaketen vom Signierer-Progamm 
  * Test der Signaturen
  * Weiterleiten der Blockchain-Transaktionen aus diesen Datenpaketen
  * Publikation der signierten Dokumente aus diesem Signierer-Programm.
  * Lesen, Zugriff und Kontrolle der auf der Blockchain und in IPFS publizierten Daten, auch von anderen Wahllokalen

### Wahlablauf

1. Vor der Wahl erzeugt der zentrale Wahlleiter, jeder lokale Wahlleiter und auch lokale Wahlhelfer wenn gewünscht mit dem Signierer-Program ein Schlüsselpaar und melden den öffentlichen Schlüssel an den zentralen Wahlleiter. 
2. Der Zentrale Wahlleiter erstellt eine Liste aller öffentlichen Schlüssel, signiert sie mit seinem Signier-Programm und veröffentlicht sie mit dem Melder-Program auf IPFS und Blockchain
3. Jeder lokale Wahlleiter erstellt mit dem Signier-Programm eine Ergebnis-Meldung und packt Fotos der Papierdokumente dazu. Alle Dateien werden von ihm signiert.
4. jeder zentrale Wahlleiter publiziert diese Dateien mit dem Melder-Programm auf IPFS und der Blockchain
5. lokale Wahlhelfer können die Meldung wenige Minuten später mit ihrem Melder-Programm kontrollieren und die Kontrolle mit dem Signier-Program bestätigen (und anschließend mit dem Melder-Programm melden)
6. Jedermann kann mit einer lokalen Installation des Melder-Programmes oder anderer Programme die Blockchain überwachen und Ergebnisse lesen und kontrollieren.


## Erwartete Schwierigkeiten

Dieses Projekt weisst einige Schwierigkeiten auf:

### Benutzerfreundlichkeit

Die strikte Trennung zwischen Signierer- und Melder-System ist sicherheitstechnisch wünschenswert. Gleichzeitig ist aber eine Datenübertragung in eine Richtung notwendig. Diese Übertragung muß möglichst benutzerfreundlich erfolgen ohne daß dabei ein Sicherheitsrisiko besteht. Die Übertragenen Daten sind nicht zu groß, so daß man sie per Bluetooth oder USB-Stick übertragen könnte, wobei dabei wieder Sicherheitsrisiken entstehen. 

Gibt man die strikte Trennung auf, würde sich für das Signierer-Progamm eine Smartphone-App anbieten, da dort leicht Fotos gemacht werden können. Unter iOS könnte der private Schlüssel auch sicher im Telefon verwahrt werden. Unter Android wäre das in der Regel leider nicht möglich.

In jedem Fall ist Hilfe von UX-Experten nötig, um beide Programme einfach handhabbar zu machen.

### Finanzierung

Es gibt eine bestehende Software mit bekannten Sicherheitslücken für das Problem. Es ist unklar ob die öffentliche Hand per Vertrag gebunden ist, diese Software weiter zu zahlen und zu nutzen. Es ist vermutlich hochgradig unwahrscheinlich, daß sie bereit wäre, ein Open Source Projekt als Alternative finanziell zu unterstützen. Als beste Möglichkeit erscheint dem Autor, Finanzierung über Stiftungen oder Prototyp-Ausschreibungen zu suchen und, wenn die Lösung erst mal existiert, öffentlich Druck für eine Anwendung zu machen.

### Öffentlichkeitswirkung

Dieses Projekt wird nur dann öffentlich wahr genommen werden, wenn die Problematik in die Öffentlichkeit getragen wird. Dafür ist dedizierte Öffentlichkeitsarbeit nötig, die ebenfalls Kosten erzeugt.

### Sicherheit

Das Signierer-Programm ist die sicherheitstechnische Schwachstelle im System. Das Melder-Programm ist relativ unkritisch, denn es kann maximal Daten vom Signierer-Programm unterdrücken oder gefälscht erscheinen lassen. Beides würde jedoch schnell auffallen und würde das Endergebnis nicht beeinflussen.
