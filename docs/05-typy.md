# Typy

## [porządkowy](https://www.freepascal.org/docs-html/ref/refsu4.html#x26-250003.1.1)

|Type    |Range                    |Size|
|:-------|:-----------------------:|:--:|
|BYTE    |0 .. 255                 |1   |
|SHORTINT|-128 .. 127              |1   |
|WORD    |0 .. 65535               |2   |
|SMALLINT|-32768 .. 32767          |2   |
|CARDINAL|0 .. 4294967295          |4   |
|LONGWORD|0 .. 4294967295          |4   |
|DWORD   |0 .. 4294967295          |4   |
|UINT32  |0 .. 4294967295          |4   |
|INTEGER |-2147483648 .. 2147483647|4   |
|LONGINT |-2147483648 .. 2147483647|4   |

## [logiczny](https://www.freepascal.org/docs-html/ref/refsu4.html#x26-250003.1.1)

|Type    |Ord(True)                |Size|
|:-------|:-----------------------:|:--:|
|BYTE    |0 .. 255                 |1   |

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