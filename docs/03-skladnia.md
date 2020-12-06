# Składnia

## [Komentarze](http://www.freepascal.org/docs-html/ref/refse2.html)

W MP do oznaczenia komentarza jednoliniowego służą znaki `//`, dla wieloliniowego klamry `{ }`, lub `(* *)`.

```pascal
// to jest komentarz
inc(a); // to jest komentarz

(* komentarz *)

(*
  komentarz
*)

{ to
  jest
  komentarz
}
```

## Zarezerwowane słowa

#### rozkazy

```pascal
absolute           and                 array              asm               begin
case               const               div                do                downto
else               end                 file               for               function
if                 implementation      interface          main              mod
not                of                  or                 procedure         program
record             repeat              shl                shr               stack
string             then                to                 type              unit
until              uses                var                while             xor
```

#### stałe

```pascal
pi
true
false
```

## Wyrażenia

#### [Liczby](http://www.freepascal.org/docs-html/ref/refse6.html)

###### zapis decymalny
```pascal
-100
-2437325
1743
```
###### zapis hexadecymalny
```pascal
$100
$e430
$000001
```
###### zapis binarny
```pascal
%0001001010
%000000001
%001000
```
###### zapis kodami ATASCII
```pascal
'a'
'fds'
'W'
#65#32#65
#$9b
```

#### Operatory

###### arytmetyczne

```pascal
+   Addition
-   Subtraction
*   Multiplication
/   Division
DIV Integer division
MOD Remainder
```

###### bitowe

```pascal
NOT Bitwise negation (unary)
AND Bitwise and
OR  Bitwise or
XOR Bitwise xor
SHL Bitwise shift to the left
SHR Bitwise shift to the right
```

###### logiczne

```pascal
NOT logical negation (unary)
AND logical and
OR  logical or
```

###### relacji

```pascal
=   Equal
<>  Not equal
<   Less than
>   Greater than
<=  Less than or equal
>=  Greater than or equal
```

## [Dyrektywy kompilatora](http://www.freepascal.org/docs-html/prog/progch1.html#x5-40001)

Zapis dyrektyw kompilatora ma postać:

    {$dyrektywa parametry}
    {$lista_dyrektyw_przełącznikowych}

Dyrektywa stanowi komentarz, w którym pierwszy znak $ odróżnia zwykły komentarz, od dyrektywy kompilatora.

#### [CONDITIONAL](https://wiki.freepascal.org/Conditional_compilation)

```
CONDITIONAL {$IFDEF label}, {$IFNDEF label}, {$ELSE}, {$ENDIF}, {$DEFINE label}, {$UNDEF label}
```

#### [FASTMUL](https://codebase64.org/doku.php?id=base:seriously_fast_multiplication)

```
{$f $70}  // fastmul at $7000
```

Alternatywne procedury szybkiego mnożenia dla typu `BYTE`, `SHORTINT`, `WORD`, `SMALLINT`, `SHORTREAL`. Procedury zajmują **2KB** i są umieszczane od adresu __PAGE*256__.

#### [IOCHECK](https://www.freepascal.org/docs-html/prog/progsu38.html#x45-440001.2.38)

```
IOCHECK {$I+} {$I-}

{i+}  IOCHECK ON  default
{i-}  IOCHECK OFF
```

Dla {$i+} w przypadku wystąpienia błędów transmisji **I/O** (`RESET`, `REWRITE`, `BLOCKREAD`, `BLOCKWRITE`, `CLOSE`) wykonywany program zostaje zatrzymany, generowany jest komunikat błędu `ERROR xxx`. Wyłączenie `IOCHECK {$i-}` przydaje się gdy chcemy sprawdzić istnienie pliku na dysku, np.:

```pascal
function FileExists(name: TString): Boolean;
var f: file;
begin

  {$I-}     // io check off
  Assign (f, name);
  Reset (f);
  Result:=(IoResult<128) and (length(name)>0);
  Close (f);
  {$I+}     // io check

end;
```

W blokach `PROCEDURE`, `FUNCTION` dyrektywa `IOCHECK` jest zasięgu lokalnego, po zakończeniu kompilacji takiego bloku przywracana jest wartość `IOCHECK` która została określona poza takim blokiem.