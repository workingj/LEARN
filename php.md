# PHP

- [PHP](#php)
  - [Setup](#setup)
    - [php.ini-Direktiven des Sprachkerns](#phpini-direktiven-des-sprachkerns)
  - [Error Reporting](#error-reporting)
  - [PHP-TAG](#php-tag)
  - [Ausführung](#ausführung)
  - [Ausdrücke](#ausdrücke)
  - [Operatoren](#operatoren)
    - [Ternärer Operator `?:`](#ternärer-operator-)
    - [?? - Coalescence Operator](#---coalescence-operator)
    - [OR](#or)
    - [Inkrement und Dekrement](#inkrement-und-dekrement)
    - [Vergleichsoperatoren](#vergleichsoperatoren)
  - [Typsystem](#typsystem)
    - [Runden](#runden)
    - [Weak Typing](#weak-typing)
    - [Typumwandlung (Typen-Jonglage)](#typumwandlung-typen-jonglage)
    - [Type Casting](#type-casting)
    - [Typenvergleich](#typenvergleich)
  - [include und require](#include-und-require)
  - [Variablen](#variablen)
    - [Referencen](#referencen)
    - [Vordefinierte Variablen](#vordefinierte-variablen)
    - [Variablen aus externen Quellen (HTML-Formulare)](#variablen-aus-externen-quellen-html-formulare)
    - [Geltungsbereich von Variablen](#geltungsbereich-von-variablen)
    - [Vardump to String](#vardump-to-string)
    - [Isset vs Empty vs Is\_null](#isset-vs-empty-vs-is_null)
      - [Truth table](#truth-table)
      - [Differences table](#differences-table)
  - [Datentypen](#datentypen)
    - [Booleans](#booleans)
    - [Strings](#strings)
    - [Arrays](#arrays)
      - [Assoziative Arrays](#assoziative-arrays)
      - [Foreach und Arrays](#foreach-und-arrays)
      - [Array Destrukturierung](#array-destrukturierung)
    - [Konstanten](#konstanten)
    - [Compile-time constants](#compile-time-constants)
  - [Kontrolltrukturen / Verzweigungen](#kontrolltrukturen--verzweigungen)
  - [Funktionen](#funktionen)
  - [Anonyme Funktionen - Closures](#anonyme-funktionen---closures)
  - [Objektorientierung](#objektorientierung)
    - [public, protected, private](#public-protected-private)
    - [OOP - Klassen](#oop---klassen)
    - [OOP - Interfaces](#oop---interfaces)
    - [OOP - Vererbung](#oop---vererbung)
    - [OOP - Abstract Classes](#oop---abstract-classes)
    - [OOP - Statische Funktionen](#oop---statische-funktionen)
    - [OOP - Magic Methodes](#oop---magic-methodes)
    - [OOP - Konstanten](#oop---konstanten)
    - [OOP - Static](#oop---static)
    - [OOP - Singelton Pattern](#oop---singelton-pattern)
  - [Namespaces](#namespaces)
  - [Autoloading](#autoloading)
    - [PSR-4 (PHP Standard Recommentation) Improved Autoloading](#psr-4-php-standard-recommentation-improved-autoloading)
  - [Exceptions](#exceptions)
  - [Output Kontrolle](#output-kontrolle)
  - [HTTP QUERIES](#http-queries)
  - [HTTP Header](#http-header)
  - [SESSIONS](#sessions)
  - [COOKIES](#cookies)
  - [MySQL und PDO](#mysql-und-pdo)
    - [PDO - PHP Data Object](#pdo---php-data-object)
    - [PDO - Fetch in to Class](#pdo---fetch-in-to-class)
    - [MYSQL - Storage Engines](#mysql---storage-engines)
    - [MYSQL - InnoDB - Tranaktionen](#mysql---innodb---tranaktionen)
  - [Sicherheit](#sicherheit)
    - [Sicherheit bei Formularen](#sicherheit-bei-formularen)
    - [Sicherheit bei Nutzereingaben](#sicherheit-bei-nutzereingaben)
    - [Passwortsicherheit](#passwortsicherheit)
    - [SQL-Sicherheit](#sql-sicherheit)
  - [BestPractice](#bestpractice)
    - [Code Strucktur](#code-strucktur)
    - [MCV - Pattern](#mcv---pattern)
  - [Examples](#examples)
    - [Time](#time)
    - [Ordner auslesen](#ordner-auslesen)
    - [PHP Formulare](#php-formulare)
    - [GET - Formular](#get---formular)
    - [POST - Formular](#post---formular)
    - [Render Funktion](#render-funktion)
    - [Container - Pattern](#container---pattern)
  - [Reguläre Ausdrücke](#reguläre-ausdrücke)
  - [.htaccess](#htaccess)
    - [**Fehlerseite Konfigurieren**](#fehlerseite-konfigurieren)
  - [Berechtigungen unter Linux](#berechtigungen-unter-linux)
    - [Complete Tables](#complete-tables)
    - [Default Permissions](#default-permissions)
    - [How to change permissions for a folder and its subfolders/files](#how-to-change-permissions-for-a-folder-and-its-subfoldersfiles)

## Setup

**C:\xampp\php\php.ini**  

- nach Änderung Webserver neu starten

XAMPP - Config

```ini
display_errors=On
display_startup_errors=On

sudo /opt/lampp/lampp start
sudo /opt/lampp/lampp stop
```

### [php.ini-Direktiven des Sprachkerns](https://www.php.net/manual/de/ini.core.php#ini.variables-order)

## Error Reporting

```php
ini_set('display_errors', 1);
ini_set('display_startup_errors', 1);
error_reporting(E_ALL);

// Warnungen verhindern mit @ pro Ausdruck
@include __DIR__ . DIRECTORY_SEPARATOR . "b.php";

```

## PHP-TAG

```php
// Nur bereich
<?php ...?>
// für ganzes Dokument nicht schließen
<?php
```

**[Kurtztag](https://www.php.net/manual/de/language.basic-syntax.phptags.php)**

- erzeugt einen Zeilenumbruch

```php
// das gleiche wie <?php echo "hallo"; ?>
<?= "hallo"?>
```

**Ausgabe unter Verwendung von Bedingungen**

```php
<?php if ($expression == true): ?>
Dies wird angezeigt, wenn der Ausdruck wahr ist.
<?php else: ?>
Andernfalls wird dies angezeigt.
<?php endif; ?>

<!-- Alternative -->

<?php if (!empty($pageTitle)) {?>
    <h2><?php echo $pageTitle; ?></h2>
<?php }?>

<!-- Alternative -->

<?php $ver3 = TRUE;  $debug2 = FALSE; ?> 
// and then deeper inside the file: 
<?php if ($ver3) {
print("This code is included since we are testing version 3");
}
?>

<?php if ($debug2) {
print("This code is 'commented' out");
}
?>
```

**PHP mit HTML verschachtelt**

```php
<?php
$bgColor = 'red';
?>

<p<?php if (!empty($bgColor)): ?> style="background-color: <?php echo $bgColor ?>;"<?php endif;?>>Test Inhalte...</p>
```

- Wenn eine Datei nur PHP-Code enthält, ist es besser, den schließenden PHP-Tag am Ende der Datei wegzulassen. Dies verhindert, versehentliche ausgaben da php an dieser stelle mit der ausgabe beginnt.
- Wenn PHP in XML oder XHTML eingebettet wird, müssen die normalen `<?php ?>`-PHP-Tags verwenden werden, um die Standards einzuhalten.
- Für die Ausgabe von großen Textblöcken ist der Ausstieg aus dem Parse-Modus generell effizienter, als den gesamten Text durch echo oder print zu jagen

## Ausführung

- [`eval()`](https://www.php.net/manual/de/function.eval.php) Sprach Konstrukt das gegebenen Code auswertet und bei return mit null oder gegebenem Wert zurück kehrt
- ein loses returnstatement in einem script, beendet einen script und kann einen variable über include zurückgeben

### Differences between die() and exit() Functions:

| die()                                            | exit()                                                                            |
| ------------------------------------------------ | --------------------------------------------------------------------------------- |
| The die() method is used to throw an exception   | The exit() method is only used to exit the process.                               |
| The die() function is used to print the message. | The exit() method exits the script or it may be used to print alternate messages. |
| This method is from die() in Perl.               | This method is from exit() in C.                                                  |

## Ausdrücke

- alles was einen Wert het oder zurück gibt
- Anweisung werden von rechts nach links geparst
- `$i += 2`, `$i -= 2`, `$i *= 2`, `$i /= 2` schneller als `$i = 4i + 2`

## Operatoren

### Ternärer Operator `?:`

- `(ausdr1) ? (ausdr2) : (ausdr3);`
  - wenn (ausdr1) true dann (ausdr2)
  - wenn (ausdr1) false dann (ausdr3)

### ?? - Coalescence Operator

- Ersetzt IF(isset())-Kombinationen

```php
$currentPage = @(int) ($_GET['page'] ?? 1);
```

### OR

Both OR and || are short-circuited operators, which means they will stop evaluating once they reach a TRUE value. By design, OR is evaluated after assignment (while || is evaluated before assignment).

This has the benefit of allowing some simple constructions such as:

```php
$stuff=getStuff() or die('oops');
$thing=something() or $thing=whatever();
```

The first example, often seen in PERL, could have been written as `<?php if(!$stuff=getStuff()) die('oops'); ?>` but reads a little more naturally. I have often used it in situations where null or false indicate failure.

The second allows for an alternative value if a falsy one is regarded as insufficient. The following example

```php
$page=@$_GET['page'] or $page=@$_COOKIE['page'] or $page=1;
```

is a simple way sequencing alternative values. (Note the usual warnings about using the @ operator or accepting unfiltered input …)

All this presupposes that 0 is also an unacceptable value in the situation.

### Inkrement und Dekrement

- Post: `var++`, `var--`, verändern nach auslesen
- Prä: `++var`, `--var`,  verändern vor auslesen

### Vergleichsoperatoren

- `>` größer
- `<` kleiner
- `>=` größer oder gleich
- `<=` kleiner oder gleich
- `!=` ungleich
- `==` gleich
- `===` inhalts- und typgleich, keine Typen Konvertrierung zugelassen
- `!==` nicht inhalts- oder typgleich, keine Typen Konvertrierung zugelassen

## Typsystem

- **Skalare**
  - int, float,string, bool
  - lassen sich nicht in kleinere Elemente aufteilen
- **Zusammengesetzte**
  - Array, Objekt
- **Typenkonvertierung verhindern mit** [`declare(strict_types=1);`](https://www.php.net/manual/de/language.types.declarations.php#language.types.declarations.strict)

### Runden

```php
round(12,7); // Runden float(13)
ciel(12,7); // Aufrunden float(13)
floor(12,7); // Abrunden float(12)
```

### Weak Typing

```php
$a = '2';
is_string($a); // true
is_bool($a);  // false
is_array($a); // false
is_numeric($a); // true
'2' == 2; // true
'2' === 2; // false
echo '2' + 2; // 4
echo '2' + '2'; // 4
```

### Typumwandlung (Typen-Jonglage)

- [Typumwandlung (Typen-Jonglage)](https://www.php.net/manual/de/language.types.type-juggling.php#language.types.typecasting)

### Type Casting

```php
$a = (int) 12.7; // Integer
$a = (float) 12.7; // Float
$len = (int) $_GET['len']; // int(...)
$len = round($_GET['len']); // fload(...)

$foo = 10;            // $foo ist eine ganze Zahl
$str = "$foo";        // $str ist eine Zeichenkette
$fst = (string) $foo; // $fst ist ebenfalls eine Zeichenkette

$var = 3 / 2  = 0,6666 // ungleiche teilung wird zu float
```

### Typenvergleich

-[Tabelle zu Typenvergleichen in PHP](https://www.php.net/manual/de/types.comparisons.php)

## include und require

- variablen müssen vor ***include*** gesetzt werden um sie in den includierten scripts auf zu rufen
- führt eine Datei aus, unabhängig von ihrer Endung
- parst allen Text und führt nur php aus
- geht bei Pfadsuche immer von der Einstigs Datei aus
- **include, & include_once** warnt wenn Datei nicht vorhanden
- **require, & require_once** bricht ausführung ab wenn nicht vorhanden
- require kann return values haben, die man in variablen speichern kann, dafür müss man in der angeforderten Datie die Variablen am Ende returnen
- 
```php
include __DIR__ ."/f.php";
include __DIR__ . DIRECTORY_SEPARATOR . "b.php";
include dirname(__FILE__) . "/f.php";
// Verhindert erneutes Includieren
include_once __DIR__. "/f.php";
// Require bricht PHP ausführung ab
require __DIR__ ."/f.php";
require_once __DIR__ ."/f.php";
```

## [Variablen](https://www.php.net/manual/de/language.variables.php)

 **Declaration rules:**  

1. start with dollar sign($)
2. case-sensitive
3. first letter of variable name comes from a-zA-z_
4. next letters of variable name comes from a-zA-Z0-9_
5. no space,no syntex

**User Define variables are 3 types**

1. variable scope
2. variable variables
3. reference variable

**[variable Variablen](https://www.php.net/manual/de/language.variables.variable.php)**

- Eine variable Variable nimmt den Wert einer Variablen und behandelt ihn als Name der Variablen

```php
$a = 'Hallo';
$$a = 'Welt';
echo "$a {$$a}";
// gleichen Ausgabe wie
echo "$a $Hallo";
// Variable mit Variablem Namen
${'xyz'} = 'hallo welt';
$name = 'xyz';
${$name} = 'hallo welt';
// Variablen aus Arrays erstellen
$array = [
  'xyz' => 'Hallo Welt'
];
// Mit schleife
foreach ($array as $key => $value) {
  ${$key} = $value;
}
// Mit Funktione aus der STD-Lib.
extract($array);
```

- können nicht mit Superglobalen Arrays in Funktionen oder Klassenmethoden verwendet werden
- `$this` kann nicht dynamisch referenziert werden

- Verwenden als Variable `${$a[1]}`
- Verwenden als Index dieser Variable (arry) `${$a}[1]`

**Variable Scope**

1. local scope
2. global scope
3. static variable

- [`global`](https://www.php.net/manual/en/language.variables.scope.php#language.variables.scope.global)-Keyword, bindet eine Variable aus dem globalen scope in den lokalen, z.B. in eine Funktion.
- [`extract($array)`](https://www.php.net/manual/de/function.extract.php), Importiert Variablen eines Arrays in die aktuelle Symboltabelle

**Initialisieren**

- bool ist standardmäßig **`false`**
- Ganz- und Gleitkommazahlen sind standardmäßig **`NULL`**
- Zeichenketten und Arrays sind leer
- **HINWEIS:** Es ist problematisch sich auf den Vorgabewert einer nicht initialisierten Variable zu verlassen, wenn Sie eine Datei in eine andere inkludieren, die den gleichen Variablennamen verwendet

- `$this` kann nicht geändert werden
- `isset(mixed $var, mixed ...$vars): bool` — Prüft, ob eine Variable deklariert ist und sich von **null** unterscheidet
- `empty(mixed $var): bool` — Ermittelt ob eine Variable leer ist
- `unset(mixed $var, mixed ...$vars): void` — Zerstört eine Variable
- `var_dump(mixed $value, mixed ...$values): void` — Gibt alle Informationen zu einer Variablen aus
- `print_r(mixed $value, bool $return = false): string|bool`  — zeigt Informationen über eine Variable in menschenlesbarer Form an.
- [Funktionen zur Behandlung von Variablen](https://www.php.net/manual/de/ref.var.php)
- `instanceof` gibt die Klasse eines Objekts zurück

**[NULL](https://www.php.net/manual/de/language.types.null.php)**

- isset($var) liefert false wenn $var null ist

### Referencen

- nur Variablennamen dürfen referenziert werden
- Referenzen werden nicht statisch gespeichert
- **[Sonderfälle bei `global` und `static`](https://www.php.net/manual/de/language.variables.scope.php#language.variables.scope.references)**

```php
$foo = 'Bob';             // 'Bob' der Variablen $foo zuweisen.
$bar = &$foo;             // $foo per $bar referenzieren (ref mut)
$bar = "Ich heiße $bar";  // $bar verändern...
echo $bar;
echo $foo;                // $foo wurde ebenfalls verändert.
```

### [Vordefinierte Variablen](https://www.php.net/manual/de/reserved.variables.php)

- **[Superglobals](https://www.php.net/manual/de/language.variables.superglobals.php)** — Interne Variablen, die immer in allen Gültigkeitsbereichen verfügbar sind
  - Standardmäßig sind alle Superglobals verfügbar, allerdings haben einige Einstellung in PHP Einfluss auf ihre Verfügbarkeit.
  - Superglobals können nicht als variable Variablen innerhalb von Funktionen oder Klassenmethoden verwendet werden.
  - Sie sind in allen Gültigkeitsbereichen (Scopes) eines Skripts verfügbar
  - `$GLOBALS` — Referenziert alle Variablen, die im globalen Gültigkeitsbereich vorhanden sind
  - `$_SERVER` — Informationen über Server und Ausführungsumgebung
  - `$_GET` — HTTP GET-Variablen Array
  - `$_POST` — HTTP POST-Variablen Array
  - `$_FILES` — HTTP Dateiupload-Variablen
  - `$_REQUEST` — HTTP Request-Variablen
  - `$_SESSION` — Sessionvariablen
  - `$_ENV` — Umgebungsvariablen
  - `$_COOKIE` — HTTP Cookies

- `$php_errormsg` — Die vorangegangene Fehlermeldung
- `$http_response_header` — HTTP Response-Header
- `$argc` — Die Anzahl der an das Skript übergebenen Argumente
- `$argv` — Array der an das Skript übergebenen Argumente

### [Variablen aus externen Quellen (HTML-Formulare)](https://www.php.net/manual/de/language.variables.external.php)

- [GET and POST](https://www.php.net/manual/de/language.variables.external.php)
- [HTTP-Cookies](https://www.php.net/manual/de/language.variables.external.php#language.variables.external.cookies)

### [Geltungsbereich von Variablen](https://www.php.net/manual/de/language.variables.scope.php)

- ergibt sich aus dem Zusammenhang, in dem sie definiert wurden
- **`$GLOBALS`** — Als Superglobale in jedem Geltungsbereich verfügbar
- **`global`** — zum verwenden vonglobalen Variablen in loklen Geltungsbereichen, kann auch verwendet werden, eine Datei innerhalb einer Funktion eingebunden wird

```php
$a = 1; // globaler Geltungsbereich
include 'b.inc'; // $a ist in b.inc verfügbar

// globale Variablen sind nicht in Funktionen verfügbar
function test()
{
    echo $a; // Referenz auf ein Variable im lokalen Geltungsbereich

    // so können globale variablen verwendet werden
    global $a, $b;
    $b = $a + $b;

    // alternativ mit $GLOABALS-Array
    $GLOBALS['b'] = $GLOBALS['a'] + $GLOBALS['b'];

}
```

- [**`static`**](https://www.php.net/manual/de/language.variables.scope.php#language.variables.scope.static)
- wird nur beim ersten Aufruf initialisiert
- Statische Deklarationen werden bei der Kompilierung aufgelöst
- werden seit PHP 8.1.0 bei Methoden mit vererbt

```php
function test()
{
    static $a = 0; // nur beim ersten Aufruf der Funktion initialisiert 
    echo $a;
    $a++; // wird bei jedem Funktionsaufruf erhöht
}
function test()
{
    static $count = 0;

    $count++;
    echo $count;
    if ($count < 10) {
        test();
    }
    $count--;
}
```

### Vardump to String

```php
ob_start();
var_dump($someVar);
$str = ob_get_clean();
```

### Isset vs Empty vs Is_null

- [isset()](https://www.php.net/manual/en/function.isset.php) is to check if a variable is set with a value and that value should not be null.
- [empty()](https://www.php.net/manual/en/function.empty.php) is to check if a given variable is empty. The difference with isset() is, isset has null check.
- [is-null()](https://www.php.net/manual/en/function.is-null.php) is to check whether a variable is defined as null.

#### Truth table

|           | “”    | “apple” | NULL  | FALSE | 0     | undefined      | TRUE  | array() | 123   |
| --------- | ----- | ------- | ----- | ----- | ----- | -------------- | ----- | ------- | ----- |
| isset()   | TRUE  | TRUE    | FALSE | TRUE  | TRUE  | FALSE          | TRUE  | TRUE    | TRUE  |
| empty()   | TRUE  | FALSE   | TRUE  | TRUE  | TRUE  | TRUE           | FALSE | TRUE    | FALSE |
| is_null() | FALSE | FALSE   | TRUE  | FALSE | FALSE | Warning / TRUE | FALSE | FALSE   | FALSE |

#### Differences table

| Value of $var           | isset() | empty() | is_null()    |
| ----------------------- | ------- | ------- | ------------ |
| “” (empty string)       | TRUE    | TRUE    | FALSE        |
| ‘apple’ (string value)  | TRUE    | FALSE   | FALSE        |
| null (declaration-only) | FALSE   | TRUE    | TRUE         |
| FALSE                   | TRUE    | TRUE    | FALSE        |
| 0                       | TRUE    | TRUE    | FALSE        |
| undefined  variable     | FALSE   | TRUE    | WARNING/TRUE |
| TRUE                    | TRUE    | FALSE   | FALSE        |
| array() (empty array)   | TRUE    | TRUE    | FALSE        |
| 123 (numeric value)     | TRUE    | FALSE   | FALSE        |

## Datentypen

### Booleans

```php
var_dump((bool) "");        // bool(false)
var_dump((bool) "0");       // bool(false)
var_dump((bool) 1);         // bool(true)
var_dump((bool) -2);        // bool(true)
var_dump((bool) "foo");     // bool(true)
var_dump((bool) 2.3e5);     // bool(true)
var_dump((bool) array(12)); // bool(true)
var_dump((bool) array());   // bool(false)
var_dump((bool) "false");   // bool(true)
```

- `false` wird in einen  leeren String "" konvertiert
- nur die zahl 0 wird zu false ausgewertet
- `AND,OR` hat ein geringere Wertgikeit als `=` !!!, also immer in Klammern verwenden

### Strings

- [String-Funktionen](https://www.php.net/manual/de/ref.strings.php)

```php
$teil = "Teil";
$greeting = 'Hallo Strings';

echo $greeting . " " . "!";
echo 'Hallo $name ! \br'; // singel quotes
echo "Hallo $name ! \n\t";
echo "{$teil}haber";
echo '"Anführungszeichen"';
echo ' \' ';
echo " \" ";
echo " ' ";
// Länger der Zeichenkette
strlen('üü') // = 4 -> Zählt bytes nicht chars!!
mb_strlen('üü') // = 2 -> Zählt chars nicht bytes!!
```

### Arrays

- [Array Funktionen](https://www.php.net/manual/de/ref.array.php)
- [array_diff()](https://www.php.net/manual/de/function.array-diff.php) — Ermittelt die Unterschiede zwischen Arrays

```php
$a = array('Max', 'Erika');
$a = ['Mimm', 'Nymm', 'Max', 'Erika'];
$a[] = 'Samm Kalle'; // Hinzufügen
$a[0] = 'Kall Tonke'; // Überschreiben
$a[100] = 'Kling Gone'; // An Position 100
// Einzelzugriff
print $a[2]; 
$z = 1;
print $a[$z];
// Suchen True/False
in_array('Nymm', $a); 
// Elemente Zählen
count($a);
$a[rand(0, count($a) - 1)];
// Zustand
empty($a); // false
empty($a[99]); // true
isset($a[99]); // false
unset($a[0]); // Array-Variable Löschen
// Doppelte entfernen, kopie erstellen
array_unique($a); 
// Sortiert übergebenen array
sort($a);
// Array - String -Array
$var = array('alpha', 'beta', 'gamma');
implode(', ', $var); // alpha, beta, gamma
$str = "Hallo meine schöne Welt!";
explode(' ', $str); // Array ( [0] => Hallo [1] => meine 
```

**Arrays Entpackn**

```php
// Verwendung der kurzen Array-Syntax.
// Funktioniert auch mit der array()-Syntax.
$arr1 = [1, 2, 3];
$arr2 = [...$arr1]; //[1, 2, 3]
$arr3 = [0, ...$arr1]; //[0, 1, 2, 3]
$arr4 = [...$arr1, ...$arr2, 111]; //[1, 2, 3, 1, 2, 3, 111]
$arr5 = [...$arr1, ...$arr1]; //[1, 2, 3, 1, 2, 3]
```

- Solange ein Arry besteht bleibt der Höchste Integer-Key (Indizierung) erhalten

```php
unset($arr[5]); // Dies entfernt das Element aus dem Array
unset($arr);    // Dies löscht das gesamte Array
$array = array_values($array); // Neue Indizierung
$firstquarter  = array(1 => 'Januar', 'Februar', 'März'); // 1-basierte Indizes
```

#### Assoziative Arrays

- Schlüssel -> Wert - Zuordnungen
- Keys Integer oder String,
  - gültige Ganzzahlen, floats und bools  werden in integer umgewandelt, null wird zum String ""
  - Array und Objecte als Keys sind unzulässig
  - gleichnamige keys werden überschrieben
  - wenn kein Key angegeben wird wirde der bisherig größte int key erhöt
- Zugriff auf nicht definirte schlüssel gibt null zurück
- String und Integer Keys können gleichzeitig vorliegen
- Value ist beliebig
- Zugriff ist performant
- [array_keys()](https://www.php.net/manual/de/function.array-keys.php)  — Liefert alle Schlüssel oder eine Teilmenge aller Schlüssel eines Arrays
- [array_values()](https://www.php.net/manual/de/function.array-values.php) — Liefert alle Werte eines Arrays

```php
$a = [
    'ban', // besser nicht mischen
    'app' => 'App',
    'ora' => 'Apf'
];
// Zugriff über Key $a[2] geht hier nicht
$a['app'];
// Alle Schlüssel als neuer Array
array_keys($a);
// Alle Werte als neuer Array
array_values($a);
```

#### Foreach und Arrays

```php
foreach ($a as $name) {
    if ($name === 'Max') continue; // Schleifendurchlauf wird übersprungen
  if ($name == 'Nymm') break; // Schleife wird abgebrochen
    echo $name.'<br>';
}
```

**mit php tag**

```php
<?php foreach ($a as $name): ?>
  <p><?php echo $name ?></p>
  <?php endforeach?>
```

**für assoziativ array**

```php
foreach ($a as $key => $value) {
    var_dump($key);
    var_dump($value);
}
```

#### Array Destrukturierung

- [each()](https://www.php.net/manual/de/function.each.php) - Liefert das aktuelle Schlüssel-Wert-Paar eines Arrays und rückt den Arrayzeiger vor
- [array()](https://www.php.net/manual/de/function.array.php) - Erstellt ein Array
- [extract()](https://www.php.net/manual/de/function.extract.php) - Importiert Variablen eines Arrays in die aktuelle Symboltabelle

```php
// Array Erstellen
$source_array = ['foo', 'bar', 'baz'];
// Destrukturieren
[$foo, $bar, $baz] = $source_array;
[, , $baz] = $source_array;

foreach ($source_array as [$foo, $bar, $baz]) {
    // der Code mit $foo, $bar und $baz
}

// Mit assoziativen Arrays
$source_array = ['foo' => 1, 'bar' => 2, 'baz' => 3];
foreach ($names as ['name' => $name, 'year' => $year, 'count' => $count]) {
// Zuweisen des Elements bei Index 'baz' an die Variable $three
['baz' => $three] = $source_array;
[2 => $baz] = $source_array;

// Variablen Tauschen
$a = 1;
$b = 2;
[$b, $a] = [$a, $b];
```

### Konstanten

**define**

```php
define('APP_PATH', __DIR__);
define('PUBLIC_PATH', __DIR__ . '/public');
```

### [Compile-time constants](https://www.php.net/manual/en/reserved.keywords.php)

- `__CLASS__`,`__DIR__`,`__FILE__`,`__FUNCTION__`,`__LINE__`,`__METHOD__`,`__NAMESPACE__`,`__TRAIT__`

## Kontrolltrukturen / Verzweigungen

```php
<?php if (condition): ?>
/* html code to run if condition is */ true
<?php else: ?>
/* html code to run if condition is */ false
<?php endif ?>
```

## Funktionen

- Es gibt keine Funktionüberladung
- Default Werte für Parameter machen Parameter übergabe optional
- snake_case ist best practice
- return beendet die Funktion
- **Redeklaration vermweiden** mit [function_exists](https://www.php.net/manual/de/function.function-exists.php)
- Typenannotation verhinder Ausführung von Funktionen mit falschem Datentyp, kann Fehler verhindern
  - Führ wo immer möglich Typeconversion aus
- Typeannotation für return values kann Fehler verhindern

```php
// ?string accepts Null
function f(?string $str = "_", int $count = 3)
{
  for ($i = 0; $i < $count; $i++) {
    print_r("str: $str | count:" . $count . "\n");
  }
}
f(); # str: _ | count:3
f(null); # str:  | count:3
f('Hallo'); #str: Hallo | count:3
f(2.4, 2); #str: 2.4 | count:2

// Avoid redclaration 
// Enforce Retrurnvalue
if (!function_exists('add_numbers')) :int {  
  // Mit Default Paramaterwerten und Typanotation
  function add_numbers(int|float $number1 = 1, int|float $number2 = 1)
  {
    if (($number1 == 0) || $number2 == 0) {
      return 0; // Funktionsausführung ended hier 
    }
    return $number1 + $number2;
  }
}
// Optionale Parameterübergabe
add_numbers(); // 2
add_numbers(2); // 3
add_numbers(2,2); // 4
```

## Anonyme Funktionen - Closures

```php
function execute($func) {
    $func();
}

function f() {
    $name = 'Max Müller';

    # Access variables from parent scope with use
    execute(function() use($name) {
    // execute(function() { # Undefined variable $name
        var_dump($name);
        var_dump("Funktion wird ausgeführt");
    });
}
f();
```

## Objektorientierung

- Datenkapselung durch public und private setzten von Eigenschaften
  - mit private kann man Funktionalität explizit verhindern
  - mit private Zugang nur über setter und getter methoden um unqualifiziertes ändern der daten eines Objektes zu verhindern Zb ändern eines Wertes durch puplic-Zugriff ohne dabei die Datenbank darüber zu Informieren, eine Funktion die der Setter implementiert.
  - ! Klassen nur einmal includen `require_once`
- `get_class()` Ermittelt die Klasse eines Objekts
- geht auch mit return values

### public, protected, private

- **public** can be accessed everywhere.
- **protected** can be accessed only within the class itself and by inheriting and parent classes. 
- **private** may only be accessed by the class that defines the member.

### OOP - Klassen

- Klassennamen ausgeben mit `PagesModel::class`

```php
 class BankAccount
{
  // Kurzschreibweise
  function __construct(private string $iban, private float $balance)
  {
  }
  // public string $iban;
  // public float $balance;

  // function __construct(string $iban, float $balance)
  // {
  //   $this->iban = $iban;
  //   $this->balance = $balance;
  // }

  // default visibility für Methoden ist public
  public function printBalance()
  {
    echo "$this->iban :: $this->balance&euro;\n";
  }

 function sepa(BankAccount $to, $amount)
  {
    if ($amount > $this->balance) {
      echo "Guthaben reicht nicht aus!";
      return;
    }
    echo "Überweisung von $this->iban zu $to->iban\n";
    $this->balance -= $amount;
    $to->balance += $amount;
    $this->logBalance();
  }

  // invisible logging
  private function logBalance(){
    echo "$this->iban :: $this->balance&euro;\n";
  }

  // Getter und Setter
  function getIban()
  {
    return $this->iban;
  }

  function getBalance()
  {
    return $this->balance;
  }

  function atmPayIn($amount)
  {
    $this->balance += $amount;
  }
}

$account1 = new BankAccount('DE17234932876', 75349);
$account1->printBalance();
$account2 = new BankAccount('AT752304987432', 43278);
$account2->printBalance();
$account1->sepa($account2, 500);
 ```

### OOP - Interfaces

```php
interface Person {
    public function getAge(): int;
}

class Student implements Person {
    public function getAge(): int {
        return 21;
    }
}

class Teacher implements Person {
    public function getAge(): int {
        return 40;
    }
}

function printAgeOf(Person $person) {
    echo 'Diese Person ist ' . $person->getAge() . ' Jahre alt.'."\n";
}

$s = new Teacher();
printAgeOf($s);

var_dump($s instanceof Person);

if ($s instanceof Person) {
    var_dump($s->getAge());
}
```

#### Traits vs Interfaces

- **Traits** provide horizontal reuse of methods: a class that uses a trait mixes in the implementation of a set of methods. 
- **Interfaces** provide a promise of a class's implementation: a class that implements an interface is guaranteed to provide a set of methods.

### OOP - Vererbung

- Überschriebene Methoden müssen diegleiche Signatur haben, wie Elternklasse
- Wenn kein Konstruktor vorhenden, wir der von der Elternklasse genommen
- Paren Classe should not access properties of child classes
- Paren Classe can access methods of child classes

```php
class Animal
{
    private string $color;
    private float $weight;
    protected float $length;

    public function __construct(float $weight)
    {
        $this->weight = $weight;
        echo "Ein neues Animal wurde erstellt...\n";
    }
    public function eat($point)
    {
        echo "Animal::eat() \t $point\n";
    }
    public function move($point)
    {
        echo "Animal::move() \t $point\n";
    }
    public function callEat()
    {
        # Mathod call to Animal::eat()
        self::eat('self::eat');
        # Method call to potential Child class
        $this->eat('$this->eat');
    }
}

class Dog extends Animal
{
    private float $weight; # Duplicate private propertie not recommended but possible
    public string $name;

    public function __construct(float $weight, string $name)
    {   # Optional call to parent::contructor if needed
        parent::__construct($weight);
        $this->name = $name;
        $this->weight = 30;
        echo "Ein neuer Dog wurde erstellt...\n";
    }
    public function bark($point)
    {
        echo "Dog::bark() \t $point \t $this->name $this->weight\n";
    }
    # Overrides parrent::move($point)
    public function move($point)
    {
        # Method call to Dog::bark()
        $this->bark('$this->bark');
        # Method call to Dog::bark()
        self::bark('self::bark');
        # Method call to Animal::eat()
        parent::eat('parent::eat');
        echo "Dog::move() \t $point \t $this->name $this->weight\n";
    }
    public function eat($point)
    {
        echo "Dog::eat() \t $point \t $this->name $this->weight\n";
    }
}
$d = new Dog(20, 'Fridolin');
$d->bark('$d->bark');
$d->eat('$d->eat');
$d->move('$d->move');
$d->weight = 10; #Cannot access private property Dog::$weight
$d->name = 'Wausch';
$d->color = "white"; # Will be created if not protected
$d->length = 32; # Cannot access protected property Dog::$length
$d->callEat();
```

### OOP - Abstract Classes

- Abstrakt definierte Klassen können nicht instantiiert werden
- Jede Klasse, die wenigstens eine abstrakte Methode enthält, muss ebenso abstrakt sein
- Abstrakt definierte Methoden deklarieren nur die Signatur der Methode - sie können nicht die Implementierung definieren
- es gelten die blichen Vererbungs-Regeln

```php
abstract class Car
{
    # Must be implemnted from child
    # Can be public, private, protected
    abstract protected function getConsumptionValue();
    # Shared Methods
    public function printCosumption()
    {
        echo "Verbrauch: " . get_class($this) . " {$this->getConsumptionValue()}";
    }
}
class ElectricCar extends Car
{
    protected function getConsumptionValue()
    {
        return  "20kwh/100km";
    }
}

$e = new ElectricCar();
$e->printCosumption();
$h = new Car(); # Cannot instantiate abstract class Car
```

### OOP - Statische Funktionen

- sollten nur für klassenspezifische Hilfsfunktionen verwendet werden

```php

class Image {

    public static $a = 'Hallo Welt';

    public static function resize($a) {
        var_dump('Das Bild wird skaliert...');
        var_dump($a);
    }
}

Image::resize('Parameter...');
var_dump(Image::$a);
```

### OOP - Magic Methodes

- werden dann aufgerufen wenn es die Eigenschaft nicht gibt
- `__get()`, `__set()` ermöglichen abweichende interne repräsentation
- `__isset()` eingene implemntation, zb weiterleitung an Datenbank

```php
class PageModel {

    // public function __construct(public string $title = 'Hallo') {}

    public function __construct(public array $attributes = []) {}

    public function __get($name) {
        return $this->attributes[$name];
    }

    public function __set($name, $value) {
        // var_dump($value);
        $this->attributes[$name] = $value;
    }

    public function __isset($name) {
        return isset($this->attributes[$name]);
    }
}

$page = new PageModel([
    'title' => 'Hallo Welt'
]);
var_dump($page->title);

$page->title = 'Hallo Mars';

var_dump(isset($page->title));

```

### OOP - Konstanten

```php
class ImageHelper {

    public const QUALITY_LOW = 20;
    public const QUALITY_MEDIUM = 50;
    public const QUALITY_HIGH = 80;

    public static function resizeImage($a, $quality = 80) {
        var_dump($a);
        var_dump($quality);
    }
}

var_dump(ImageHelper::QUALITY_LOW);

ImageHelper::resizeImage("........", ImageHelper::QUALITY_MEDIUM);
```

### OOP - Static

- Eine statische Variable existiert nur in einem lokalen Funktions-Geltungsbereich, der Wert geht beim Verlassen dieses Bereichs aber nicht verloren.
- Klasseneigenschaften oder -methoden als statisch zu deklarieren, macht diese zugänglich, ohne dass man die Klasse instantiieren muss.
- Auch innerhalb eines instantiierten Klassenobjekts kann statisch auf sie zugegriffen werden. 
- Anonyme Funktionen können statisch deklariert werden. Dies verhindert, dass die aktuelle Klasse automatisch an sie gebunden wird. Objekte können zur Laufzeit ebenfalls nicht an sie gebunden werden.
- `$this` ist nicht in statischen Methoden verfürbar

```php
class Image {
    
    public static $a = 'Hallo Welt';

    public static function resize($a) {
        var_dump('Das Bild wird skaliert...');
        var_dump($a);
    }
}

// $i = new Image();
// $i->resize('Parameter');

Image::resize('Parameter...');
var_dump(Image::$a);
```

### OOP - Singelton Pattern

- Verhindert das es mehrere Instanzen von einem Object gibt, das in der Ausführung aber nur einmal vorkommen sollte

```php
class Container {

    private function __construct() {}

    private static $instance = null;

    public static function getInstance() {
        if (empty(self::$instance)) {
            // self::$instance = new Container();
            self::$instance = new self();
        }
        return self::$instance;
    }
}

$c1 = Container::getInstance();
$c2 = Container::getInstance();

var_dump($c1);
var_dump($c2);
```

## Namespaces

- Könne verschachtelt sein

```console
C:.
│   index.php
│
└───src
    ├───Admin
    │       Role.php
    │       User.php
    │
    └───User
            User.php
```

**./index.php**

```php
namespace MeineApp;
// Groß- und Kleinschreibung beachten
use MeineApp\Admin\User; // Klassen können jetzt als User verwendet werden
use MeineApp\User\User as UUser;

require_once __DIR__ . '/src/User/User.php';
require_once __DIR__ . '/src/Admin/User.php';
require_once __DIR__ . '/src/Admin/Role.php';

$u = new User();
$u->printName();

// vom Globalen Namespace ausgenen, nicht vom Namspace Admin
$u2 = new \MeineApp\User\User();
$u2->printName();

$u3 = new UUser();
$u3->printName();;
```

**User/User.php**

```php
// gleicher name wie übergeorneter Ordner ist best practice
namespace MeineApp\User;
use MeineApp\Admin\Role;

class User {
    public function printName() {
        $role = new Role();
        echo 'printName() von der Klasse User/User wurde aufgerufen';
    }
}
```

**Admin/User.php**

```php
// gleicher name wie übergeorneter Ordner ist best practice
namespace MeineApp\Admin;

// Aus Globalen Namspace importieren
use PDO;

class User {
    public function printName() {
        $pdo = new PDO();

        $role = new Role();
        echo 'printName() von der Klasse Admin/User wurde aufgerufen';
    }
}
```

**Admin/Role.php**

```php
namespace MeineApp\Admin;

class Role {

}
```

## Autoloading

-**HINWEIS:** Es müssen die Namespaces und die Pfade der Dateien übereinstimmen

```php
// Wird aufgerufen, wenn eine Klasse nicht geladen ist
spl_autoload_register(function ($class) {
  $file = __DIR__ . '/src/' . str_replace('\\', '/', $class . '.php');
  file_exists($file) and require_once $file;
});
```

### PSR-4 (PHP Standard Recommentation) Improved Autoloading

- namespace für die gesamte Anwendung anlegen um namespaces anderer Module leichter importieren zu können

```php
# index.php
namespace MeineApp;
# Admin.php
namespace MeineApp\Admin;
# User.php
namespace MeineApp\User;

# Autoloader

spl_autoload_register(function ($class) {

    // project-specific namespace prefix
    $prefix = 'App\\';

    // base directory for the namespace prefix
    $base_dir = __DIR__ . '/../src/';

    // does the class use the namespace prefix?
    $len = strlen($prefix);
    if (strncmp($prefix, $class, $len) !== 0) {
        // no, move to the next registered autoloader
        return;
    }

    // get the relative class name
    $relative_class = substr($class, $len);

    // replace the namespace prefix with the base directory, replace namespace
    // separators with directory separators in the relative class name, append
    // with .php
    $file = $base_dir . str_replace('\\', '/', $relative_class) . '.php';

    // if the file exists, require it
    if (file_exists($file)) {
        require $file;
    }
});
```

## Exceptions

```php
class InvalidUserException extends Exception {}
class TitleTooShortException extends Exception {}

function edit_page($user, $title) {
    if ($user !== 'author') {
        throw new Exception('Der Benutzer ist nicht "author".');
    }
    if ($user !== 'admin') {
        throw new InvalidUserException('Der Benutzer ist nicht "admin".');
    }
    if (strlen($title) < 3) {
        throw new TitleTooShortException('');
    }

    // Seite wird editiert
    return true;
}

try {
    edit_page('admin', 'S');
}
catch (Exception $e) {
    var_dump("Es ist ein Fehler aufgetreten");
    var_dump($e->getMessage());
}
catch (InvalidUserException $e) {
    var_dump("Es ist ein Fehler aufgetreten");
    var_dump($e->getMessage());
}
catch (TitleTooShortException $e) {
    var_dump("Der Titel ist zu kurz...");
}
```

## [Output Kontrolle](https://www.php.net/manual/de/ref.outcontrol.php)

```php
ob_flush(); // Gepufferte Ausgaben absenden

// beginnt das Puffern
ob_start();
...
// Header können später gesetzt werden
header('Content-Type: text/plain');
...
// Output Puffer in Variable Umleiten
$content = ob_get_contents();
// Ausgabepuffern beenden
ob_end_clean();

var_dump($content);
```

- ob_clean — Löscht den Inhalt des aktiven Ausgabepuffer
- ob_flush — Leert (sendet) den Rückgabewert des aktiven Ausgabe-Handlers
- ob_start — Ausgabepufferung aktivieren
- ob_get_length — Return the length of the output buffer
- ob_end_clean — Löscht den Inhalt des aktiven Ausgabepuffers und deaktiviert ihn
- ob_end_flush — Leert (sendet) den Rückgabewert des aktiven Ausgabe-Handlers und deaktiviert den aktiven Ausgabepuffer

## HTTP QUERIES

- http_build_querry()

```php
var_dump($_GET);

print('<hr>');

// Build query
// http://localhost/?id=hallo-welt&zweidi=wert

$query = http_build_query(['Max & Moritz !']); // Max+%26+Moritz+!=0=Max+%26+Moritz+!
// array(1) { ["Max_&_Moritz_!"] => string(16) "0=Max & Moritz !" }
var_dump($query);

?>
</pre>
<a href="index.php?<?php echo $query; ?>">Max und Moritz</a> 
```

## HTTP Header

- können nur gesendet Werden bevor andere Daten an den Browser übertragen wurden
- PHP verwenden Output-Buffering, d.h. es werden est daten versendet wenn eine bestimmte Menge an Bytes zusammen gekommen sind

**Custom Header**

```php
header("X-mein-header: digs hehe");
```

**Content type bestimmen**

```php
header("Content-type: text/plain"); // Die Seite wird dann vom Browser wie plain text behandelt
header("Content-type: text/html");
// Oder zum generieren von CSS
<?php header("Content-type: text/css") ?>
body {
  background-color: rgb(<?=rand(0, 255)?>, <?=rand(0, 255)?>, <?=rand(0, 255)?>);
}
```

**redirects**

```php
// PHP wird weiter ausgeführt, aber Browser schon weiter geleitet
// Response code je nach Fall, aber für Std-Konformen Code, und SEO bei zb. Domänen-Umzug
http_response_code(301); // Moved Permanently 
header("Location: http://localhost/index.php");
die(); // um asführung des PHP-Scripts zu beenden
```

## Sessions

- eine Datei die auf dem Server gespeichert wird
- der browser erhält nur die id davon
- acceps only serialzeable data

```php
# Jede Datei die session_start aufruft hat CRUD-Zugriff auf die Session Cookies
session_start(); # PHPSESSID=ec49j4i2h7tjg8ngmq2iqbdvgt; path=/
$_SESSION['name'] = 'Max Musterman'; 

var_dump($_SESSION);
var_dump(session_save_path());
```

## Cookies

- `$_COOKIE` Enthält nur Cookies die der Browser mitschickt
- Solange keine geschcikt wurden ist er lehr, und nach dem setcookie()
- muss erst eine neue Anfrage vom browser kommen, das der cookie mitkommt
  - Output Buffering beachten

```php
var_dump($_COOKIE);
# Erstellt Cookies die zuerst an den browser gesender werden
setcookie('abc', 'xyz', 0); # Sitzungskookie, wird gelöscht wenn browser geschlossen
setcookie('abc', 'xyz', time() + 3600); # ist für 1h gültig
setcookie('abc', 'xyz', time() + 24 * 60 * 60 * 31); # ist für 1 Monat gültig
setcookie('abc', '', time() - 3600); # Wird vom Broser sofort gelöscht

# @pfad #  damot bezieht sich der cookie immer auf einen bestimmten pfad
setcookie('abc', 'xyz', 0, '/'); # für gesamten pfad gültig
```

## MySQL und PDO

- Tabellennamen
  - nur Kleinbuchstaben
  - und unterstriche
- **BEST PRACTICE** Spaltennamen nie wie Keywords
- **BEST PRACTICE** Spaltennamen am besten immer im snake_case
  - um Spaltennamen immer Backticks `user`
- Daten-Konsistenz-check über länger der Strings varchar(10)
- Daten-Konsistenz über Primärschlüssel
- Schnellerer Datenzugriff über Indizes, dafpr aber C,U,D langsamer
  - Indexe werden von vorn her augebaut (Strings)
  - `SELECT ... M%` -> Query kann den Index verwenden
  - `SELECT ... %ann%` -> Query kann den Index nicht mehr verwenden
  - Bei strings für  SQL-Querries kein `_` und `%` zulassen

### PDO - PHP Data Object

- Ein Datenbank [Treiber](https://www.php.net/manual/de/pdo.drivers.php)
- leichte, konsistente Schnittstelle bereit, um mit PHP auf Datenbanken zuzugreifen
- **[Prepare Statements](https://www.php.net/manual/de/pdo.prepared-statements.php)**

```php
// Instantiate a POD-Object
$pdo = new PDO('mysql:host=localhost;dbname=php_kurs', 'root', '', [
    // Throws exception if error occures
    PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION
]);
// Prepare statement
$stmt = $pdo->prepare('SELECT * FROM `news` ');
// best practice mit Platzhalter und bind Value
$stmt = $pdo->prepare('SELECT * FROM `news` WHERE `id` = :id');
// Fill placeholder with value
$stmt->bindValue(':id', $id, PDO::PARAM_INT); // separate call for each place holder annotate types otherwise it will be a string
// Execute Statement
$stmt->execute();
// Return the ID of the last inserted row or sequence value
echo $pdo->lastInsertId();
// Getting buffered result
$results = $stmt->fetch(PDO::FETCH_ASSOC); // nur ein Eintrag
$results = $stmt->fetchAll(PDO::FETCH_ASSOC); // alle Einträge
```

### PDO - Fetch in to Class

```php
$stmt = $this->pdo->prepare('SELECT * FROM `images` ORDER BY id');
$stmt->execute();
// Spalten namen müssen identisch sein mit variablen namen
// sonst fetch array verweden und händisch zuweisen
return $stmt->fetchAll(PDO::FETCH_CLASS, GalleryImageModel::class);
```

### MYSQL - Storage Engines

- InnoDB -> Blockiert Zugriff auf Zelle  bei Update
- MyISAM -> Blockiert Zugriff auf ganze Tabelle bei Updates

### MYSQL - InnoDB - Tranaktionen

- `PDO::Transaction`

## Sicherheit

- adminbereich immer https verschlüsselt !

### Sicherheit bei Formularen

- **HTML-Tags Entfernen**

  ```php
  // Strip HTML Tags
  strip_tags($_GET['search']);

  // Zeichen Allow List
  $search = preg_replace("/[^A-Za-z0-0\ \.öäüßÖÄÜ,]/", '', $search);

  if (empty($search) || strlen($search) < 3) {
    return null;
  }
  ```

  - Bei strings für  SQL-Querries kein `_` und `%` zulassen

### Sicherheit bei Nutzereingaben

- **Bei Ausgabe von Nutzereingaben [HTML Sonderzeichen umwandeln](https://www.php.net/manual/de/function.htmlspecialchars.php)**

  ```php
  function hsc($html)
  {
      // &,",',<,>
      return htmlspecialchars($html, ENT_QUOTES, 'UTF-8', true);
  }
  ```

- **allowlist für select tags**
- **Typen-Abfragen für alle Nutzereingaben**
  - is_string, is_array, is_bool, is_uploaded_file
  - Können Daten auf der meine Logik basiert vom Nutzer verändert werden, wenn ja was brauch ich um es zu sichern?
  - Strings auf Zeichen-Art prüfen mit [Ctype-Funktions](https://www.php.net/manual/de/ref.ctype.php)
- **Type Casting**
  - Validieren von Eingaben

### Passwortsicherheit

- schlecht: Kurze berechnungszeit (md5, sha1)
- Regenbogentabellen (Liste von Passwort hashes)
`passwort_hash()`
`passwort_verify()`

```php
$password = password_hash('top-secret', PASSWORD_DEFAULT);
$input = 'top-secret...';
$password;
password_verify($input, $password);
```

### SQL-Sicherheit

- **[SQL-Injection](https://www.php.net/manual/de/security.database.sql-injection.php)**
- Stellen Sie nie als Superuser oder Eigentümer einer Datenbank eine Verbindung zur Datenbank her. Verwenden Sie immer speziell angelegte Benutzer mit sehr limitierten Rechten.
- Prüfen Sie, ob die gegebene Eingabe dem erwarteten Datentyp entspricht. [Variablenfunktionen](https://www.php.net/manual/de/ref.var.php), [Character-Type-Funktionen](https://www.php.net/manual/de/ref.ctype.php)

- **PDO-Exceptions Abfangen**

  - to not leake DB-Access data
  - to not inform petential attacker about anything

  - ```php
      try {
        $pdo = new PDO('mysql:host=localhost;dbname=php_kurs', 'root', '', [
            PDO::ATTR_ERRMODE => PDO::ERRMODE_EXCEPTION
        ]);
        } catch (PDOException $err) {
            echo "Fehler: bei der Datenbankverbindung.";  // <-- SAVE NO LEAK
            // print_r($err);  // <-- UNSAVE
            // echo $err->getCode();  // <-- UNSAVE
            // echo $err->getMessage();  // <-- UNSAVE
            die();

        }
    ```

- **Nutzereingaben behandeln**

```php
// Maximale Vorsicht beim übernehmen von Nutzereingaben
if (!empty($_POST)) {
  $name = @(string) ($_POST['name'] ?? '');
  $title = @(string) ($_POST['title'] ?? '');
  $content = @(string) ($_POST['content'] ?? '');

  if (!empty($name) && !empty($title) && !empty($content)) {
    $stmt = $pdo->prepare('INSERT INTO entries (`name`,`title`,`content`,`time`) VALUES (:name, :title, :content, :time)');
    $stmt->bindValue('name', $name, PDO::PARAM_STR);
    ...
    $stmt->execute();
    echo '<a href="index.php">Nun aber zur&uuml;ck zum G&auml;stebuch!</a>';
    die();
  }
}
echo '<H4>Es ist ein Fehler aufgetreten...</H4>';
```

## BestPractice

### Code Strucktur

- Logik und View strickt trennen
  - Bussinuess Logik scripts haben maximal debug ausgeben und logging
  - View Scripts übernehmen alle Ausgaben

### MCV - Pattern

## Examples

### Time

- PHP verwendet die Zeitzohne vom darunterliegendem System
`- date_default_timezone_set('UTC');`

```php
date_default_timezone_set('UTC'); # Set the default Timzone to use
$d = time(); # Unix timestamp - NOW!
$d = mktime(12, 4, 5, 12, 20, 2050); # Timstamp from Date
date('Y-m-d', $d); # Convert to human readable Timestamp
date("H:i", time());
$currentDate = gmdate('h:m:s Y-m-d', $timestamp);
```

### Ordner auslesen

```php
$files = [];
$handel = opendir(__DIR__ . '/img');
$files[] = readdir($handel)); // 
$files[] = readdir($handel)); // 
// ...
// oder

// Anweisungen haben ihren eigenen Wert, den wert zu dem sie Ausgewertet werden
while (false !== ($file = readdir($handel))) {
    if (str_starts_with($file, ".")) {
        continue;
    }
    $files[] = $file;
}
// Unix Systeme begrenzen die Menge an IO-Operationen, daher file_handles immer schließen
closedir($handel);
```

### PHP Formulare

- **Best Practice**: `GET`-Method für READ operation
- **Best Practice**: `POST`-Mehtod für CREATE, UPDATE; DELETE operationen
- Tag-Eigenschaft `minlength="3"` für input-Felder
- **Limit für Dateiuploads**
  - max_file_size -> php_ini
  - posts_max_size -> php_ini

### GET - Formular

- für Aufrufe als visual Feedback für den Nutzer

```html
<form action="arrays-02.php" method="GET">
    <fieldset>
        <label for="firstname">firstname</label>
        <!-- EXTREME UNSAFE CODE FOLLOWING!! -->
        <input type="text" name="firstname" value="<?php if (!empty($_GET['firstname'])) {
        echo $_GET['firstname'];
        }
        ?>" />
            <label for="lastname">lastname</label>
        <input type="text" name="lastname" value="<?php if (!empty($_GET['lastname'])) {
            echo $_GET['lastname'];
        }
        ?>" />
        <input type="submit" value="Abschicken" />
        <br>
        <?php echo 'GET: ';
        var_dump($_GET) ?>
    </fieldset>
</form>
```

### POST - Formular

- immer dann verwenden wenn man daten verändert, auch löschen von einträgen in der datenbank

```html
<form action="arrays-02.php" method="POST">
    <fieldset>
        <label for="firstname_p">firstname</label>
        <!-- EXTREME UNSAFE CODE FOLLOWING!! -->
        <input type="text" name="firstname_p" value="<?php if (!empty($_POST['firstname_p'])) {
            echo $_POST['firstname_p'];
        }
        ?>" />
            <label for="lastname_p">lastname</label>
            <input type="text" name="lastname_p" value="<?php if (!empty($_POST['lastname_p'])) {
            echo $_POST['lastname_p'];
        }
        ?>" />
        <input type="submit" value="Abschicken" />
        <br>
        <?php echo 'POST: ';
        var_dump($_POST) ?>
    </fieldset>
</form>
```

### Render Funktion

```php
function render($path, array $data = []) {
   ob_start();
   extract($data);
   require $path;
   $content = ob_get_contents();
   ob_end_clean();
   # Content steht in main.view.php zur verfügung
   require __DIR__ . '/../views/layouts/main.view.php';
}
```

### Container - Pattern

```php
class Container {
    protected $receipts = [];
    protected $instances = [];

    public function add(string $key, \Closure $func) {
        $this->receipts[$key] = $func;
    }

    public function get($what) {
        if (!isset($this->instances[$what])) {
            $this->instances[$what] = $this->receipts[$what]();
        }
        return $this->instances[$what];
    }
}
```

## Reguläre Ausdrücke

- [Reguläre Ausdrücke - PCRE (Perl Compatible Regular Expression)](https://www.php.net/manual/de/book.pcre.php)
- [Niederschrift zu Regex](./regex.md)

```php
# CHARACTER CLASSES
$text = 'Hallo Welt';
strpos($text, 'Welt'));// int(6)
preg_match('/Welt/', $text);// int(1)
// Die Ziffern:0-9
preg_match('/\d/', $text); // int(0)
// Alle Zeichen bis auf: 0-9
preg_match('/\D/', $text); // int(1)
// White-Space, Leerzeichen, Tabulatoren, Zeilenumbrüche...
preg_match('/\s/', $text); // int(1)
// Alles bis auf \s
preg_match('/\S/', $text); // int(1)
// Kleinbuchstaben, Großbuchstaben, Ziffern, Unterstriche...
preg_match('/\w/', $text); // int(1)
// Alles bis auf \w
preg_match('/\W/', $text); // int(1)

# KOMBINATION

preg_match('/\dOrangen/', '3Orangen'); // int(1)
preg_match('/\d\sOrangen\s\d/', '3 Orangen 7'); // int(1)
preg_match('/\d/', 'Hallo 123', $matches); // int(1)
// var_dump($matches); // array(1) {[0]=>string(1) "1"}

# QUANTIFIER

// Findet etwas, weil eine Ziffer auch 0x vorkommen darf
preg_match('/\d*/', 'Hallo 123 Welt...', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(0) "" } 

preg_match('/\d*/', '4132 Hallo 123', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(4) "4132" } 

preg_match('/\d+/', 'Hallo 123', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(3) "123" } 

preg_match('/Hallo?/', 'Hallo Welt', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(5) "Hallo" } 

preg_match('/apples?/', 'apple, oranges', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(5) "apple" } 

preg_match('/apples{0,1}/', 'apple, oranges', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(5) "apple" }

# META CHARACTERS

preg_match('/^H/', 'hallo', $matches); // int(0)
// var_dump($matches); // array(0) { }

preg_match('/^H/', 'Hallo', $matches)); //int(1)
// var_dump($matches); // array(1) { [0]=> string(1) "H" }

preg_match('/^H/', ' Hallo', $matches); // int(0)
// var_dump($matches); // array(0) { }

preg_match('/^.H/', ' Hallo', $matches)); //int(1)
// var_dump($matches); // array(1) { [0]=> string(2) " H" }

preg_match('/^.H/', '  Hallo', $matches); // int(0)
// var_dump($matches); // array(0) { }

preg_match('/^.*H/', '  Hallo', $matches)); //int(1)
// var_dump($matches); // array(1) { [0]=> string(3) " H" }

# VALIDATE EMAILADRESS

preg_match('/^.+@.+\..+$/', 'hallo@welt.de', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(13) "hallo@welt.de" } 

preg_match('/^\S+@.+\.\S+$/', 'sdfg hallo@welt.de sdfg', $matches); // int(0)
// var_dump($matches); // array(0) { } 


# VALIDATE DATUM

// ^ und $ wichtig fpr Serverseitiges validieren
preg_match('/^\d{2}.\d{2}.\d{2,4}$/', '08.11.24', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(8) "08.11.24" }

preg_match('/^\d{2}.\d{2}.\d{2,4}$/', '08.11.2024', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(10) "08.11.2024" } 


# CHARACTER GROUPS

preg_match('/[A-Z]/', 'HAllo Welt', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(1) "H" }

preg_match('/[a-z]/', 'Hallo Welt', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(1) "a" }

preg_match('/[a-zäöü]/', 'Hällo Welt', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(1) "ä" }

preg_match('/[a-z]+/', 'Hallo Welt', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(4) "allo" }

preg_match('/[0-9]+€/', 'Ein Apfel kostet 10€', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(3) "10€" }

preg_match('/[0-9]+[ ]?€/', 'Ein Apfel kostet 10 €', $matches); // int(1)
preg_match('/[0-9]+ ?€/', 'Ein Apfel kostet 10 €', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(4) "10 €" }

preg_match('/^[a-zA-Z\,\-0-öÖäÄüÜß]+\@gmail.com$/', 'fjsadölfk@gmail.com', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(19) "fjsadölfk@gmail.com" }

preg_match('/\@gmail.com$/', 'fjsa+dölfk@gmail.com', $matches); // int(1)
// var_dump($matches); // array(1) { [0]=> string(10) "@gmail.com" }


# CAPTURE GROUPS

preg_match('/(.*)\@(.*)/', 'hallo@gmail.com', $matches); // int(1)
// var_dump($matches); // array(3) { [0]=> string(15) "hallo@gmail.com" [1]=> string(5) "hallo" [2]=> string(9) "gmail.com" } 

preg_match('/^(https?)/', 'https://www.google.com', $matches); // int(1)
// var_dump($matches); // array(2) { [0]=> string(5) "https" [1]=> string(5) "https" } 

//  Performanter ist aber:
var_dump(str_starts_with('https://www.google.com', 'https://')); // bool(true) 

PREG_REPLACE

preg_replace('/l/', '-', 'Hallo Welt!'); // string(11) "Ha--o We-t!" 
// Mit Limit
preg_replace('/l/', '-', 'Hallo Welt!', 1); // string(11) "Ha-lo Welt!" 
preg_replace('/[a-z]/', '-', 'Hallo Welt!'); // string(11) "H---- W---!" 
preg_replace('/[^a-z]/', '-', 'Hallo Welt!'); // string(11) "-allo--elt-" 
preg_replace('/^.+\@/', '', 'learn@gmail.com'); // string(9) "gmail.com" 
preg_replace('/^.+\@.+/', '', 'learn@gmail.com'); // string(0) "" 
preg_replace('/(^.+)\@(.+)/', '$2@$1', 'learn@gmail.com'); // string(15) "gmail.com@learn" 

$search = '!!Hal,:lo& W-e_lt%';
preg_replace('/[^a-zA-Z0-9 ]*/', '', $search); // string(10) "Hallo Welt"
$email = preg_replace('/\@googlemail.com/', '@gmail.com', $email);
$email = preg_replace('/([a-zA-Z0-9]+)(\+\w+)\@/', '$1@', $email);
```

## .htaccess

- Nur wenn Apache der HTTPD ist, kein NGINX
- htaccess-Datein in Apache erlauben
- ErrorDocument muss in Apache erlaubt sein
- [.htaccess-Book](https://htaccessbook.com/commenting-your-htaccess-code/)

### **Fehlerseite Konfigurieren**

```apache
# Pfadangabe muss absolut zum Document root sein
ErrorDocument 404 /12-wissen/error.php
```

## Berechtigungen unter Linux

- **siehe auch umask & `umask()`**
Note that if the first digit is zero, it is not displayed. For example, if umask is set to `022`, `22` is displayed.

**chmode**

- Ein datei gehört eineme Benutzer und einer Gruppe
- Berechtigungen auf 3 Ebene
  - Benutzer
  - Gruppe
  - alle Anderen (Welt)

 **Berechtigung**

- `1` Ausführechte
- `2` Datei / Ordner ist schreibbar
- `4` Die Datei ist lesbar  

 **0754**

- `0` Steht für Oktalsystem
- Auf benutzerebene ist die Datei ausführbar , schreibbar, lesbar (`1+2+4=7`)
- Auf Gruppenebene ist die Datei lesbar und ausführbar (`4+1=5`), aber nicht schreibbar
- Für alles anderen ist die Datei nur lesbar

### Complete Tables

| Binary | Octal |    File    |    Dir     | Meaning                 |
| :----: | :---: | :--------: | :--------: | :---------------------- |
|  000   |   0   |    rw-     |    rwx     | no permissions          |
|  001   |   1   |    rw-     |    rw-     | execute only            |
|  010   |   2   |    r--     |    r-x     | write only              |
|  011   |   3   |    r--     |    r--     | write and execute       |
|  100   |   4   |    -w-     |    -wx     | read only               |
|  101   |   5   |    -w-     |    -w-     | read and execute        |
|  110   |   6   |    --x     |    --x     | read and write          |
|  111   |   7   | --- (none) | --- (none) | read, write and execute |

### Default Permissions

| Permission         | File  |       |       |  Dir  |       |       |
| ------------------ | :---: | :---: | :---: | :---: | :---: | :---: |
|                    | user  | group | other | user  | group | other |
| Predefined initial |   6   |   6   |   6   |   7   |   7   |   7   |
| Umask              |   0   |   2   |   2   |   0   |   2   |   2   |
| Default            |   6   |   4   |   4   |   7   |   5   |   5   |


To determine the umask value you want to set, subtract the value of the permissions you want from `666` (for a file) or `777` (for a directory). 

### How to change permissions for a folder and its subfolders/files

- To change all the directories to 755 (drwxr-xr-x):  
    `find /opt/lampp/htdocs -type d -exec chmod 755 {} \;`

- To change all the files to 644 (-rw-r--r--):  
    `find /opt/lampp/htdocs -type f -exec chmod 644 {} \;`
