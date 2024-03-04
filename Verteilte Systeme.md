# Verteilte Systeme und Anwendungen


## Verteilte Systeme
- Ein Verteiltes System ist ein System in dem sich Hardware und Software Komponenten auf vernetzten Computern befinden und mit einander Komunizieren. 
- Ein Verbund von Knoten in einem Netz.
- Ein Protokoll definiert die Sprache und die Regeln der Komunikation
- Protokolle verbinden die Teilnehmer durch erfolgreiche Komunikation, sie sind der Kleber der das Internet zusammenhält.
- Die Kommunikationsinfrastrucktur eines VS bietet rudimentäre Kommunikationsdienste wie Verbindungs Auf- und Abbau, Datenpaketübertragung, Übertragungssicherheiten und Fehlerbehandlung auf Bitebene
  - Die Netzwerkschicht (IP) stellt logische Host zu Host Zustellung von Datagrammen zur Verfügung aber keinerlei Garantien
  - Die Transportschicht (TCP,Port) stellt verbindungsorientierte Pozess zu Prozess Zustellung von Segmenten zu Verfügung und garantiert:
    - Verlustfreien und fehlerfreien Datentransfer
    - in richtiger Reihenfolge der Pakete
    - mit Fluß- und Überlastkontrolle


### Verteilten Anwendung

- Anwendungslogik ist auf mehrere voneinander weitgehend unabhängige Anwendungskomponenten verteilt
- Komponenten verteilter Anwendungen können auf seperaten Knoten des verteilten Systems liegen
- Die Gesamtheit der Anwendungskomponenten erfüllt die Aufgabe der Anwendung
- Ein verteiltes System ist die Komunikationsinfrastruktur für Verteilte Anwendungen

### Verteilte Informations Systeme

- Informationssysteme sind Software intensiv
- Sie sind Datenorientiert und verwalten Daten und unterstützen den Anwender dabei
- Sie sind Interaktiv und verwenden Gui's
- Sie sind hochgradig nebenläufig
- Sie sind unternehmens Kritisch

**Weitere Verteilte Systeme**

- Eingebettet verteilte Systeme
- Mobile verteilte Systeme

### Middleware

- Setzt eine Anwendung auf einem verteilten System auf und implementiert selbst den Zugriff auf den Protokolstack spricht man von Netzwerkprogrammierung (mehr Einfluss, bessere Performance, Mehraufwand, anspruchsvoll)
- Liegt jedoch eine Schicht zwischen dem VS und der Verteilten Anwendung spricht man von einer Middleware
- Eine intelligente Programmierschnitstelle, die die Netzwerkschicht abstrahiert und Anwendugsablläufe unterstützt

### Kommunikationsmodelle

- Synchron - Blocking
  - Mehr Kontrolle und Genauigkeit beim Ablauf
- Asynchron - Non-Blocking
  - entkopelte Partner, parallele Ausführung, 

### Transparenzen Bei der Abstraktion

- Zugriffstransparenz, Lokal oder remote ist nicht sichtbar
- Ortstransparenz, physisch nicht lokalisierbar
- Nebenläufigkeitstransparenz, parallel Ausführung, Threads etc nicht sichtbar
- Fehlertransparenz, auftretend Fehler, Ausfälle werden vom Benutzer nicht wahrgenommen
- Replikationstransparenz, die Anwendung weis nicht wiviele Replikate existieren


