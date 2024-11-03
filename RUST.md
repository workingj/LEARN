# Rust

- [Rust](#rust)
    - [Debuging](#debuging)
    - [Variablen](#variablen)
    - [Ownership / Besitzrecht](#ownership--besitzrecht)
    - [Referencen](#referencen)
    - [Branching \& Controlflow / Verzweigung \& Kontrollfluss](#branching--controlflow--verzweigung--kontrollfluss)
    - [Datentypen](#datentypen)
    - [Modules](#modules)
    - [Traits](#traits)
    - [Newtype-Pattern, Wrapper Typen](#newtype-pattern-wrapper-typen)

## Debuging

- enabeling RUST_BACKTRACE

```rust
    /*
     * DEBUG > START
     */
    std::env::set_var("RUST_BACKTRACE", "1");
    // let socket = UdpSocket::bind("0.0.0.0:8887")?;
    /*
     * END > DEBUG
     */
```

## Variablen

### Assigment / Zuweisung

```rust
let zahl = if n > 33 { 1 } else { 2 };
```

### Shadowing

```rust
let var = 2 * 3;
let var = var * 5;
```

### Global Namespace

- Space around main

## Ownership / Besitzrecht

- Variablen sind nur gültig in ihrem scope
- jeder wert hat immer nur einen Besitzer
- einfache Datentypen wie integer, floats, char, bool, tupel mit gleichen primitiven datentyp in allen Feldern werdern automatisch kopiert (Copy-Trait)

## Referencen

## Branching & Controlflow / Verzweigung & Kontrollfluss

### match

- ist ein Ausdruck und liefert einen Rückgabewert

```rust
match number {
        1 => println!("One!"),
        2 | 3 | 5 | 7 | 11 => println!("This is a prime"),
        13..=19 => println!("A teen"),
        _ => println!("Ain't special"),
    }

let boolean = true;
let binary = match boolean {
        false => 0,
        true => 1,
    };
```

## Datentypen

### Primitive Datantypen

U8,

### Constanten

- immutable
- datatyp must be defined
- constant value, that must be evaluated during compiletime
- can be defined everywhere

```rust
const MAX_VALUE: u8 = 32 * 2;
```

### Tupel

- eine einfach Liste mit Werten
- keine neuen werte hinzufügbar
- keine alten werte entfernbar
- Datetypen können geischt werden

```rust
let colors = ("red", "green", "yellow");
println("Color: {}", colors.1);
// destructuring
let (r, g, y) = colors;

let d: (u8, f32, &str) = (1, 2.3, "Text);
```

### Arrays

- fester Datentyp für alle felder
- neue werte lassen sich hinzufügen
- alte werte lassen sich entfernen

```rust
let arr: [u8, 4] = [192, 168, 0, 1];
```

## Modules

- dürfern verschachtelt werden

## Traits

### Standardparameter für generische Typen und Operatorüberladung

**`<Rhs=Self>`: Standardtypparameter (default type parameters)**

```rust
trait Add<Rhs=Self> {
    type Output;

    fn add(self, rhs: Rhs) -> Self::Output;
}
```

- Um einen Typ zu erweitern, ohne bestehenden Code zu brechen.
- Um eine Anpassung zb eines Traits aus std in bestimmten Fällen zu ermöglichen
- Um eine Erweiterung der Funktionalität eines Traits zu ermöglichen kanst du einem vorhandenen Trait im Typparameter den Standardwert hinzufügen ohne den vorhandenen Implementierungscode zu brechen.

```rust
use std::ops::Add;

struct Millimeters(u32);
struct Meters(u32);

impl Add<Meters> for Millimeters {
    type Output = Millimeters;

    fn add(self, other: Meters) -> Millimeters {
        Millimeters(self.0 + (other.0 * 1000))
    }
}
```

### Vollständig qualifizierte Syntax für Methoden u. assoziierte Funktionen

- Nur nötig in Fällen in denen es mehrere Implementierungen gibt, die denselben Namen verwenden

```rust
<Type as Trait>::function(receiver_if_method, next_arg, ...);
```

Definieren von **Methoden** mit gleichem Namen

```rust
trait Pilot {
    fn fly(&self);
}

trait Wizard {
    fn fly(&self);
}

struct Human;

impl Pilot for Human {
    fn fly(&self) {
        println!("Hier spricht Ihr Kapitän.");
    }
}

impl Wizard for Human {
    fn fly(&self) {
        println!("Hoch!");
    }
}

impl Human {
    fn fly(&self) {
        println!("*Wütend mit den Armen wedeln*");
    }
}
```

Aufrufen von **Methoden** mit gleichem Namen

```rust
fn main() {
    let person = Human; // Human::fly(&person)
    Pilot::fly(&person);
    Wizard::fly(&person);
    person.fly();
}
```

Definieren von **assoziierten Funktionen** mit gleichem Namen

```rust
trait Animal {
    fn baby_name() -> String;
}

struct Dog;

impl Dog {
    fn baby_name() -> String {
        String::from("Spot")
    }
}

impl Animal for Dog {
    fn baby_name() -> String {
        String::from("Welpe")
    }
}
```

Aufrufen von **assoziierten Funktionen** mit gleichem Namen

```rust
fn main() {
    println!("Ein Hundebaby wird {} genannt.", <Dog as Animal>::baby_name());
}
```

### Supertraits

- Sind Traits deren Elemente wiederum in anderen Traits verwendet werden und somit für eine implementierug vorraus gesetzt werden  
  
```rust
use std::fmt;

trait OutlinePrint: fmt::Display {
    fn outline_print(&self) {
        let output = self.to_string();
        let len = output.len();
        println!("{}", "*".repeat(len + 4));
        println!("*{}*", " ".repeat(len + 2));
        println!("* {output} *");
        println!("*{}*", " ".repeat(len + 2));
        println!("{}", "*".repeat(len + 4));
    }
}
```

Da wir festgelegt haben, dass OutlinePrint das Merkmal Display erfordert, können wir die Funktion to_string verwenden, die automatisch für jeden Typ implementiert wird, der Display implementiert.

## Newtype-Pattern, Wrapper Typen

- zum umgehen der Waisenregel

```rust
use std::fmt;

struct Wrapper(Vec<String>);

impl fmt::Display for Wrapper {
    fn fmt(&self, f: &mut fmt::Formatter) -> fmt::Result {
        write!(f, "[{}]", self.0.join(", "))
    }
}

fn main() {
    let w = Wrapper(vec![String::from("Hallo"), String::from("Welt")]);
    println!("w = {w}");
}
```
