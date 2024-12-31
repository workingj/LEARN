# REGULÄRE AUSDRÜCKE

- [REGULÄRE AUSDRÜCKE](#reguläre-ausdrücke)
  - [Links](#links)
  - [Character-Classes](#character-classes)
  - [Quantifier](#quantifier)
  - [Metacharacters](#metacharacters)
  - [Bracket Expression](#bracket-expression)
  - [Capture Groups](#capture-groups)
  - [Cheatcheet](#cheatcheet)
  - [Examples](#examples)

## Links

- [Validator - https://regexr.com/](https://regexr.com/)
- [Cheetsheet](https://www.debuggex.com/cheatsheet/regex/pcre)

## Character-Classes

- Sind greedy, nehmen so viele Zeichen wie sie können

- `\d` Die Ziffern:0-9
- `\D` Alle Zeichen bis auf: 0-9
- `\s` White-Space, Leerzeichen, Tabulatoren, Zeilenumbrüche...
- `\S` Alles bis auf \s
- `\w` Kleinbuchstaben, Großbuchstaben, Ziffern, Unterstriche...
- `\W` Alles bis auf \w
- `.` Ein beliebiges Zeichen (bis auf Zeilenumbruch)

## Quantifier

- Sind auch greedy und weiten sich aus auf mögliche Zeichen

- `*` 0x bis belibig oft
- `+` 1x bis belibig oft
- `?` 0x oder 1x
- `{n}` Exavt `n` mal
- `{n,}` Mindestens `n` mal
- `{n,m}` `n` bis `m` mal

## Metacharacters

- `^` ssert start of string (or line, in multiline mode)
- `$` assert end of string (or line, in multiline mode)

There are two different sets of metacharacters: those that  are  recog nized  anywhere in the pattern except within square brackets, and those that are recognized within square brackets.  Outside  square  brackets, the metacharacters are as follows:

- `\` general escape character with several uses
- `.` match any character except newline (by default)
- `[` start character class definition
- `|` start of alternative branch
- `(` start subpattern
- `)` end subpattern
- `?` extends the meaning of `(`
  - also 0 or 1 quantifier
  - also quantifier minimizer
- `*` 0 or more quantifier
- `+` 1 or more quantifier
  - also "possessive quantifier"
- `{` start min/max quantifier

Part  of  a  pattern  that is in square brackets is called a "character class". In a character class the only metacharacters are:

- `\` general escape character
- `^` negate the class, but only if the first character
- `-` indicates character range
- `[` POSIX character class (only if followed by POSIXsyntax)
- `]` terminates the character class

## Bracket Expression

- steht immer für ein Zeichen
- Groß und klein nicht mischen [a-Z]

- `[abc]` Ein Zeichen aus 'a','b','c'
- `[ABC]` Ein Zeichen aus 'a','b','c'
- `[a-k]` Ein Zeichen aus dem Bereich 'a' bis 'k' (in Unicode)
- `[A-Za-z0-9]` Ein Zeichen zwischen 'A' bis 'Z', 'a' und 'z' und alle Ziffern von 0 bis 9
- `[öäüßÖÄÜ]` Ein Zeichen welches ein Umlaut ist
- `[A-Za-z0-9öäüßÖÄÜ]` Ein Zeichen zwischen A-Z, a-z, 0-9 oder eins aus 'öäüßÖÄÜ'
- `[A-Za-z\d]` Ein Zeichen zwischen 'A' bis 'Z', 'a' und 'z' und alle Ziffern von 0 bis 9
- `[^A-Z]` `^` negiert hier den Ausdruck

## Capture Groups

- `/(.*)\@(.*)/'`
- `/^(https?)/'`

## Cheatcheet

### Regular Expression Basics

- `.` Any character except newline
- `a` The character a
- `ab` The string ab
- `a|b` a or b
- `a*` 0 or more a's
- `\` Escapes a special character

### Regular Expression Quantifiers

- `*` 0 or more
- `+` 1 or more
- `?` 0 or 1
- `{2}` Exactly 2
- `{2, 5}` Between 2 and 5
- `{2,}` 2 or more
Default is greedy. Append ? for reluctant.

### Regular Expression Groups

- `(...)` Capturing group
- `(?P<Y>...)` Capturing group named Y
- `(?:...)` Non-capturing group
- `(?>...)` Atomic group
- `(?|...)` Duplicate group numbers
- `\Y` Match the Y'th captured group
- `(?P=Y)` Match the named group Y
- `(?R)` Recurse into entire pattern
- `(?Y)` Recurse into numbered group Y
- `(?&Y)` Recurse into named group Y
- `\g{Y}` Match the named or numbered group Y
- `\g<Y>` Recurse into named or numbered group Y
- `(?#...)` Comment

### Regular Expression Character Classes

- `[ab-d]` One character of: a, b, c, d
- `[^ab-d]` One character except: a, b, c, d
- `[\b]` Backspace character
- `\d` One digit
- `\D` One non-digit
- `\s` One whitespace
- `\S` One non-whitespace
- `\w` One word character
- `\W` One non-word character

### Regular Expression Assertions

- `^` Start of string
- `\A` Start of string, ignores m flag
- `$` End of string
- `\Z` End of string, ignores m flag
- `\b` Word boundary
- `\B` Non-word boundary
- `\G` Start of match
- `(?=...)` Positive lookahead
- `(?!...)` Negative lookahead
- `(?<=...)` Positive lookbehind
- `(?<!...)` Negative lookbehind
- `(?()|)` Conditional

### Regular Expression Escapes

- `\Q..\E` Remove special meaning

### Regular Expression Flags

- `i` Ignore case
- `m` ^ and $ match start and end of line
- `s` . matches newline as well
- `x` Allow spaces and comments
- `J` Duplicate group names allowed
- `U` Ungreedy quantifiers
- `(?iLmsux)` Set flags within regex

### Regular Expression Special Characters

- `\n` Newline
- `\r` Carriage return
- `\t` Tab
- `\0` Null character
- `\YYY` Octal character YYY
- `\xYY` Hexadecimal character YY
- `\x{YY}` Hexadecimeal character YY
- `\cY` Control character Y

### Regular Expression Posix Classes

- `[:alnum:]` Letters and digits
- `[:alpha:]` Letters
- `[:ascii:]` Ascii codes 0 - 127
- `[:blank:]` Space or tab only
- `[:cntrl:]` Control characters
- `[:digit:]` Decimal digits
- `[:graph:]` Visible characters, except space
- `[:lower:]` Lowercase letters
- `[:print:]` Visible characters
- `[:punct:]` Visible punctuation characters
- `[:space:]` Whitespace
- `[:upper:]` Uppercase letters
- `[:word:]` Word characters
- `[:xdigit:]` Hexadecimal digits

## Examples

- `hello` contains `{hello}`
- `gray|grey` contains `{gray, grey}`
- `gr(a|e)y` contains `{gray, grey}`
- `gr[ae]y` contains `{gray, grey}`
- `b[aeiou]bble` contains `{babble, bebble, bibble, bobble, bubble}`
- `[b-chm-pP]at|ot` contains `{bat, cat, hat, mat, nat, oat, pat, Pat, ot}`
- `colou?r` contains `{color, colour}`
- `rege(x(es)?|xps?)` contains `{regex, regexes, regexp, regexps}`
- `go*gle` contains `{ggle, gogle, google, gooogle, goooogle, ...}`
- `go+gle` contains `{gogle, google, gooogle, goooogle, ...}`
- `g(oog)+le` contains `{google, googoogle, googoogoogle, googoogoogoogle, ...}`
- `z{3}` contains `{zzz}`
- `z{3,6}` contains `{zzz, zzzz, zzzzz, zzzzzz}`
- `z{3,}` contains `{zzz, zzzz, zzzzz, ...}`
- `[Bb]rainf\*\*k` contains `{Brainf**k, brainf**k}`
- `\d` contains `{0,1,2,3,4,5,6,7,8,9}`
- `\d{5}(-\d{4})?` contains a United States zip code
- `1\d{10}` contains an 11-digit string starting with a 1
- `[2-9]|[12]\d|3[0-6]` contains an integer in the range 2..36 inclusive
- `Hello\nworld` contains Hello followed by a newline followed by world
- `mi.....ft` contains a nine-character (sub)string beginning with mi and ending with ft (Note: depending on context, the dot stands either for “any character at all” or “any character except a newline”.) Each dot is allowed to match a different character, so both microsoft and minecraft will match.
- `\d+(\.\d\d)?` contains a positive integer or a floating point number with exactly two characters after the decimal point.
- `[^i*&2@]` contains any character other than an i, asterisk, ampersand, 2, or at-sign.
- `//[^\r\n]*[\r\n]` contains a Java or C# slash-slash comment
- `^dog` begins with "dog"
- `dog$` ends with "dog"
- `^dog$` is exactly "dog"
