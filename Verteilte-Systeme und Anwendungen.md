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
- Liegt jedoch eine Schicht zwischen dem Verteilten System und der Verteilten Anwendung spricht man von einer Middleware
- Eine intelligente Programmierschnitstelle, die die Netzwerkschicht abstrahiert und Anwendugsablläufe unterstützt

### Kommunikationsmodelle

- Synchron - Blocking
  - Mehr Kontrolle und Genauigkeit beim Ablauf
- Asynchron - Non-Blocking
  - entkopelte Partner, parallele Ausführung,

### Transparenzen bei der Abstraktion

- Zugriffstransparenz, Lokal oder remote ist nicht sichtbar
- Ortstransparenz, physisch nicht lokalisierbar
- Nebenläufigkeitstransparenz, parallel Ausführung, Threads etc nicht sichtbar
- Fehlertransparenz, auftretend Fehler, Ausfälle werden vom Benutzer nicht wahrgenommen
- Replikationstransparenz, die Anwendung weis nicht wiviele Replikate existieren

### Zweck der Verteilung

- Gemeinsame Nutzung von Hardware
- Gemeinsame Nutzung von Funktionalität
- Gemeinsame Nutzung von Daten und Informationen

**Informationen beruhen auf Daten, beschreiben jedoch zusätzliche Zusammenhänge**

### Entwurf von Verteilten-Anwendungen

- Sicherheit, Perfomance, Verfügbarkeit
- Welche und wieviele Anwendungskomponenten wird es geben ?
- Wie werden die Aufgaben geeignet auf die Komponenten verteilt ?
- Wie werden die Anwendungskomponenten auf die Knoten des Verteilten Systems verteilt ?
- **Aufgabenteilung**
  - Präsentation, GUI, Nutzerschnittstellen
  - Anwendungslogik
  - Datenhaltung

## Architektur Modelle

- Beschreibt die Rollenverteilung der Komponenten in einer Verteilten Anwendung sowie die Beziehungen zwischen ihnen.

1. Client Server Modell:

   - kurzlebiger Clientprozess und langlebiger Serverprozess
   - **Kooperierende Sever**:
     - Anfragen werden vom einem Verbund von Servern bearbeitet, sichtbar oder transparent (DNS)
   - **Replizierte Server**:
     - Sichtbare oder Transparente Replikate um höhere Anfrageaufkommen abarbeiten zu können (bei hoher Verfügbarkeitsforderung)
     - Mirror Server, zur verteilung der Komunikationslast verteilt auf Kontinente, mit regelmäßigen Updates
     - Web Caching von CDN's - Content Distribution Networks
   - **Mobiler Code**:
     - Applets werden an Client gesendet, local ausgeführt und kommunizieren wenn nötig wieder mit den ursprungs- oder weiteren Servern

2. Peer to Peer Modell:

   - Komunikation gleichberechigter Prozesse
   - Laufen local, komunizieren nur bei Bedarf
   - Benötigen keinen zentralen Prozess

3. n-Tier Modelle:

   - Ergänzen das Client-Sever-Architekturmodell
   - Beschreiben die Verteilung der Anwendung auf die Knoten
   - Finden vor allem bei Informationssystemen Verwendung
   - ein Tier bezeichnet einen eigenständigen Prozessraum innerhalb der Anwendung
   - Tier-Grenzen treten an Rechnergrenzen oder local an Grenzen von Prozessräumen auf
   - 2-4 Tier ist gängig in der Praxis
   - Die gewälte Architektur kann sich erheblich auf die Eigenschaften eine Anwendung auswirken

### n-Tier Architekturen

**2-Tier-Architektur**
- Client-Tier übernimmt Präsentation
- Server-Tier übernimmt Datenhaltung
- Anwendungslogik ist auf Client, Server oder beide verteilt
- Schlecht skalierbar

**3-Tier-Architektur**
- Client-Tier, Präsentations
- Middle-Tier, Anwendungslogik
- Server-Tier, Datenhaltung
- Zentrale Verwaltung der Anwendungslogik
- Gut Skalierbar

**4- und mehr Tier-Architekturen**
- Unterscheiden sich nicht wesentlich von 3-Tier-Architekturen, sie verfeinern das Client-Server-Modell
- Neben der Middel-Tier werden weitere Tiers zwischen Client- und Server-Tier eingebaut
- Die Anwendungslogik wird auf weitere Tiers verteilt und bekommen optional eine eigene Bezeichnung

**Thin- und Fat-Clients**
- Thin-Client-Architektur, Client übernimmt nur Präsentation, wenig oder keine Anwendungslogik
- Fat-Client-Architektur, Client übernimmt Präsentation und teile der Anwendungslogik
- Die meisten 2-Tier-Architekturen sind auch Fat-Client-Architekturen

## Middelware

Eine Schicht zwischen Betriebsystem o. verteiltem System und Anwendungen

### Kommunikationsorientierte Middleware

orientiert sich auf die Bereitstellung von Komunikationsinfrastrucktur und Funktionalität für eine verteilte Anwendung wie z.B:

- Kommunikations-Protokolle z.B.: RPC (sync), RMI (sync), Message queing (async)
- Technik zur Datentransformation
- Mechanismen zur Fehrlerbahndlung und Fehlerbehebung (Prüfsummen, Sendungswiederholung, kontrolliertes Beenden)

### Anwendungsorientierte Middleware

Auch als Laufzeitumgebung oder Container bezeichnete Softwareschicht, die das Betriebssystem um Funktionalität erweitert die notwendig ist damit die Anwendung Hardware- und Betriebsystem-unabhängig funktionieren kann. Ihre Aufgaben können sein:

- Ressourcenverwaltung für Performance, Skalierbarkeit, Verfügbarkeit
  - Thread and Connection pooling
- Aufteilen des Hauptspeichers in Bereiche mit unterschiedlichen Sicherheitskonzepten
- Sicherheitsdienste wie: Authentifizeirung (Kennung und Passwort), Authorisierung (Zugriffsrechte), Vertraulichkeit (Abhörsicher, Verschlüsselt), Integrität (nicht manipulierte Daten)
- Verfügbarkeit durch Cluster-isierung
- Bereitstellen von Diensten

#### Cluster

Eine Reihe von Hard- und Software-Replikaten die nach Außen als Einheit auftreten

**fail-over Cluster**: Zur Ausfallvermeidung, springen nur bei Komponenten Ausfall ein
  - Tranparenter Wechsel möglich durch **Hot-Stand-By**
  - **cold-stand-by** benötigt Anlaufzeit der Komponenten

**load-balancing Cluster**: Zur Lastenverteilung, erhöhen Parallelität durch immer aktive Replikate

#### Dienste

Anwendungsorientierte Middelware bietet ihere Dienste impliziet über die Laufzeitumgebung an
Bieten Anwendungen klar definierte technische Funktionalität über Schnittstellen an, die bei bedarf genutzt werden können

- sind Anwendungs unabhängig, können beliebig viele sein
- Namensdienst zur Namensauflösung von Ressourcen (DNS) zb. Druckerzugang
- Sitzungsdienst (RAM intensiv bei vielen Benutzern)
- Transaktionsdienste für Multi-User CRUD-Operationen

#### Transaktionen

- Ermöglichen Datenkonsistenz trotz paralleler Zugriffe, 
- sie umfassen eine Reihe atomarer Aktionen für deren durchführung die gleichen Eigenschaften gelten
- z.B.: Drukerwarteschlangen, Datenbanken, Nachrichtenwarteschlangen
- Sie besitzen die **ACID** Eigenschaften
  - Atomarität/Atomicity: "Alles oder nichts" Alle aktionen werden Ausgeführt oder keine
  - Konsitenz/Consistency: Eine Transaktion bringt einen konsistenten Zustand immer einen neuen konsistenten Zustand
  - Isolation: Transaktion sind von einander isoliert und stören sich nicht gegenseitig
  - Dauerhaft/Durability: Der Zustand am Ende einer Transaktion wird dauerhaft festgeschrieben
