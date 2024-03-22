## 1 Aufbau von Computersystemen

Der Zweck eines Computers ist es Daten zu verarbeiten

### Bytereihenfolge (Endianness)

- Leserichtung von Zahlen: von Links (MSB) nach Rechts (LSB)

```text
1234
1000 1 = Most significant BYTE
 200 2
  30 3
   4 4 = Least significant BYTE
```

- **Little-Endian** Legen höherwertige Bytes auf höhere Speicheradressen, beginnt mit dem LSB im Speicher (beginnt am kleinen Ende)
- **Big-Endian** Legen höherwertige bytes auf niedrigere Speicheradressen, beginnt mit dem MSB im Speicher (beginnt am großen Ende)

```
32-Bit Integer (4 Bytes hex) Representation im Speicher
╔══╦══╦══╦══╗                         ╔══╦══╦══╦══╗
║0D║0C║0B║0A║            I            ║0D║0C║0B║0A║
╚╤═╩╤═╩╤═╩╤═╝      (LE)  N  (BE)      ╚═╤╩═╤╩═╤╩═╤╝
 │  │  │  │ LSB    ┣━━┫     ┣━━┫    LSB │  │  │  │
 │  │  │  └────> 0 ┃0A┃  M  ┃0D┃ 0 <────┘  │  │  │
 │  │  │           ┣━━┫  E  ┣━━┫           │  │  │
 │  │  └───────> 1 ┃0B┃  M  ┃0C┃ 1 <───────┘  │  │
 │  │              ┣━━┫  O  ┣━━┫              │  │
 │  └──────────> 2 ┃0C┃  R  ┃0B┃ 2 <──────────┘  │
 │          MSB    ┣━━┫  Y  ┣━━┫    MSB          │
 └─────────────> 3 ┃0D┃     ┃0A┃ 3 <─────────────┘
                   ┣━━┫     ┣━━┫ 
   Little-Endian                    Big-Endian
```

Little Endian und Big Endian bezeichnen die Bytereihenfolge von Daten im Speicher. **Von rechts nach links gelesen enden sie auf die jeweils größte (BE) oder kleinste (LE) Stelle.** Beim übertragen von Daten über das Netzwerk von Rechnern mit unterschiedlichen Bytereihenfogen, kommt es hierbei zu Problemen. Den Serialisierung und Deserialisierung unterscheiden sich. LE `11` würde zu BE `184549376`, BE `6` zu LE `100663296`
Die Bits in einem Byte sind Standartmäßig immer in Big-Endian Format.  
Das **Least-Significant-Bit** ist ganz "Rechts".
Big Endian wirt auch Network-Byte-Order genannt

- **Little-Endian**: von rechts nach links, Intel-Familie
  
  ```
               32 Bit Word - Little Endian
              ═════════════════════════════
  Byte        3        2        1        0
  Bits       32       24       16        8 
  Daten   ┏━━━━━━━━┳━━━━━━━━┳━━━━━━━━┳━━━━━━━━┓ Adresse
  Zahl 6  ┃00000110┃00000000┃00000000┃00000000┃    0
          ┣━━━━━━━━╋━━━━━━━━╋━━━━━━━━╋━━━━━━━━┫
  Zahl 11 ┃00001011┃00000000┃00000000┃00000000┃    4
          ┣━━━━━━━━╋━━━━━━━━╋━━━━━━━━╋━━━━━━━━┫
  "ABCD"  ┃01000100┃01000011┃01000010┃01000001┃    8
          ┣━━━━━━━━╋━━━━━━━━╋━━━━━━━━╋━━━━━━━━┫
          ┃   D    ┃   C    ┃   B    ┃   A    ┃
          ┗━━━━━━━━┻━━━━━━━━┻━━━━━━━━┻━━━━━━━━┛
  ```

- **Big-Endian**: von links nach rechts, SPARC, IBM-Großrechner
  
```
                32 Bit Word - Big Endian
               ══════════════════════════
  Byte        0        1        2        3
  Bits        8       16       24       32 
  Adresse ┏━━━━━━━━┳━━━━━━━━┳━━━━━━━━┳━━━━━━━━┓ Daten
     0    ┃00000000┃00000000┃00000000┃00000110┃ Zahl 6
          ┣━━━━━━━━╋━━━━━━━━╋━━━━━━━━╋━━━━━━━━┫
     4    ┃00000000┃00000000┃00000000┃00001011┃ Zahl 11
          ┣━━━━━━━━╋━━━━━━━━╋━━━━━━━━╋━━━━━━━━┫
     8    ┃01000001┃01000010┃01000011┃01000100┃ "ABCD"
          ┣━━━━━━━━╋━━━━━━━━╋━━━━━━━━╋━━━━━━━━┫
          ┃   A    ┃   B    ┃   C    ┃   D    ┃
          ┗━━━━━━━━┻━━━━━━━━┻━━━━━━━━┻━━━━━━━━┛
  ```

### GPU's VS CPU's

- GPU's sind optimiert für hohen Durchsatz und spezialisiert auf parallelisierbare Workloads, Transitoren werden für mehr Kerne verwendet
  
  - Hiding Latency durch ausführen wartender Threads
  
  - SIMD, eine Instruktion wird gleichzeitig auf 32 Daten-Ströme ausgeführt
  
  - Compute Shader werden in eine Zwischensprache übersetzt (IR) und dann vom Treiber für den Grafikchip Compiliert

- CPU's sind optimiert für Pipelining, Branchprediction, Register renaming, die Transitoren werden für Technologimplementationen verwendet

## 3 Die ISA (Instruction Set Architecture)

Definiert <u>Maschienenbefehle</u>, <u>Datentypen</u> und Register, <u>sowie</u> das Speichermodell des <u>Prozessors</u>.

### Eine Schnittstelle

- Schnittstelle zwischen Mikroarchitektur und Betriebsystemebene

- Schnitstelle zwischen Soft und Hardware, das Hardware Interface

- Definiert die Schnittstelle zwischen Kompiler und Hardware, es ist die Sprache die beide verstehen müssen

- Wird durch Mikroprogramme oder die Hardware direkt ausgeführt

- Die Microarchitektur ist die Hardware implementation der ISA, sie bestimmt den Aufbau der ISA und umgekehrt

### Entwicklung

- Wird im Idealfall von Hardware-Architekten zusammen mit Compiler-Entwicklern entworfen um die angestrebten Merkmal auf beiden Seiten zu garantieren.

- Abwärtskompatibilität ist oft ein bestimmender Faktor

- Eine gute ISA lässt sich effizient in vorhandene und zukünftige Technologie implementieren, lebt damit über viele Generationen hinweg

- Ein gute ISA bietet einem Compiler, Regelmäßigkeit und Vollständigkeit im Bereich von begrenzten Optionen zwischen denen der Compiler wählen eine wählen muss.

- Die ISA wird danach definiert wie sich die Maschine dem Programmierer darstellt. 

### Eigenschaften

- Die Beschaffenheit der Mikroarchitektur ist auf der ISA-Ebene für den Compiler-Entwickler bis auf das Leistungsverhalten nicht sichtbar.

- Die meisten Maschinen haben hab zwei Modi, 
  
  - **Kernel-Modus**: Für das OS vorgesehen, Ausführung aller Befehle möglich
  
  - **User-Modus**: für Anwendungsprogramme, unterbindet Ausführung kritischer best. kritischer Befehle

- Die Effiziens einer ISA hängt stark von der Technologie ab mit der der Rechner impementiert wird. (zB. Ausführungsgeschwindigkeit vs Befehlslänge, Speicheruflösung, Eweiterbarkeit vs Bandbreite der Speicherzugriffe)

#### Speichermodelle

Das Speichermodell in der ISA umfasst die Größe einer Speicherzelle, die Breite der  dessen, die Anordnung von Bytes in Datenworten, deren  Ausrichtung im Adressraum  und die Semantik aufeinanderfolgender Speicherzugriffe.

- Speicher wird in Zellen mit aufeinander folgenden Adressen aufgeteilt

- 8-Bit ist die zz. übliche Zellgröße, ein Byte (Oktett)

- Bytes gruppiert man meist zu 4-Byte-Wörtern (32 Bit) oder 8-Byte-Wörtern (64 Bit), wobei es Befehle gibt die ganze Wörter manipulieren

- Viele Architekturen verlangen aus Effizienz Gründen das Ausrichten der Wörter an ihren natürlichen Grenzen (z.B: 4-Byte an Adresse 0,4,8... nicht aber 2,6,10... )

- **Adressräume** auf der ISA-Ebene
  
  - **Linear**: Sehr verbreitet, 2³² -1 o. 2^64 -1, unsicher, potentielle Fehlerquelle durch überschreiben von Befehlen
  - **Geteilt**: Daten und Befehle getrennt, sicherer, kein überschreiben von Befehlen möglich, kleinerer Adressraum

- **Speichersemantik** extreme in Bezug auf *WAR*-, *WAW*-, RAW-*Abhängigkeiten*:
  
  - **Serialisieren** aller Speicherabfragen um vorhersagbares Verhalten zu garantieren (*In-Order-Execution*), schlechteste Performance
  - **keine Garantien** irgend einer Art, dafür maximale Optimierung der Speichernutzung, ein `SYNC`-Befehl muss vom Programm ausgeführt werden um den Speicher zu ordnen, es werden vorerst keinen neuen Speicher-Befehle ausgeführt
  - Eigenheiten der ISA sind auf zugrunde liegende Architekturgestaltung zurück zu führen

#### Register

- Sind auf der Mikroarchitektur-Ebene implementiert, und für die ISA-Ebene Sichtbar, aber z.B. Register für den Kernel-Modus zur Hardwaresteuerung sind für die ISA-Ebene und deren Benutzer nicht sichtbar

- Die ISA legt die Spezial-Register fest und wie viele allgemeine Register für Ganz- und Gleitkomma-Zahlen zu Verfügung stehen sowie deren Adessierung 

- Sie steuern die Ausführung des Programms, speichern Zwischenergebnisse und Zustände und geben Zugriff darauf um Speicherzugriffe zu vermeiden

- 32 oder auch mehr allgemeine Register zu freien Wahl bei der Verwendung

- Oft haben aber Systeme Konventionen für die Registerverwendung an die man sich halten sollte um Konflikte zu vermeiden

#### Befehle

Hauptmerkmal der ISA, die Maschienenbefehle steuern die Aktionen der Maschine

- arithmetische Befehle, logische Befehle, Operanden Vergleichen und Verzweigen, 

- Datentransport zwischen Registern, Kopieren, Laden, Speichern

### Architekturentwicklung

- IA-32 ist kompatibel zurück bis zum (16-Bit) 8088, 8086, (8-Bit) 8080, 8008 und (4-Bit) 4004 

- 80386 erste 32-Bit Architektur die alle Nachfolger mit leichten Änderungen auch besitzen (80486, Pentium, Pentium Pro, Pentium II, Pentium III, Pentium 4,  Celeron, Xenon, Pentium M, Centrino, Core 2 duo, Core i7...)

- AMD64 o. x86-64 ist die 64-Bit Erweiterung der IA-32, hebt Ganzzahlberechnungen und virtuelle Adressen auf 64-Bit an

- **3 Modi in Intel Prozessoren:**
  
  - **Real-Modus**: Schaltet alle eingeführten Merkmale ab dem 8088 ab, Fehler legen den Prozessor lahm
  
  - **virtueller 8086-Modus**: Verhalt sich wie ein 8088, das OS behält aber die Kontrolle über den ganzen Computer, MS-DOS Programme werden isoliert ausgeführt und Fehler an das  OS gemeldet
  
  - **geschützter Modus**: Verhält sich wie ein Core i7 mit 4 Ebenen, 0 Ist der Kernel-Modus fürs OS mit vollem Maschienenzugriff, 3 Ist für Anwendungsprogramme, 1,2 werden selten benutzt

### Datentypen

- Die ISA definiert Ganzzahlen, Fest- und Fließkommazahlen, logische Werte, Zeichenketten und Zeiger

- Es werden Formate, Genauigkeit und Operationen festgelegt

- Es gibt Hardware gestützte Datentypen für die HW vorhanden ist und welche die nur in der Software implementiert ist.

- Numerische Datentypen
  
  - Vorzeichen los 32-Bit 2³² -1
  
  - Vorzeichen behaftet 32-Bit 2³¹ -1 **Zweierkomplement**
  
  - Gleitkommazahlen 32, 64, 128 Bit, umfassen einfache Genauigkeit und doppelte Genauigkeit, sind Näherungswerte reeller Zahlen und werden als näherungsweise numerische Typen betrachtet.
  
  - Hardware unterstütze Dezimalzahlen 4-Bit pro Byte, **BCD**-Format (binärcodiertes Dezimalformat)

- Nicht numerische Datentypen
  
  - Zeichenfolgen, oft Durchsuchen und Kopieren in der HW implementiert
  
  - Boolsche Werte, die Verwendung eines ganzen Bytes ist üblich, alles ungleich Null wird als Wahr interpretiert
  
  - Bittmaps, 32-Bit hat 32 Boolsche Werte
  
  - Zeiger, Maschienenadresse

### Befehlsformate

      ┏━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━┓
      ┃            OPCODE              ┃
      ┣━━━━━━━━┳━━━━━━━━━━━━━━━━━━━━━━━┫
      ┃ OPCODE ┃ ADDR                  ┃
      ┣━━━━━━━━╋━━━━━━━━━━━┳━━━━━━━━━━━┫
      ┃ OPCODE ┃ ADDR1     ┃ ADDR2     ┃
      ┣━━━━━━━━╋━━━━━━━┳━━━┻━━━┳━━━━━━━┫
      ┃ OPCODE ┃ ADDR1 ┃ ADDR2 ┃ ADDR3 ┃
      ┗━━━━━━━━┻━━━━━━━┻━━━━━━━┻━━━━━━━┛

- Design Kriterien sind ua.
  
  - Die Läng der Befehle, fest oder variabel (Speicherusflösung vs Bandbreite vs Befehlslänge vs CPU Geschwindigkeit vs Decodieraufwand vs Caches)
  
  - Länge des Befehlsformates für die OPCODE's (`2^n` Befehle brauchen `n` Bits pro Befehl, zukünftige Erweiterungen
  
  - Anzahl der Bits im Adressfeld (Decodierung Speicherauflösung)

- Bei manchen Prozessoren sind alle OPCODE's gleich lang, das erleichtert die Decodierung und ermöglicht einen effizentere Implementirung kann aber auch Platz verschwenden.

- Längere OPCODE's und größere Adressbreite schaffen mehr Flexibilität, haben aber auch größeren Speicherbedarf und längere Zugriffszeiten.

- Die Befehlslänge kann eine Wortlänge sein aber auch darunter o. darüber liegen, sie bestimmt auch die Größe die ein Programm im Speicher belegt (16-Bit, 32-Bit), und sie wirkt sich Maßgeblich auf die Prozessorleistung aus (Caches, Pipelining)

- unter sonst gleichen Umständen sind kurze Befehle immer besser als lange

- Die Bassiseinheit für den Speicher bestimmt wieviele Speicheradressen benötigt werden, je kleiner (zb. 8bit) desto mehr Adressen, je größer (zb. 32bit) desto weniger Adressen aber um so mehr Aufwand einzelne Zeichen zu adressieren.

- Je feiner die Speicherauflösung, desto länger die Adressen und damit auch die Befehle.

- OPCODES können auch erweitert werden in dem mann die zur Verfühgung stehenenden Bits in Unterschiedliche Felder aufteilt zB.  16 Bit in 15 Drei-Adressbefehle, 14 Zwei-Adressbefehle, 31 Ein-Adressbefehle und 16 Befehle ohne Adresse

- in der IA-32 wird der 1-Byte-Opcode über einen Escape-Code um eine zweites Befehlsbyte erweitert. Es werden auch Präfixbytes eingesetzt um einzelne Befehle zu modifizeren. So können immer neue Maschienen Befehle integriert werden.

### Adressierung

Es gibt viele verschiedene Adressier-Modi, nicht alle sind immer in allen Architekturen verfügbar

Für eine effizente ISA müssen nicht alle Modi implementiert sein, in der Praxis genügen meist unmittelbarer, direkter, Register- und indizierter Modus. Durch kompliziertere Adressierungsmodi lässt sich die Anzahl der Befehle verringern aber dafür müssen zusätzliche Operationssequenzen (Befehle) eingeführt werden die sich mit anderen sequnziellen Operationen nicht parallel ausführen lassen.


- **Unmittelbare Adressierung**
  
  - *Operant ist Wert*
  
  - Konstante wird direkt im Befehl spezifiziert (unmittelbarer, immediate Operant),
  
  - Die Größe des Wertes wird von der größe des Feldes beschränkt

- **Direkte Adressierung:**
  
  - *Operant ist die effektive Speicheradresse*
  
  - Opereant wird mit vollständiger Speicheradresse spezifiziert
  
  - Die Position im Speicher ist Fix, aber die Daten/der Wert sind variabel
  
  - nur für globale Variablen nützlich, wo Adressen zu Compiliertzeit bekannt sind

- **Indirekte Adressierung:**
  
  - Operant ist Speicheradresse die die effektive Speicheradresse enthält

- **Registeradressierung direk:**
  
  - *Operant ist CPU Register das den Wert enthält*
  
  - wie direkte Adressierung, nur wird eine Register spezifiziert
  
  - Compiler können für häufig verwendete Variablen Register festlegen (z.B. ein Schleifenindex)

- **Registeradressierung indirekt:**
  
  - *Operant ist CPU Register das die effektive Speicheradresse enthält*
  
  - Quelle o. Ziel des Operanten ist im Speicher der über eine Adresse Referenziert wird
  
  - Diese Adresse ist nicht fest im Befehl codiert, sondern in einem Register enthalten
  
  - Der Wert des Registers kann sich mit jedem Aufruf ändern und somit auch das abgerufene Speicherwort (lokale Variablen)

- **Indizierte Adressierung:**
  
  - *Operant ist ein Vorher bekannter Versatz um zur effektiven speicheradresse zu gelangen*
  
  - Die effektive Speicheradresse wird Adressiert in dem zu einem (expliziet oder implizit) angegebenen Register ein vorher bekannter Versatz (Offset) hinzu addiert wird (Indexed Addressing)

- **Basis Indizierte Adressierung:**
  
  - ist relativ zu einer Basisadresse

- **Relative Adressierung:**
  
  - Die effektive Speicheradresse ist eine Adresse relative zur Adresse des Programcounters
  
  - Der Oprant ist der Versatz (Offset) vom `PC`
  
  - Dieser Modus wird von Sprunganweisungen verwendet

- **Stapel Adressierung:**
  
  - Hier eignet sich hervoragend die **Umgekerte polnische Notation** nach J. Lukasiewicz für Rechen-Operationen. Mit dieser lassen sich Operationen CPU-gerecht beschreiben. Dijkstra hat einen Algorythmus zur Umwandlung von einer Notation in die Andere entwickelt, diese ähnelt eineme **Push & Pop**-verfahren auf einem Stack.
  
  - **Infix Notation:** `(8 + 2 × 5) / (1 + 3 × 2 – 4)`
  
  - **Postfix Notation:** `8 2 5 × + 1 3 2 × + 4 – /` 
    (o. Umgekerte polnische Notation nach J. Lukasiewicz)

  ```asm6502
  Schritt  Verbleibende Zeichenfolge   Befehl      Stapel
  ---------------------------------------------------------------------
  1        8 2 5 × + 1 3 2 × + 4 − /   BIPUSH 8    8
  2        2 5 × + 1 3 2 × + 4 − /     BIPUSH 2    8,   2
  3        5 × + 1 3 2 × + 4 − /       BIPUSH 5    8,   2,  5
  4        × + 1 3 2 × + 4 − /         IMUL        8,  10
  5        + 1 3 2 × + 4 − /           IADD        18
  6        1 3 2 × + 4 − /             BIPUSH 1    18,  1
  7        3 2 × + 4 − /               BIPUSH 3    18,  1,  3
  8        2 × + 4 − /                 BIPUSH 2    18,  1,  3,  2
  9        × + 4 − /                   IMUL        18, 1,   6
  10       + 4 − /                     IADD        18, 7
  11       4 − /                       BIPUSH 4    18,  7,  4
  12       − /                         ISUB        18, 3
  13       /                           IDIV        6
  ```

Die Zahl oben auf der Spitze des Stapels ist der rechte Operand und nicht der linke. Es wird also immer zuerst der Zähler und dann der Nenner auf den Stapel gelegt. Das ist bei Divisionen und Subtraktionen wichtig, weil die Reihenfoge der Operanten signifikant ist.

### Adressierungsmodi für Verzweigungen

- Dafür können die Verherbenannten Adressierungsmodi verwendet werden

- Häuf wird auch Adressierung relativ zum ***Programm Counter*** verwendet

- Bei der indirekten Registeradressierung kann ein Programm die Ziel Adressen zur Laufzeit berechnen und dann in ein Register schreiben was sehr Flexibel ist


### Traps

Tritt eine Ausnahme in einem Programm auf, so wird über einen Trap eine Behandlungsroutine automatisch aufgerufen.
