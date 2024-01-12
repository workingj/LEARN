# Wie funktioniert ein UNION (C, c++, Rust)

Beispiel von [wiki/Byte-Reihenfolge](https://de.wikipedia.org/wiki/Byte-Reihenfolge)

```c
union {
    uint16_t sixteenBits;
    uint8_t twoBytes[2];
} test_endianness;

test_endianness.sixteenBits = 1 << 15; // 0x8000, 32768
    if (test_endianness.twoBytes[0] != 0) {
     // Das Programm läuft auf einer Big-Endian-Maschine.
    }
    else {
        // Das Programm läuft auf einer Little-Endian-Maschine.
    }
```
