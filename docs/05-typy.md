# Typy

## [porządkowy](https://www.freepascal.org/docs-html/ref/refsu4.html#x26-250003.1.1)

|Type    |Range                    |Size in bytes|
|:-------|:-----------------------:|:-----------:|
|BYTE    |0 .. 255                 |1            |
|SHORTINT|-128 .. 127              |1            |
|WORD    |0 .. 65535               |2            |
|SMALLINT|-32768 .. 32767          |2            |
|CARDINAL|0 .. 4294967295          |4            |
|LONGWORD|0 .. 4294967295          |4            |
|DWORD   |0 .. 4294967295          |4            |
|UINT32  |0 .. 4294967295          |4            |
|INTEGER |-2147483648 .. 2147483647|4            |
|LONGINT |-2147483648 .. 2147483647|4            |

## [logiczny](https://www.freepascal.org/docs-html/ref/refsu4.html#x26-250003.1.1)

|Type    |Ord(True)                |Size in bytes|
|:-------|:-----------------------:|:-----------:|
|BYTE    |0 .. 255                 |1            |

## [wyliczeniowy](https://www.freepascal.org/docs-html/ref/refsu4.html#x26-280003.1.1)

Typ wyliczeniowy w **MP** został zaimplementowany w podstawowej postaci, tzn.:

```pascal
Type
  Days = (monday,tuesday,wednesday,thursday,friday,
          saturday,sunday);

  Joy = (right_down = 5, right_up, right, left_down = 9, left_up, left, down = 13, up, none);
```
Typ wyliczeniowy przechowywany jest tylko w pamięci kompilatora **MP**, do pliku wynikowego nie zostaną zapisane jakiekolwiek informacje dotyczące pól typu wyliczeniowego. Dopuszczalne jest użycie komendy `ORD`, `SIZEOF` oraz rzutowania dla typu wyliczeniowego.

```pascal
var
   d: Days;

   d:=friday;
   writeln(ord(d));
   writeln(ord(sunday));
   writeln(sizeof(days));
   writeln(sizeof(monday));

   d:=days(20);

   case d of
    sunday: writeln('sunday');
   end;
```

Aktualnie kompilator **MP** nie sprawdzi poprawności typów wyliczeniowych dla operacji `IF ELSE`.

## [rzeczywisty](https://www.freepascal.org/docs-html/ref/refsu5.html#x27-300003.1.2)

|Type             |Range                   |Size in bytes|
|:----------------|:----------------------:|:-----------:|
|SHORTREAL (Q8.8) |-128..127               |2            |
|REAL (Q24.8)     |-8388607..8388608       |4            |
|SINGLE (IEEE-754)|1.5E-45 .. 3.4E38       |4            |
|FLOAT (IEEE-754) |1.5E-45 .. 3.4E38       |4            |

Konwersja typu `FLOAT` / `SINGLE` do liczby całkowitej dostępna jest tylko w zakresie `INTEGER`. Typ `INTEGER` nie pozwoli zaprezentować maksymalnej wartości `3.4E38` typu `FLOAT` / `SINGLE`.

## [znakowy](https://www.freepascal.org/docs-html/ref/refsu6.html#x29-320003.2.1)

|Type    |Range                    |Size in bytes|
|:-------|:-----------------------:|:-----------:|
|CHAR    |ATASCII (0 .. 255)       |1            |
|STRING  |1 .. 255                 |256          |
|PCHAR   |0 .. 65535               |2            |

Ciąg znaków `STRING` reprezentowany jest jako tablica o możliwym maksymalnym rozmiarze `[0..255]`. Pierwszym bajtem takiej tablicy `[0]` jest długość ciągu z zakresu `0..255`. Od bajtu `[1..]` zaczyna się właściwy ciąg znaków.

Ciąg znaków `PCHAR` reprezentowany jest przez wskaźnik do typu `CHAR`. Znakiem końca ciągu `PCHAR` jest znak `#0`.

Dopuszczalne jest użycie dodatkowych znaków po końcowym apostrofie, takich jak `*`, `~`. Znak `*` oznacza ciąg w inwersie, tylda `~` ciąg w kodach **ANTIC-a**.

Innym sposobem modyfikacji wyprowadzanych znaków jest użycie systemowej zmiennej `TextAttr`, każdy znak wyprowadzany na ekran jest zwiększany o wartość `TextAttr` (domyślnie = 0).

```pascal
a: string = 'Atari'*;         // ciąg znaków w inwersie
b: string = 'Spectrum'~;      // ciąg znaków w kodach ANTIC-a
c: char = 'X'~*;              // znak w inwersie, kodach ANTIC-a
```

## [wskaźniki](https://www.freepascal.org/docs-html/ref/refse15.html)

|Type    |Ord(True)                |Size in bytes|
|:-------|:-----------------------:|:-----------:|
|POINTER |0 .. 65535               |2            |

Wskaźniki w **MP** mogą być typowane i bez określonego typu, np.:

```pascal
 a: ^word;         // wskaźnik typowany na słowo
 b: pointer;       // wskaźnik bez typu
```

Niezaincjowany wskaźnik najczęściej będzie miał adres `$0000`, należy zadbać aby przed jego wykorzystaniem zaincjować go adresem odpowiedniej zmiennej, np.:

    a := @tmp;         // wskaźnikowi A zostaje przypisany adres zmiennej TMP

Jeśli tego nie zrobimy to w przypadku uruchomienia takiego programu na **PC** spowodujemy błąd ochrony pamięci **Access Violation**.

Zwiększanie wskaźnika przez `INC` zwiększy go o rozmiar typu na jaki wskazuje. Zmniejszenie wskaźnika przez `DEC` zmniejszy go o rozmiar typu na jaki wskazuje. Jeśli typ jest nieokreślony, wówczas domyślną wartością zwiększania/zmniejszanie będzie 1.
