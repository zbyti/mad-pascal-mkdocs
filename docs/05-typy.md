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

## [tablice](https://www.freepascal.org/docs-html/ref/refsu14.html#x38-500003.3.1)

Tablice w **MP** są tylko statyczne, jednowymiarowe lub dwuwymiarowe z początkowym indeksem równym `0`, np.:

```pascal
var tb: array [0..100] of word;
var tb2: array [0..15, 0..31] of Boolean;
```

W przypadku początkowego indeksu innego niż zero zostanie wygenerowany błąd **Error: Array lower bound is not zero**.

W pamięci tablica reprezentowana jest przez wskaźnik `POINTER`, wskaźnik jest adresem tablicy w pamięci `WORD`. Najszybszą metodą odwołania się do tablicy z poziomu assemblera jest zastosowanie przedrostka `ADR.`, np.:

    asm
    { lda adr.tb,y   ; bezpośrednie odwołanie do tablicy TB
      lda tb         ; odwołanie do wskaźnika tablicy TB
    };

Kompilator generuje kod dla tablic zależnie od ich deklaracji:

* gdy nie przekracza 256 bajtów
```pascal
array [0..255] of byte
array [0..127] of word
array [0..63] of cardinal
```

Gdy liczba bajtów zajmowanych przez tablicę nie przekracza 256 bajtów generowany jest najszybszy kod odwołujący się bezpośrednio do adresu tablicy (przedrostek `ADR.`) z pominięciem wskaźnika. Dla takiej tablicy nie ma możliwości zmiany adresu.

    ldy #118
    lda adr.tb,y

* gdy liczba elementów tablicy wynosi `1`
```pascal
array [0..0] of type
```

Gdy liczba elementów tablicy wynosi `1` jest ona traktowana specjalnie. Generowany kod odwołuje się do tablicy poprzez wzkaźnik. Istnieje możliwość ustalenia nowego adresu takiej tablicy.

    lda TB
    add I
    tay
    lda TB+1
    adc #$00
    sta bp+1
    lda (bp),y

* gdy przekracza 256 bajtów
```pascal
array [0..255+1] of byte
array [0..127+1] of word
array [0..63+1] of cardinal
```

Gdy liczba bajtów zajmowanych przez tablicę przekracza 256 bajtów generowany kod odwołuje się do tablicy poprzez wskaźnik. Istnieje możliwość ustalenia nowego adresu takiej tablicy.

    lda TB
    add I
    tay
    lda TB+1
    adc #$00
    sta bp+1
    lda (bp),y

