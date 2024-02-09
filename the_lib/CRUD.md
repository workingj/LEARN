# [CRUD](https://www.crowdstrike.de/cybersecurity-101/observability/crud/)

**CRUD** ist die Abkürzung für **CREATE** (Erstellen), **READ** (Lesen), **UPDATE** (Aktualisieren) und **DELETE** (Löschen). Dies sind die vier grundlegenden Operationen zur Erstellung und Verwaltung persistenter Datenelemente, die hauptsächlich in relationalen und NoSQL-Datenbanken zum Einsatz kommen.

Dieser Artikel beschreibt, wie CRUD-Operationen im Rahmen der Datenverarbeitung genutzt werden. Zudem erläutern wir die Probleme, die bei der Überwachung von Datenbanken auf Systemadministratoren und DevOps-Entwickler zukommen können.

## CRUD erklärt

Wie bereits erwähnt, werden CRUD-Operationen in persistenten Speicheranwendungen genutzt – also in Anwendungen, die ihre Daten nach dem Herunterfahren des Systems beibehalten. Sie unterscheiden sich von Operationen mit Daten, die in flüchtigen Speichern wie dem Arbeitsspeicher oder Cache-Dateien gespeichert sind.

CRUD wird häufig in Datenbankanwendungen wie relationalen Datenbankverwaltungssysteme (dt. für Relational Database Management Systems, RDBMS) (z. B. Oracle, [MySQL und PostgreSQL](https://www.crowdstrike.de/cybersecurity-101/observability/postgresql-vs-mysql/)) sowie NoSQL-Datenbanken (z. B. MongoDB, Apache Cassandra und AWS DynamoDB) genutzt.

Mitunter werden auch ähnliche Operationen wie CRUD an persistenten Datenstrukturen (z. B. Dateien) ausgeführt. So lässt sich beispielsweise ein Microsoft Word-Dokument über den Datei-Explorer erstellen, aktualisieren, lesen und löschen. Dateien sind jedoch nicht datensatzorientiert (bzw. im Fall von MongoDB oder Couchbase dokumentorientiert). Die CRUD-Terminologie bezieht sich speziell auf datensatzorientierte Operationen und nicht auf Flat-File-Operationen.

### CREATE (Erstellen)

Die **CREATE**\-Operation fügt einer Datenbank einen neuen Datensatz hinzu. In RDBMS werden einzelne Tabellenzeilen einer Datenbank als Datensatz bezeichnet, während Spalten Attribute oder Felder genannt werden. Die CREATE-Operation fügt einer Tabelle einen oder mehrere neue Datensätze mit unterschiedlichen Feldwerten hinzu.

Das gleiche Prinzip gilt für NoSQL-Datenbanken. Bei dokumentorientierten NoSQL-Datenbanken wird der Sammlung ein neues Dokument (z. B. ein JSON-formatiertes Dokument mit seinen Attributen) hinzugefügt, was einer RDBMS-Tabelle entspricht. Bei NoSQL-Datenbanken wie DynamoDB fügt die CREATE-Operation in ähnlicher Weise einer Tabelle ein Element (entspricht einem Datensatz) hinzu.

### READ (Lesen)

Die **READ**\-Operation gibt abhängig von den Suchkriterien Datensätze (oder Dokumente bzw. Elemente) aus einer Datenbanktabelle (oder einer Sammlung bzw. einem Bucket) zurück. Die Operation kann alle Datensätze und einzelne oder alle Felder zurückgeben.

### UDPATE (Aktualisieren)

Die **UPDATE**\-Operation dient dazu, bestehende Datensätze in der Datenbank zu ändern. Dies können beispielsweise Adressänderungen in einer Kundendatenbank oder Preisänderungen in einer Produktdatenbank sein. Ebenso wie READ-Operationen können UPDATE-Operationen je nach den gewählten Kriterien auf alle Datensätze oder nur auf einige wenige angewendet werden.

Die UPDATE-Operation kann Änderungen an einem einzelnen Feld oder mehreren Feldern des Datensatzes vornehmen und Persistenz herstellen. Wenn mehrere Felder aktualisiert werden sollen, stellt das Datenbanksystem sicher, dass entweder alle oder keine aktualisiert werden. Einige Big-Data-Systeme implementieren erst gar keine UPDATE-Operation, sondern erlauben nur eine CREATE-Operation mit Zeitstempel, wobei jedes Mal eine neue Version der Zeile hinzugefügt wird.

### DELETE (Löschen)

**DELETE**\-Operationen ermöglichen dem Benutzer, Datensätze aus der Datenbank zu entfernen. Beim endgültigen Löschen wird ein Datensatz vollständig entfernt, während er beim vorläufigen Löschen markiert, aber an Ort und Stelle belassen wird. Dies ist beispielsweise bei Gehaltsabrechnungen wichtig, wo die Personalakten noch aufbewahrt werden müssen, wenn Mitarbeiter das Unternehmen bereits verlassen haben.

## Wie werden CRUD-Operationen in einer Datenbank ausgeführt?

Bei RDBMS werden die CRUD-Operationen über SQL-Befehle (Structure Query Language) ausgeführt.

- Die INSERT-Anweisung wird zum Erstellen genutzt:

        INSERT INTO <table name> VALUES (field value 1, field value, 2…)

- Die SELECT-Anweisung wird zum Lesen genutzt:

        SELECT field 1, field 2, …FROM <table name> \[WHERE <condition>\]

- Die UPDATE-Anweisung wird zum Aktualisieren genutzt:

        UPDATE <table name> SET field1\=value1, field2\=value2,… \[WHERE <condition>\]

- Die DELETE-Anweisung wird zum Löschen genutzt:

        DELETE FROM <table name> \[WHERE <condition>\]

Abhängig von der Sprache der jeweiligen Datenbankplattform gibt es unterschiedliche CRUD-Operationen. Beispielsweise sieht Cassandra CQL der SQL-Sprache sehr ähnlich. Bei MongoDB hingegen werden die Operationen mithilfe integrierter Funktionen ausgeführt:

- CREATE wird über `db.collection.insertOne()` oder `db.collection.insertMany()` ausgeführt. Die erste Funktion fügt einer Datenbanksammlung ein Dokument hinzu, während die zweite mehrere Dokumente hinzufügt.
- READ wird über `db.collection.find()` oder `db.collection.findOne()` ausgeführt.
- UPDATE wird über `db.collection.updateOne()`, `db.collection.updateMany()` oder `db.collection.replaceOne()` ausgeführt.
- DELETE wird über
  `db.collection.deleteOne()` oder `db.collection.deleteMany()` ausgeführt.

Datenbankentwickler oder Datenbankadministratoren (DBAs) führen CRUD-Anweisungen für die Datenbank häufig manuell über ein Client-Tool aus. Allerdings werden diese Anweisungen im Produktiveinsatz meist in den Code der Programmiersprache eingebettet. Wenn das Programm ausgeführt wird, übernimmt die API für die Zieldatenbank die CRUD-Anweisung und übersetzt sie in die native Sprache der Datenbank.

Wenn beispielsweise Besucher eines Online-Shops den Registrierungsprozess starten, kann ein mit Python oder Java geschriebener Mikroservice die Eingabewerte lesen (z. B. Vorname, Nachname, E-Mail-Adresse, Postanschrift usw.) und dynamisch einen Oracle PL- bzw. SQL-Befehl erstellen. Die Anweisung wird dann an die Oracle-Treiberbibliothek geschickt, die sie auf die Datenbank anwendet.

## Beispiele für CRUD-Operationen

Spinnen wir das Beispiel des Online-Shops weiter.

- Wenn die Benutzer Kundendatensätze ERSTELLEN, können sie das bestehende Angebot durchLESEN, indem sie sich den Produktkatalog anschauen.
- Wenn sie eine Bestellung aufgeben, AKTUALISIERT das Backend-System den Bestand vorübergehend, um die geringere Anzahl verfügbarer Artikel widerzuspiegeln.
- Wenn sie den Artikel kaufen, wird die AKTUALISIERUNG endgültig und andere Benutzer, die die Anzahl der verfügbaren Artikel LESEN, können die Änderung sehen. Währenddessen ERSTELLT ein anderer Prozess einen Datensatz in der Datenbank des Versandunternehmens und benachrichtigt die Mitarbeiter über den Versandauftrag.
- Wenn die Benutzer einen Artikel aus dem Einkaufswagen entfernen, wird ein temporärer Datensatz, der der Tabelle „Verkäufe“ hinzugefügt wurde, GELÖSCHT.

Benutzer können bei einem Online-Reisebüro eine Buchungsanfrage ERSTELLEN, eine Übersicht der verfügbaren Flüge für die angeforderte Route LESEN und Käufe tätigen. Dadurch werden eine Liste der verfügbaren Sitzplätze für den Flug AKTUALISIERT und mehrere Datensätze in der Tabelle „Reiseplan“ ERSTELLT. Wenn die Benutzer die Sitzung auf halbem Weg beenden, werden alle Zeilen, die sich auf diese Transaktion beziehen, GELÖSCHT.

## Testen von CRUD-Operationen

Software-Operationen mit CRUD werden in der Regel durch Blackbox-Tests geprüft. Anstatt den Code zu analysieren, testen die Prüfer die Backend-Datenbank, indem sie bestimmte Operationen ausführen. Sie überprüfen damit, ob die beabsichtigten Änderungen vorgenommen bzw. die richtigen Daten zurückgegeben wurden. Diese Tests validieren alle CRUD-Operationen, die sich aus den zahlreichen möglichen Benutzerinteraktionen bei verschiedenen Szenarien ergeben.

## CRUD und Datenbank-Leistung

Ein effizientes Datenbankkonzept ist die Voraussetzung für die optimale Ausführung von CRUD-Operationen. Ohne ein gutes Konzept können CRUD-Operationen die Leistung einer Datenbank beeinträchtigen.

So müssen beispielsweise die Zeilen (und ihre zugehörigen Ressourcen wie Datenseiten oder Indizes) bei Operationen wie UPDATE oder DELETE gesperrt werden, sodass die Zeilen keinen anderen Prozessen oder Benutzern für CRUD-Operationen zur Verfügung stehen und die Integrität der Daten sichergestellt ist.

Datensätze dürfen während des Löschens nicht gelesen werden. Außerdem dürfen nicht mehrere Benutzer gleichzeitig in der Lage sein, einen einzelnen Datensatz zu aktualisieren. Andere Arten von Sperren wie gemeinsam genutzte Sperren ermöglichen gleichzeitige READ-Operationen. Die Sperren lassen sich auf der Ebene der Datenbank oder der Anweisung konfigurieren. Zudem gibt es verschiedene Arten von Sperren, die bestimmen, welche CRUD-Operationen zulässig sind und wie sich die jeweiligen CRUD-Operationen verhalten.

Die Art der Sperre und die Anzahl gleichzeitiger Sperren durch Benutzersitzungen wirken sich selbstverständlich auf die Leistung einer Datenbank aus. Ein Online-Shop, auf dem sich hunderte oder tausende Benutzer gleichzeitig aufhalten, muss parallel zahlreiche Sperren verwalten. Das kann zu einer langsamen Reaktionsgeschwindigkeit führen, da die Benutzer darauf warten müssen, dass Sperren aufgehoben werden.

Aufgrund dieses Leistungsproblems müssen Datenbankadministratoren sicherstellen, dass CRUD-Operationen so schnell wie möglich abgeschlossen werden. Dazu sind Abfrageoptimierungen nötig, die auf dem Feedback von Überwachungslösungen basieren. Die Lösungen können einen Überblick über aktuelle Datenbanksperren, Metriken und Protokolle geben, um Administratoren bei der Identifizierung möglicher Flaschenhälse zu helfen.
