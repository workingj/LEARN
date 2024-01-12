# Java Read Sheet

## Was ist eine [Klasse](https://docs.oracle.com/javase/tutorial/java/concepts/class.html)

- Eine Klasse ist eine Blaupause ode Prototype, von dem  Objekte erzeugt werden
- Die Definition einer Klasse ist ein Programmstück (Quell-Code), welches spezifiziert, wie sich die Objekte dieser Klasse verhalten.
- Nachdem eine Klasse definiert wurde, können Objekte dieser Klasse erzeugt werden.
- Diese Klassen können verwendet werden, um auf einfache Weise komplizierte Anwendungen, z.B. mit graphischen Benutzeroberflächen zu realisieren.
- Vordefinierte Klassen befinden sich in der Standard Bibliothek von Java.

## Was ist ein [Objekt](https://docs.oracle.com/javase/tutorial/java/concepts/object.html)

- Repräsentiert ein Objekt der realen Welt oder eines gedachten Modelles
- Das erstellen eine Objektes nenn sich Instanzierung
- Jedes Objekt gehört zu genau einer Klasse und wird Instanz (Exemplar) dieser Klasse genannt.
- Alles Objekte der selben Klassen, haben das gleiche Verhalten
- Methoden (Funktionen) representieren das Verhalten
- Felder (Variablen) repräsentieren den Zustand

**Vorteile Software in Objekte zu Bündeln**

- Modularität: Quellcode eines Objekts kann unabhängig von anderem Code gewartet werden
- Informationsschutz (Data Encapsulation): Interaktion über Methoden verhindert das innere Daten sichtbar werden
- Code Wiederverwendung: Das Objekt kann leicht in anderen Kontexten wieder verwendet werden
- Zuschaltbarkeit und Debug vereinfachung: Fehlerhafte Objekte einfach durch ein anderes ersetzen

## Was ist eine  Methode

- Das in einer Klasse **vordefinierte Verhalten** wird als **Methode** bezeichnet.
- Das aufrufen der Methode eines Objektes entspricht dem Senden der Nachricht an dieses Objekt.
- Methoden ohne Rückgabewert geben `void` zurück.

### **Signatur** eine Methode

Bezeichnung (Name) der Methode plus Beschreibung seiner Argumente

```java
feineMethode(int value, int counter)
```

### **Prototyp** einer Methode

Signatur + Beschreibung des Return-Wertes

```java
int feineMethode(int value, int counter);
```

### **Selektor** einer Methoden

```java
  System.out.println("Hallo Welt!");/*
  |________________________________| > Statement
            |______________________| > Methoden-Aufruf
  |_________|                        > Referenz auf Empfänger_Objekt
            |_______|                > Methoden Selector (Verhalten, sendet Nachricht)
                    |______________| > Argument (Inhalt der NChricht)

```

Alle Aktionen in Java werden durch **Statements** spezifiziert.

### Was sind Statements

- Das Versenden einer Nachricht an ein Objekt ist eine vom Programmierer spezifizierte Aktion.
- Diese Aktion wird vom Computer ausgeführt, wenn das Programm läuft.
- In Java werden alle Aktionen durch Statements spezifiziert.
- der Gesammte Ausdruck `System.out.println("Argument");` ist ein **Statement**
- Statements werden in der Reihenfolge ausgeführt, in der siegeschrieben wurden.

### Was sind Expressions (Ausdrücke)
Expressions, Statements, and Blocks

Now that you understand variables and operators, it's time to learn about expressions, statements, and blocks. Operators may be used in building expressions, which compute values; expressions are the core components of statements; statements may be grouped into blocks.
Expressions

An expression is a construct made up of variables, operators, and method invocations, which are constructed according to the syntax of the language, that evaluates to a single value. You've already seen examples of expressions, illustrated in bold below:

int cadence = 0;
anArray[0] = 100;
System.out.println("Element 1 at index 0: " + anArray[0]);

int result = 1 + 2; // result is now 3
if (value1 == value2) 
    System.out.println("value1 == value2");

The data type of the value returned by an expression depends on the elements used in the expression. The expression cadence = 0 returns an int because the assignment operator returns a value of the same data type as its left-hand operand; in this case, cadence is an int. As you can see from the other expressions, an expression can return other types of values as well, such as boolean or String.

The Java programming language allows you to construct compound expressions from various smaller expressions as long as the data type required by one part of the expression matches the data type of the other. Here's an example of a compound expression:

 
1 * 2 * 3

In this particular example, the order in which the expression is evaluated is unimportant because the result of multiplication is independent of order; the outcome is always the same, no matter in which order you apply the multiplications. However, this is not true of all expressions. For example, the following expression gives different results, depending on whether you perform the addition or the division operation first:

x + y / 100    // ambiguous

You can specify exactly how an expression will be evaluated using balanced parenthesis: ( and ). For example, to make the previous expression unambiguous, you could write the following:

 
(x + y) / 100  // unambiguous, recommended

If you don't explicitly indicate the order for the operations to be performed, the order is determined by the precedence assigned to the operators in use within the expression. Operators that have a higher precedence get evaluated first. For example, the division operator has a higher precedence than does the addition operator. Therefore, the following two statements are equivalent:

x + y / 100 


x + (y / 100) // unambiguous, recommended

When writing compound expressions, be explicit and indicate with parentheses which operators should be evaluated first. This practice makes code easier to read and to maintain.
Statements

Statements are roughly equivalent to sentences in natural languages. A statement forms a complete unit of execution. The following types of expressions can be made into a statement by terminating the expression with a semicolon (;).

    Assignment expressions
    Any use of ++ or --
    Method invocations
    Object creation expressions

Such statements are called expression statements. Here are some examples of expression statements.

// assignment statement
aValue = 8933.234;
// increment statement
aValue++;
// method invocation statement
System.out.println("Hello World!");
// object creation statement
Bicycle myBike = new Bicycle();

In addition to expression statements, there are two other kinds of statements: declaration statements and control flow statements. A declaration statement declares a variable. You've seen many examples of declaration statements already:

// declaration statement
double aValue = 8933.234;

Finally, control flow statements regulate the order in which statements get executed. You'll learn about control flow statements in the next section, Control Flow Statements
Blocks

A block is a group of zero or more statements between balanced braces and can be used anywhere a single statement is allowed. The following example, BlockDemo, illustrates the use of blocks:

```java
class BlockDemo {
     public static void main(String[] args) {
          boolean condition = true;
          if (condition) { // begin block 1
               System.out.println("Condition is true.");
          } // end block one
          else { // begin block 2
               System.out.println("Condition is false.");
          } // end block 2
     }
}
```


## Was ist [Inheritance (Vererbung)](https://java-tutorial.org/vererbung.html)?

- Erlaubt es Klassen gemeinsam genutztes Verhalten mit anderen Klassen zu teilen
- Es wird jetzt zwischen einer Super- und einer Subklasse unterschieden
- Jede Subklasse die von Superklasse erbt, bekommt alle Felder und Methoden der Superklasse
- In der Subklasse befindent sich nur der Code der diese von der Superklasse unterscheidet
- Jede Klasse erbt von der `Objekt`-Klasse `toString()`, `equals()`, `getClass()`, `hashCode()`, `clone()`
- **extends** sorgt dafür das `BetterBR` alles Methoden und Instanzvariablen die in `BufferedReader` definiert wurden auch besitzt. (sie werden quasi vereerbt...)

```java
class MountainBike extends Bicycle {
    // new fields and methods defining a mountain bike would go here
}
class RoadBike extends Bicycle {
    // new fields and methods defining a road bike would go here
}
```

```java
    public static void main ( String[] args )
    {
        Bicycle fahrrad = new MountainBike( "blau" );
        fahrrad = new RoadBike ( "rot" );
    }
}
```

## Was ist [Polymorphie](https://java-tutorial.org/polymorphie.html)

- Wenn  zwei Klassen denselben Methodennamen verwenden, aber die Implementierung der Methoden sich unterscheidet
- Häufig wird Polymorphie bei der Vererbung verwendet

## Was ist Data Encapsulation

- Ein Grundprinzip Objekt orientierter Programmierung (OOP)
- Verbergen des inneren Zustands eines Objekts
- Felder eines Objekts können nicht direkt von außen verändert werden, sondern nur über die Methoden eines Objekts
- Methoden zur Veränderung der Felder eines Objekts können verhindern dass z.B. ungültige Werte übergeben werden

## Information hiding

A supposed benefit of encapsulation is that it can reduce system complexity, and thus increase robustness, by allowing the developer to limit the interdependencies between software components.


## Fehler

Wir unterscheiden grob 2 Arten von Fehlern:

1. Compile-Zeit-Fehler (compile-time errors) werden bei der Übersetzung entdeckt und führen zum Abbruch des Übersetzungsprozesses.
2. Laufzeitfehler (run-time errors) treten bei der Ausführung auf und liefern falsche Ergebnisse oder führen zum Absturz des Programms.

Laufzeitfehler sind in der Regel schwerer zu entdecken!

## **Keywords**

### **`super`-Keyword**

Notwendiger Aufruf des Konstruktors der Superklasse zum

```java
public BetterBR(){
      super (new InputStreamReader(System.in));
}

import java.io.*;
class BetterBR extends BufferedReader {
      public BetterBR(){
            super (new InputStreamReader(System.in));
      }
      public BetterBR(String fileName) throws FileNotFoundException{
            super (new InputStreamReader (new FileInputStream(
                  new File (fileName))));
      }
      public int readInt() throws IOException{
            return Integer.parseInt(super.readLine().trim());
      }
}
```

### **`protected`-Keyword**

```java
class Figur {
protected String name;
      Figur (String s){ // Konstruktor
            name = s;
      }
      void zeichne(){
            System.out.println (" zeichne "+this);
      }
      void entferne(){
            System.out.println ("entferne "+this);
      }
      public String toString(){
            // fuer Text-Darstellung
            return "Figur: "+name;
      }
}
```

Spezielle Worte mit vordefinierter Bezeichnung zb.: `System, println, static, void, throws`

### **`public`:**

 used in a method or variable declaration. It signifies that the method or variable can be accessed by elements residing in other classes.

### **`private`:**

 bedeutet, das man nur von innerhalb der Klasse auf die mit `private` gekennzeichneten Methoden und Variablen zugreifen kann. used in a method or variable declaration. It signifies that the method or variable can only be accessed by other elements of its class.

### **`protected`:**

 used in a method or variable declaration. It signifies that the method or variable can only be accessed by elements residing in its class, subclasses, or classes in the same package.

### **`static`:**

 bedeutet, das eine Variable oder eine Methode die mit `public` gekennzeichnet ist unhabhängig von einem Objekt aufgerufen und verwendet werden kann.

### **`final`:**

 entspricht einer Konstante, wird einmal deklariert und initialisiert und ist danach nicht mehr veränderbar

### **`this`:**

  Repräsentiert eine Instanz der Klasse in der es Auftaucht. z.B. Zugriff auf eine `private` Variable o. eine Methode

### **`extends`:**

 Class X extends class Y to add functionality, either by adding fields or methods to class Y, or by overriding methods of class Y. An interface extends another interface by adding methods. Class X is said to be a subclass of class Y.

### **`super`:**

 used to access members of a class inherited by the class in which it appears. zB. Aufrufen des Konstruktors der übergeorneten Klasse.

### **`exception`**

 An event during program execution that prevents the program from continuing normally; generally, an error. The Java(TM) programming language supports exceptions with the try, catch, and throw keywords. See also exception handler.

### **`abstract`-Keyword**

A Java(TM) programming language keyword used in a class definition to specify that a class is not to be instantiated, but rather inherited by other classes. An abstract class can have abstract methods that are not implemented in the abstract class, but in subclasses.

- Es können keine Objekte einer abstrakten Klasse durch new erzeugt werden.
- Für abstrakte Methoden müssen die nicht-abstrakten Subklassen entsprechenden Code enthalten.

```java
abstract class Figur{
      abstract double flaeche(); // hier kein Rumpf
      // Muss von Sub-Klasse implementiert (überschrieben werden)
}
```

- **`abstract class`** A class that contains one or more abstract methods, and therefore can never be instantiated. Abstract classes are defined so that other classes can extend them and make them concrete by implementing the abstract methods. Z.b. `class Number` von der alle Wrapper-Klassen der primitiven Datentypen erben.
- **`abstract method`** A method that has no implementation
- **interface** used to define a collection of method definitions and constant values. It can later be implemented by classes that define this interface with the `implements` keyword.






## Was ist ein [Interface](https://docs.oracle.com/javase/tutorial/java/concepts/interface.html)

- Ist ein Sammlung von Methoden-Prototypen
- Wen ein Onjekt ein Interface implementiert, verspricht es das gesammte Verhalten des Interfaces auch zu besitzen.
- Wenn verschiedene Klassen das gleiche Interface implementieren können sie im sleben Kontext verwendet werden
- Beim übernehemen eines Interfaces für ein Objekt müssen **alle** Methoden imiplementiert werden

 ```java
interface Bicycle {
    void speedUp(int newValue);
}
 ```

```java
class FastBicycle implements Bicycle {
    int speed = 0;
    int gear = 1;

   // The compiler will now require that speedUp is implemented.
    pub void speedUp(int newValue) {
         speed = speed + increment;
    }
}
 ```

Interfaces dienen dazu, ein Verhalten zu spezifizieren, das von Klassen
implementiert werden soll. Eine Klasse kann mehrere Interfaces haben.
Ein Interface drückt Eigenschaften aus, die Klassen in unterschiedlichen Hierarchiestufen implementieren können.

```java
interface Orderable {
      boolean lessThan (Orderable comp);
      boolean equal (Orderable comp);
}
```

- Wenn eine Klasse ein Interface implementiert, kann sie so behandelt werden, als wäre sie eine Subklasse des Interfaces.
- Auch Interfaces können eine Hierarchie bilden.
- Eine implementierende Klasse muss alle Methoden eines implementierten Interfaces und seiner Vorgänger implementieren.
- Ob ein Objekt zu irgendeiner Klasse oder einem Interface gehört (is-a), lässt sich durch einen Ausdruck mit dem Schlüsselwort `instanceof` herausbekommen: Objektname `instanceof` Klasse-oder-Interface

```java
// class SortableInteger implements Orderable implements dies implements das {
class SortableInteger implements Orderable {
      private int val;

      SortableInteger (int val){
            this.val = val; // Konstruktor

      }
      public int intValue(){
            return this.val ; // Wert herausgeben
      }
      public boolean lessThan (Orderable comp){
            return this.val < ((SortableInteger) comp).val;
      }
      public boolean equal (Orderable comp){
            return ((SortableInteger) comp).val == this.val;
      }
      public String toString(){
            return new String(""+this.val); // String-Darstellung
      }
}
```

```java
interface EinDimensional{
      public int laenge();
}
interface ZweiDimensional extends EinDimensional{
      public int breite();
}
interface DreiDimensional extends ZweiDimensional{
      public int hoehe();
}
```

### Instanz mehrerer Interfaces

```java
public class Quader implements DreiDimensional,
Comparable<Quader> {
// ... Konstruktoren ...
public int laenge() { return 0; }
public int breite() { return 0; }
public int hoehe() { return 0; }
public int volumen (){
return laenge() * breite() * hoehe();
}
public int compareTo (Quader o){
int me = this.volumen();
int other = o.volumen();
if (me < other) return -1;
if (me > other) return 1;
return 0;
}
```

### Konstanten in Interfaces und Klassen

Interfaces können auch Konstanten `(static final)` definieren.

### Interfaces ohne Inhalt

Interfaces können Methoden, Konstanten, und Felder haben, oder auch leer sein.

### Interface-Implementierung durch anonyme Klasse

```java
public static void main (String[] args){
      plot (new D2Method() {// implementiert D2Method
                  public double compute (double value){
                  return value*value;
                  } // end compute
            } // end anonyme Klasse
      ); // end plot-Statement
} // end main
```

### Designentscheidung: Interface oder abstrakte Klasse

### Interface mit Standard-Implementierung

 ### **Overriding**

Die Klasse Kreis übernimmt alle Methoden der Klasse Figur.
Die Methode toString wird aber durch eine angepasste Version ersetzt.
Diesen Prozess der Ersetzung bzw. Überschreibung von Methoden nennt man Overriding.

```java
class Kreis extends Figur {
      protected Punkt zentrum;
      protected int radius;

      Kreis (String s, int x, int y, int r){// Konstruktor
            super (s);
            zentrum = new Punkt (x,y);
            radius = r;
      }
      public String toString(){ //ueberschriebene Methode
            return "Kreis: "+name+" Zentrum: "+
            zentrum+" Radius: "+radius;
      }
}
```

Möglich weil Kreis abgeleitet von Figur

```java
Figur k = new Kreis ("Otto", 3, 3, 5);
```

## **Polymorphie**

### Ausnutzung der Polymorphie

Wenn Kollektionen von Figur-Objekten verwaltet werden sollen,
können wir die Polymorphie ausnutzen:

```java
Figur[] fa = {
      new Figur ("Anna"),
      new Kreis ("Otto", 3, 3, 5),
      new Rechteck ("Cy", 7, 5, 1) };
for (Figur f: fa) f.entferne ();
```

### Zusammenfassung gemeinsamer Eigenschaften in einer Superklasse

- Wir könnten neben Kreis noch weitere Klassen von Figur ableiten, etwa Rechteck, Dreieck, ...
- Objekte verschiedener Subklassen unterscheiden sich zwar. Gemeinsam an ihrem Verhalten ist aber, dass sie alle die Methoden der Superklasse besitzen.
- Vererbung kann genutzt werden, um gemeinsame Eigenschaften von Subklassen zusammenzufassen.

### Abstrakte Methoden und Klassen (Motivation)

- Die Klasse Figur haben wir eigentlich dafür benutzt, um gemeinsame Eigenschaften ihrer Subklassen zusammenzufassen.
- Darüber hinaus wurde nur auf die Methoden der Klasse `Figur` zugegriffen.
- Was aber können wir tun, wenn wir in der `entferne`-Methode eine Ausgabe der Fläche vorsehen wollen?
- Für eine sinnvolle Methode `flaeche()` ist in dieser Klasse noch zuwenig Information vorhanden. Eine Platzhalter-Methode würde auf jeden Fall von Subklassen **überschrieben** werden.


## dynamisches binden